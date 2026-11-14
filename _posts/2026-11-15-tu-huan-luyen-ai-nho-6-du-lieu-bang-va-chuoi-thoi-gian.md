---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: "Tự huấn luyện mô hình AI nhỏ (6): Dữ liệu dạng bảng và chuỗi thời gian"
subtitle: "LightGBM, AutoGluon, TabPFN, fine-tune Chronos-2 và huấn luyện NHITS từ đầu"
date: 2026-11-15 08:50:00 +0700
tags:
- AI
- Machine Learning
- Tabular
- Time Series
- LightGBM
- AutoGluon
- Chronos
- TabPFN
series: "Tự huấn luyện mô hình AI nhỏ"
series_order: 6
---

> Bài cuối của series. Dữ liệu dạng bảng (bảng tính, bảng trong cơ sở dữ liệu) và chuỗi thời gian (doanh số theo ngày, cảm biến theo phút) là loại dữ liệu doanh nghiệp có nhiều nhất, và cũng là nơi mô hình nhỏ thắng thế rõ nhất. Phần lớn nội dung bài này chạy được trên CPU. Kiến thức nền nằm ở [bài 1](/2026/11/15/tu-huan-luyen-ai-nho-1-tong-quan/). Code là khung cốt lõi, chưa chạy kiểm chứng trên dữ liệu thật của bạn.

- [Điểm khác biệt của lĩnh vực này](#điểm-khác-biệt-của-lĩnh-vực-này)
- [Technical stack](#technical-stack)
- [Dữ liệu đầu vào](#dữ-liệu-đầu-vào)
- [Các cách làm với dữ liệu bảng](#các-cách-làm-với-dữ-liệu-bảng)
- [Từng bước với dữ liệu bảng](#từng-bước-với-dữ-liệu-bảng)
- [Các cách làm với chuỗi thời gian](#các-cách-làm-với-chuỗi-thời-gian)
- [Từng bước fine-tune Chronos-2 bằng AutoGluon](#từng-bước-fine-tune-chronos-2-bằng-autogluon)
- [Từng bước huấn luyện NHITS từ đầu](#từng-bước-huấn-luyện-nhits-từ-đầu)
- [Lưu ý quan trọng](#lưu-ý-quan-trọng)
- [Tổng kết series](#tổng-kết-series)
- [Nguồn tham khảo](#nguồn-tham-khảo)

## Điểm khác biệt của lĩnh vực này

Ở bốn lĩnh vực trước, fine-tune gần như luôn thắng huấn luyện từ đầu. Ở đây thì ngược lại trong nhiều trường hợp:

- **Cây tăng cường gradient** (LightGBM, XGBoost, CatBoost) huấn luyện từ đầu trên CPU trong vài phút vẫn là mốc rất khó vượt cho dữ liệu bảng.
- **Mô hình nền tảng cho bảng** (TabPFN, TabICL) không fine-tune theo nghĩa thông thường. Chúng nhận cả tập huấn luyện làm ngữ cảnh và dự đoán trong một lượt chạy xuôi, giống cách mô hình ngôn ngữ học từ ví dụ trong prompt.
- **Mô hình nền tảng cho chuỗi thời gian** (Chronos-2, TimesFM, Moirai) dự báo zero-shot khá tốt và fine-tune được bằng LoRA.
- Mỗi bộ dữ liệu có cột và ý nghĩa riêng, nên kiến thức chuyển giao giữa các bài toán ít hơn nhiều so với ảnh hay ngôn ngữ.

Vì vậy bài này trình bày cả hai hướng với trọng số ngang nhau, và phần "từ đầu" ở đây là lựa chọn thực dụng chứ không chỉ để học.

## Technical stack

| Nhóm | Thành phần | Ghi chú |
|---|---|---|
| Xử lý dữ liệu | pandas, Polars, DuckDB, NumPy | Đọc, làm sạch, gộp bảng |
| Mô hình bảng cổ điển | scikit-learn, LightGBM, XGBoost, CatBoost | Chạy CPU. CatBoost xử lý cột phân loại tốt |
| AutoML | AutoGluon (bảng và chuỗi thời gian), FLAML | Tự thử nhiều mô hình và ghép lại |
| Mô hình nền tảng cho bảng | TabPFN: v2, 2.5, 2.6, 3, 3.5 (Prior Labs) | Bản 3.5 nhận tới 1 triệu dòng và 20000 cột theo tài liệu. Trọng số từ bản 2.5 trở đi là phi thương mại. TabPFNv2 dùng giấy phép kiểu Apache 2.0 kèm yêu cầu ghi nguồn, giới hạn 10000 dòng và 500 cột |
| | TabICL, Kumo Tabular | Các lựa chọn khác, xem giấy phép từng mô hình |
| Mạng nơ-ron cho bảng | TabM, RealMLP, FT-Transformer (qua pytorch-tabular hoặc AutoGluon) | Huấn luyện từ đầu, 2 đến 8 GB |
| Dò siêu tham số | Optuna | Tìm kiếm tự động |
| Giải thích mô hình | SHAP, permutation importance | Biết cột nào ảnh hưởng dự đoán |
| Dự báo cổ điển | statsforecast (AutoARIMA, AutoETS, Theta, Seasonal Naive) | Rất nhanh, mốc bắt buộc |
| Dự báo bằng học máy | mlforecast (LightGBM kèm đặc trưng trễ) | Thường thắng trên dữ liệu bán lẻ |
| Mô hình nền tảng cho chuỗi thời gian | Chronos-2 (Amazon, 120M tham số), Chronos-Bolt | Chronos-2 hỗ trợ biến ngoại sinh dạng số và phân loại, ngữ cảnh tới 8192 điểm, dự báo tới 1024 bước |
| | TimesFM (Google), Moirai (Salesforce) | Các lựa chọn khác |
| Mạng nơ-ron dự báo | NeuralForecast (NHITS, NBEATS, PatchTST, TFT), Darts, GluonTS | Huấn luyện từ đầu |
| Triển khai | joblib hoặc ONNX cho mô hình cây, FastAPI, tác vụ theo lịch | Mô hình bảng thường chạy theo lô |

## Dữ liệu đầu vào

**Dữ liệu bảng**

- Một bảng, mỗi dòng một mẫu, một cột mục tiêu. Ví dụ dự đoán máy có hỏng trong 7 ngày tới: mỗi dòng là một máy tại một thời điểm, các cột là số giờ chạy, nhiệt độ trung bình, số lần báo lỗi, loại máy.
- Định dạng CSV hoặc Parquet. Kiểu dữ liệu rõ ràng: số, phân loại, ngày giờ, văn bản ngắn.
- Số lượng: từ vài trăm dòng đã làm được. Dưới 10000 dòng là vùng TabPFN mạnh nhất. Trên 100000 dòng thì cây tăng cường và mạng nơ-ron tận dụng tốt hơn.

**Chuỗi thời gian**

- Dạng dài, ba cột bắt buộc: mã chuỗi, thời điểm, giá trị.

```text
item_id,timestamp,target,gia_ban,khuyen_mai
SP001,2026-01-01,120,15000,0
SP001,2026-01-02,135,15000,1
SP002,2026-01-01,40,82000,0
```

- Tần suất đều (giờ, ngày, tuần). Thời điểm thiếu phải được điền rõ ràng: bằng 0 nếu thật sự không bán, để trống nếu mất dữ liệu.
- **Biến ngoại sinh:** loại biết trước trong tương lai (lịch, ngày lễ, giá bán và khuyến mãi đã lên kế hoạch) và loại chỉ biết trong quá khứ (thời tiết thực tế, lượt truy cập).
- Lịch sử nên dài ít nhất hai chu kỳ mùa vụ. Với dữ liệu ngày có mùa vụ theo năm, cần từ hai năm.

**Ba lỗi dữ liệu gây hại nhiều nhất**

1. **Rò rỉ mục tiêu.** Một cột chứa thông tin chỉ có sau khi sự việc xảy ra, ví dụ cột "ngày sửa chữa" khi đang dự đoán hỏng hóc. Mô hình đạt điểm tuyệt đối khi kiểm thử và vô dụng khi chạy thật. Với mỗi cột, hãy hỏi: tại thời điểm cần dự đoán, giá trị này đã có chưa?
2. **Tách tập ngẫu nhiên khi dữ liệu có thời gian.** Phải huấn luyện trên quá khứ và kiểm thử trên tương lai.
3. **Cùng một thực thể nằm ở cả hai tập.** Nếu một khách hàng có nhiều dòng, tách theo khách hàng (GroupKFold).

## Các cách làm với dữ liệu bảng

| # | Cách làm | Độ khó | Phần cứng | Khi nào dùng |
|---|---|---|---|---|
| 1 | Mốc đơn giản: hồi quy tuyến tính, hồi quy logistic, cây quyết định | Rất dễ | CPU | Luôn làm đầu tiên |
| 2 | LightGBM, XGBoost hoặc CatBoost với tham số mặc định | Dễ | CPU | Mặc định cho hầu hết bài toán |
| 3 | TabPFN chạy xuôi, không huấn luyện | Dễ | GPU 8 GB, bộ dữ liệu rất nhỏ chạy được CPU | Bảng nhỏ đến vừa, cần kết quả tốt ngay. Chú ý giấy phép |
| 4 | Cây tăng cường kèm dò siêu tham số bằng Optuna | Trung bình | CPU, vài chục phút đến vài giờ | Cần thêm vài phần trăm |
| 5 | AutoGluon với preset chất lượng cao | Trung bình | CPU nhiều nhân, GPU tuỳ chọn | Độ chính xác cao nhất với ít công sức, mô hình cuối nặng |
| 6 | Mạng nơ-ron cho bảng huấn luyện từ đầu (TabM, RealMLP, FT-Transformer) | Khó | GPU 4 đến 8 GB | Bảng lớn, hoặc cần ghép với ảnh và văn bản |
| 7 | Fine-tune mô hình nền tảng cho bảng trên dữ liệu riêng | Khó | GPU 12 đến 24 GB | Hiếm khi cần. Thử sau khi các cách trên đã hết dư địa |

Theo báo cáo của Prior Labs, TabPFN-2.5 trong một lượt chạy xuôi vượt các mô hình cây đã dò tham số và ngang AutoGluon 1.4 chạy bốn giờ, còn TabPFN-3.5 thắng XGBoost và CatBoost ở phần lớn bộ dữ liệu trong các bộ chuẩn họ dùng. Đây là số liệu của chính tác giả. Cũng theo báo cáo đó, mạng MLP dò kỹ vẫn giữ kết quả tốt nhất trên dữ liệu tách theo nhóm, tách theo thời gian và dữ liệu lớn. Hãy tự so sánh trên dữ liệu của bạn.

## Từng bước với dữ liệu bảng

Ví dụ xuyên suốt: bảng `may_moc.csv`, cột mục tiêu `hong_trong_7_ngay` (0 hoặc 1), có cột `ngay_ghi_nhan` và `ma_may`.

**Bước 1. Cài đặt.**

```bash
pip install pandas scikit-learn lightgbm optuna shap autogluon tabpfn
```

**Bước 2. Tách tập theo thời gian và lấy mốc.**

```python
import pandas as pd
from sklearn.metrics import roc_auc_score, average_precision_score

df = pd.read_csv("may_moc.csv", parse_dates=["ngay_ghi_nhan"]).sort_values("ngay_ghi_nhan")
target = "hong_trong_7_ngay"
drop = [target, "ngay_ghi_nhan", "ma_may"]

for c in df.select_dtypes("object").columns:
    if c not in drop:
        df[c] = df[c].astype("category")   # LightGBM đọc trực tiếp cột phân loại

n = len(df)
train, valid, test = df.iloc[:int(n*0.7)], df.iloc[int(n*0.7):int(n*0.85)], df.iloc[int(n*0.85):]

X_tr, y_tr = train.drop(columns=drop), train[target]
X_va, y_va = valid.drop(columns=drop), valid[target]
X_te, y_te = test.drop(columns=drop), test[target]

print("Tỷ lệ hỏng:", y_tr.mean())   # mốc ngây thơ: luôn đoán theo tỷ lệ này
```

Với dữ liệu mất cân bằng (hỏng hóc hiếm), dùng diện tích dưới đường precision-recall thay cho độ chính xác thông thường.

**Bước 3. Huấn luyện LightGBM từ đầu.**

```python
import lightgbm as lgb

model = lgb.LGBMClassifier(n_estimators=2000, learning_rate=0.03, num_leaves=31,
                           subsample=0.8, subsample_freq=1, colsample_bytree=0.8)
model.fit(X_tr, y_tr, eval_set=[(X_va, y_va)], eval_metric="average_precision",
          callbacks=[lgb.early_stopping(100), lgb.log_evaluation(100)])

p = model.predict_proba(X_te)[:, 1]
print("AUC:", roc_auc_score(y_te, p), "PR-AUC:", average_precision_score(y_te, p))
```

Dừng sớm trên tập validation tự chọn số cây. Chạy vài giây đến vài phút trên CPU.

**Bước 4. Dò siêu tham số bằng Optuna.**

```python
import optuna

def objective(trial):
    params = dict(
        n_estimators=3000,
        learning_rate=trial.suggest_float("learning_rate", 0.01, 0.2, log=True),
        num_leaves=trial.suggest_int("num_leaves", 8, 256, log=True),
        min_child_samples=trial.suggest_int("min_child_samples", 5, 200, log=True),
        subsample=trial.suggest_float("subsample", 0.5, 1.0), subsample_freq=1,
        colsample_bytree=trial.suggest_float("colsample_bytree", 0.4, 1.0),
        reg_lambda=trial.suggest_float("reg_lambda", 1e-3, 10, log=True),
        verbose=-1,
    )
    m = lgb.LGBMClassifier(**params)
    m.fit(X_tr, y_tr, eval_set=[(X_va, y_va)], eval_metric="average_precision",
          callbacks=[lgb.early_stopping(100, verbose=False)])
    return average_precision_score(y_va, m.predict_proba(X_va)[:, 1])

study = optuna.create_study(direction="maximize")
study.optimize(objective, n_trials=50)
print(study.best_params)
```

Huấn luyện lại với tham số tốt nhất rồi đo trên tập test đúng một lần. Thông thường bước này thêm được 1 đến 3 điểm phần trăm. Tạo đặc trưng tốt (tỷ lệ, hiệu, trung bình trượt theo máy) thường cho nhiều hơn thế.

**Bước 5. So với TabPFN.**

```python
from tabpfn import TabPFNClassifier

clf = TabPFNClassifier()               # tự tải trọng số ở lần chạy đầu
clf.fit(X_tr, y_tr)                    # không huấn luyện, chỉ ghi nhớ ngữ cảnh
p = clf.predict_proba(X_te)[:, 1]
print("TabPFN PR-AUC:", average_precision_score(y_te, p))
```

Kiểm tra bản trọng số nào đang được tải và giấy phép của nó. Từ bản 2.5, trọng số chỉ dành cho mục đích phi thương mại, dùng trong sản xuất cần giấy phép doanh nghiệp. Bảng lớn cần nhiều VRAM vì cả tập huấn luyện nằm trong ngữ cảnh, khi đó lấy mẫu bớt dòng.

**Bước 6. So với AutoGluon.**

```python
from autogluon.tabular import TabularPredictor

predictor = TabularPredictor(label=target, eval_metric="average_precision").fit(
    train.drop(columns=["ngay_ghi_nhan", "ma_may"]),
    tuning_data=valid.drop(columns=["ngay_ghi_nhan", "ma_may"]),
    presets="high_quality", time_limit=3600, use_bag_holdout=True,
)
print(predictor.leaderboard(test.drop(columns=["ngay_ghi_nhan", "ma_may"])))
```

Truyền `tuning_data` để AutoGluon tôn trọng cách tách theo thời gian thay vì tự tách ngẫu nhiên.

**Bước 7. Giải thích và kiểm tra rò rỉ.**

```python
import shap

explainer = shap.TreeExplainer(model)
shap.summary_plot(explainer.shap_values(X_te), X_te)
```

Nếu một cột chiếm gần hết tầm ảnh hưởng và kết quả đẹp bất thường, gần như chắc chắn đó là rò rỉ mục tiêu.

**Bước 8. Triển khai.** Lưu mô hình bằng `joblib.dump`, lưu kèm danh sách cột và kiểu dữ liệu. Chọn ngưỡng quyết định theo chi phí thực tế của báo nhầm và bỏ sót. Theo dõi phân bố dữ liệu đầu vào theo thời gian và huấn luyện lại định kỳ.

## Các cách làm với chuỗi thời gian

| # | Cách làm | Độ khó | Phần cứng | Khi nào dùng |
|---|---|---|---|---|
| 1 | Mốc ngây thơ: lặp lại giá trị cùng kỳ mùa trước (Seasonal Naive) | Rất dễ | CPU | Bắt buộc. Nhiều mô hình phức tạp không thắng nổi mốc này |
| 2 | Mô hình thống kê: AutoETS, AutoARIMA, Theta | Dễ | CPU | Ít chuỗi, lịch sử dài, mùa vụ rõ |
| 3 | Chronos-2 zero-shot | Dễ | CPU hoặc GPU 2 đến 4 GB | Kết quả tốt ngay, không cần huấn luyện |
| 4 | LightGBM với đặc trưng trễ (mlforecast) | Trung bình | CPU | Nhiều chuỗi, nhiều biến ngoại sinh |
| 5 | Fine-tune Chronos-2 bằng LoRA qua AutoGluon | Trung bình | GPU khoảng 8 GB (ước lượng) | Hơn 100 chuỗi, lịch sử đủ dài |
| 6 | Huấn luyện từ đầu NHITS hoặc PatchTST | Trung bình đến khó | GPU 2 đến 8 GB, chạy được CPU | Rất nhiều dữ liệu cùng loại, cần mô hình bé và nhanh |
| 7 | Ghép nhiều mô hình (ensemble) | Trung bình | Tổng của các mô hình thành phần | Thường cho kết quả tốt nhất |

## Từng bước fine-tune Chronos-2 bằng AutoGluon

Lý do chọn: theo tài liệu AutoGluon, Chronos-2 đứng đầu các bộ chuẩn fev-bench, GIFT-Eval và Chronos Bench II tại thời điểm tháng 12/2025, hỗ trợ biến ngoại sinh, và fine-tune mặc định bằng LoRA. Mô hình chỉ 120 triệu tham số. Tài liệu được kiểm thử trên GPU 24 GB, nhưng với kích thước này và LoRA thì mốc 8 GB là ước lượng hợp lý, hãy giảm batch nếu thiếu bộ nhớ.

**Bước 1. Cài đặt và nạp dữ liệu.**

```bash
pip install "autogluon.timeseries"
```

```python
import pandas as pd
from autogluon.timeseries import TimeSeriesDataFrame, TimeSeriesPredictor

df = pd.read_csv("doanh_so.csv", parse_dates=["timestamp"])
data = TimeSeriesDataFrame.from_data_frame(df, id_column="item_id", timestamp_column="timestamp")

H = 28                                           # dự báo 28 ngày
train_data, test_data = data.train_test_split(H) # giữ 28 ngày cuối của mỗi chuỗi để kiểm thử
```

**Bước 2. Mốc ngây thơ và zero-shot.**

```python
predictor = TimeSeriesPredictor(
    prediction_length=H, target="target", eval_metric="MASE",
    known_covariates_names=["gia_ban", "khuyen_mai"],
).fit(
    train_data,
    hyperparameters={
        "SeasonalNaive": {},
        "AutoETS": {},
        "Chronos2": [
            {"ag_args": {"name_suffix": "ZeroShot"}},
            {"fine_tune": True, "ag_args": {"name_suffix": "FineTuned"}},
        ],
    },
    enable_ensemble=True,
)
print(predictor.leaderboard(test_data))
```

Một lệnh `fit` chạy cả bốn mô hình và ghép chúng. AutoGluon in điểm theo quy ước càng cao càng tốt, nên MASE hiện ra dưới dạng số âm. MASE dưới 1 (về trị tuyệt đối) nghĩa là tốt hơn mốc ngây thơ.

**Bước 3. Điều chỉnh việc fine-tune.**

```python
{"fine_tune": True,
 "fine_tune_mode": "lora",        # mặc định. "full" để cập nhật toàn bộ trọng số
 "fine_tune_lr": 1e-4,
 "fine_tune_steps": 2000,
 "fine_tune_batch_size": 32,      # giảm xuống 8 hoặc 16 nếu hết bộ nhớ
 "ag_args": {"name_suffix": "FineTuned"}}
```

Khuyến nghị của tài liệu AutoGluon: chỉ fine-tune khi có **hơn khoảng 100 chuỗi** và độ dài lịch sử trung vị **lớn hơn 3 lần** độ dài dự báo. Ít hơn thì dễ học vẹt và bản zero-shot thường tốt hơn. Trong ví dụ của chính tài liệu, fine-tune chỉ cải thiện nhẹ so với zero-shot (điểm kiểm thử -0,688 so với -0,696), còn việc thêm biến ngoại sinh tạo khác biệt lớn hơn nhiều. Nói cách khác, ưu tiên thu thập biến ngoại sinh tốt trước khi nghĩ tới fine-tune.

**Bước 4. Xem biến nào có ích.**

```python
print(predictor.feature_importance(test_data, relative_scores=True))
```

**Bước 5. Dự báo.**

```python
future_known = ...   # TimeSeriesDataFrame chứa gia_ban, khuyen_mai của 28 ngày tới cho mỗi chuỗi
forecast = predictor.predict(train_data, known_covariates=future_known)
print(forecast.head())   # cột mean và các phân vị 0.1 đến 0.9
```

Dùng các phân vị để ra quyết định: đặt hàng theo phân vị 0,8 nếu thiếu hàng tốn kém hơn tồn kho. Với nhiều GPU, tài liệu khuyên giới hạn còn một GPU bằng biến môi trường `CUDA_VISIBLE_DEVICES` trước khi fine-tune.

## Từng bước huấn luyện NHITS từ đầu

Lý do chọn: NHITS là mạng nơ-ron dự báo gọn (thường dưới vài triệu tham số), huấn luyện nhanh, chạy được trên GPU 4 GB hoặc CPU, giấy phép hoàn toàn thuộc về bạn. Hợp khi có nhiều chuỗi cùng loại.

**Bước 1. Cài đặt và chuẩn bị dữ liệu.** NeuralForecast yêu cầu ba cột tên cố định: `unique_id`, `ds`, `y`.

```bash
pip install neuralforecast statsforecast
```

```python
import pandas as pd

df = pd.read_csv("doanh_so.csv", parse_dates=["timestamp"])
df = df.rename(columns={"item_id": "unique_id", "timestamp": "ds", "target": "y"})
df = df[["unique_id", "ds", "y"]].sort_values(["unique_id", "ds"])
```

**Bước 2. Định nghĩa mô hình.**

```python
from neuralforecast import NeuralForecast
from neuralforecast.models import NHITS
from neuralforecast.losses.pytorch import MQLoss

H = 28
model = NHITS(
    h=H, input_size=4 * H,            # nhìn lại 112 ngày để dự báo 28 ngày
    max_steps=2000, learning_rate=1e-3, batch_size=64,
    scaler_type="robust",             # chuẩn hoá từng chuỗi, quan trọng khi các chuỗi khác thang đo
    loss=MQLoss(level=[80]),          # dự báo kèm khoảng tin cậy 80%
    early_stop_patience_steps=5, val_check_steps=100,
)
nf = NeuralForecast(models=[model], freq="D")
```

**Bước 3. Kiểm định chéo theo thời gian.**

```python
cv = nf.cross_validation(df, n_windows=3, step_size=H, val_size=H)
print(cv.head())
```

Ba cửa sổ trượt: mỗi lần huấn luyện trên quá khứ và dự báo 28 ngày kế tiếp. Tính MASE hoặc sai số tuyệt đối trung bình trên kết quả và so với Seasonal Naive từ statsforecast chạy trên cùng các cửa sổ.

**Bước 4. Huấn luyện bản cuối và dự báo.**

```python
nf.fit(df, val_size=H)
forecast = nf.predict()
nf.save("nhits-doanh-so", overwrite=True)
```

**Bước 5. Cải thiện.**

- Thêm biến ngoại sinh qua `futr_exog_list` (biết trước) và `hist_exog_list` (chỉ biết quá khứ).
- Thử `input_size` từ 2 đến 6 lần độ dài dự báo.
- Thử PatchTST hoặc TFT với cùng giao diện bằng cách thêm vào danh sách `models`.
- Ghép trung bình với LightGBM kèm đặc trưng trễ và Chronos-2 zero-shot. Ba mô hình khác bản chất ghép lại thường tốt hơn từng cái riêng lẻ.

## Lưu ý quan trọng

- **Luôn có mốc ngây thơ.** Nếu mô hình không thắng "tuần này bằng tuần trước", đừng triển khai nó.
- **Kiểm thử phải mô phỏng đúng cách dùng thật.** Nếu thực tế dự báo vào thứ Hai cho cả tuần sau, hãy kiểm thử đúng như vậy, với đúng những dữ liệu sẵn có vào thứ Hai.
- **Rò rỉ là nguyên nhân số một của kết quả đẹp giả tạo.** Nghi ngờ mọi con số quá tốt.
- **Giấy phép TabPFN.** Mã nguồn là Apache 2.0 nhưng trọng số từ bản 2.5 là phi thương mại, kể cả khi đầu ra chỉ dùng cho quyết định nội bộ có tính thương mại. Dùng trong doanh nghiệp cần giấy phép riêng, hoặc dùng TabPFNv2 trong giới hạn của nó, hoặc dùng cây tăng cường.
- **Phân bố dữ liệu thay đổi theo thời gian.** Mô hình bảng và dự báo xuống cấp dần. Theo dõi sai số trên dữ liệu mới và đặt lịch huấn luyện lại.
- **Sự kiện bất thường** (dịch bệnh, đổi giá lớn, mất dữ liệu) cần được đánh dấu hoặc loại khỏi dữ liệu huấn luyện.
- **Chuỗi thưa** (phần lớn là số 0, như phụ tùng thay thế) cần thước đo và mô hình riêng. Sai số phần trăm vô nghĩa khi giá trị thật bằng 0.
- **Dự báo là phân bố, không phải một con số.** Dùng phân vị để ra quyết định tồn kho, nhân lực, công suất.
- **Mô hình đơn giản dễ giải thích hơn.** Trong môi trường cần giải trình (tín dụng, bảo trì an toàn), một mô hình cây kèm SHAP thường được chấp nhận hơn một mô hình nền tảng.

## Tổng kết series

Sáu bài đã đi qua năm lĩnh vực với cùng một khuôn: liệt kê công cụ, xếp các cách làm từ dễ đến khó, rồi đi từng bước một đường fine-tune và một đường huấn luyện từ đầu. Vài điều lặp lại ở mọi lĩnh vực:

1. Thử cách không huấn luyện trước và ghi lại con số làm mốc.
2. Dữ liệu sạch và tập kiểm thử tách đúng quan trọng hơn mọi siêu tham số.
3. LoRA trên một mô hình mở cỡ vừa là điểm cân bằng tốt nhất giữa độ chính xác và VRAM, trừ dữ liệu bảng.
4. Huấn luyện từ đầu đáng làm để hiểu bản chất, và là lựa chọn thực dụng khi mô hình phải thật bé hoặc giấy phép phải thật sạch.
5. Đọc giấy phép của mô hình và dữ liệu trước khi đầu tư công sức.

Quay lại [bài 1](/2026/11/15/tu-huan-luyen-ai-nho-1-tong-quan/) để xem bảng tóm tắt và các liên kết.

## Nguồn tham khảo

- [AutoGluon: Forecasting with Chronos-2](https://auto.gluon.ai/dev/tutorials/timeseries/forecasting-chronos.html)
- [Chronos-2: From Univariate to Universal Forecasting](https://arxiv.org/pdf/2510.15821)
- [Prior Labs: danh sách mô hình TabPFN và giấy phép](https://docs.priorlabs.ai/models)
- [TabPFN-2.5 Model Report](https://priorlabs.ai/technical-reports/tabpfn-2-5-model-report)
- [TabPFN 3.5 Beats Boosted Trees: When to Use It on Your Data](https://www.digitalapplied.com/blog/tabpfn-3-5-tabular-foundation-model-when-to-use)
- [TabPFN trên GitHub](https://github.com/PriorLabs/tabpfn)
