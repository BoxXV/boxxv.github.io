---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: Hướng dẫn phát triển dự án AI từng bước để học vào năm 2025
subtitle: AI Project Development Step By Step to learn in 2025
date: 2025-01-20 11:00:00
tags:
- AI
- 2025
- Develop
---

- [🚀 AI Project Roadmap](#-ai-project-roadmap)
- [📌 Giai đoạn 1: Xác định vấn đề và thiết kế hệ thống](#-giai-đoạn-1-xác-định-vấn-đề-và-thiết-kế-hệ-thống)
- [📌 Giai đoạn 2: Thu thập và lưu trữ dữ liệu](#-giai-đoạn-2-thu-thập-và-lưu-trữ-dữ-liệu)
- [📌 Giai đoạn 3: Tiền xử lý dữ liệu](#-giai-đoạn-3-tiền-xử-lý-dữ-liệu)
- [📌 Giai đoạn 4: Đào tạo mô hình \& tinh chỉnh (Tùy chọn)](#-giai-đoạn-4-đào-tạo-mô-hình--tinh-chỉnh-tùy-chọn)
- [📌 Giai đoạn 5: Triển khai hệ thống truy xuất](#-giai-đoạn-5-triển-khai-hệ-thống-truy-xuất)
- [📌 Giai đoạn 6: Phát triển API (NestJS)](#-giai-đoạn-6-phát-triển-api-nestjs)
- [📌 Giai đoạn 7: Tích hợp giao diện (Next.js)](#-giai-đoạn-7-tích-hợp-giao-diện-nextjs)
- [📌 Giai đoạn 8: Triển khai](#-giai-đoạn-8-triển-khai)
- [🔥 Các bước để cải thiện hệ thống AI của bạn](#-các-bước-để-cải-thiện-hệ-thống-ai-của-bạn)
  - [**Bước 1: Thu thập phản hồi của người dùng**](#bước-1-thu-thập-phản-hồi-của-người-dùng)
  - [**Bước 2: Lưu trữ phản hồi trong MongoDB**](#bước-2-lưu-trữ-phản-hồi-trong-mongodb)
  - [**Bước 3: Phân tích phản hồi AI không chính xác**](#bước-3-phân-tích-phản-hồi-ai-không-chính-xác)
  - [**Bước 4: Tinh chỉnh hệ thống**](#bước-4-tinh-chỉnh-hệ-thống)
  - [**Bước 5: Giám sát liên tục và cải tiến tự động**](#bước-5-giám-sát-liên-tục-và-cải-tiến-tự-động)


Sau đây là lộ trình chi tiết để xây dựng Ứng dụng AI tạo sinh bằng Next.js, NestJS, OpenAI và MongoDB Vector Search. Hướng dẫn này bao gồm mọi thứ từ nhúng tài liệu công ty, lưu trữ vectơ, truy xuất dữ liệu và sử dụng kỹ thuật nhắc nhở để phản hồi AI thông minh.

## 🚀 AI Project Roadmap

Hướng dẫn có cấu trúc toàn diện về cách xây dựng ứng dụng AI tạo sinh sẵn sàng đưa vào sản xuất.


-----
## 📌 Giai đoạn 1: Xác định vấn đề và thiết kế hệ thống

🎯 Mục tiêu:

- Xác định phát biểu vấn đề (ví dụ: tìm kiếm tài liệu hỗ trợ AI, chatbot, tóm tắt).
- Chọn nhiệm vụ AI (ví dụ: tạo văn bản, trả lời câu hỏi, tóm tắt).
- Xác định thông tin đầu vào của người dùng (ví dụ: truy vấn văn bản, tải tài liệu lên).
- Xác định định dạng đầu ra (ví dụ: văn bản thuần túy, phản hồi có cấu trúc).
- Xác định phương pháp truy xuất (ví dụ: MongoDB Vector Search, RAG).

🛠 Công nghệ cần học:

- Kiến thức cơ bản về AI : AI tạo sinh, RAG (Thế hệ tăng cường truy xuất).
- Tìm kiếm vectơ : Tìm kiếm vectơ trong MongoDB Atlas.
- Next.js & NestJS : Phát triển toàn diện.


-----
## 📌 Giai đoạn 2: Thu thập và lưu trữ dữ liệu

🎯 Mục tiêu:

- Thu thập tài liệu của công ty (ví dụ: PDF, Word, CSV, JSON).
- Lưu trữ tài liệu hiệu quả trong MongoDB.
- Tạo và lưu trữ nhúng vector.

🔥 Các bước thực hiện :
1. Thiết lập MongoDB Atlas:
   - Tạo cơ sở dữ liệu cho tài liệu và nội dung nhúng.
   - Bật Tìm kiếm Vector.
2. Cài đặt phụ thuộc:

```bash
npm install openai mongoose @nestjs/mongoose
```

3. Lưu trữ tài liệu trong MongoDB:

```javascript
const documentSchema = new mongoose.Schema({
	content: String,
	embedding: { type: Array, default: [] },
});
```

4. Chuyển đổi tài liệu thành nội dung nhúng:

```javascript
import OpenAI from 'openai';

const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });

async function generateEmbedding(text: string) {
	const response = await openai.embeddings.create({
		input: text,
		model: 'text-embedding-ada-002',
	});

	return response.data[0].embedding;
}
```

5. Lưu trữ Vector trong MongoDB:

```javascript
async function storeDocument(content: string) {
	const embedding = await generateEmbedding(content);
	await DocumentModel.create({ content, embedding });
}
```

🛠 Công nghệ cần học:

- Tìm kiếm vectơ trong MongoDB Atlas.
- API nhúng OpenAI.
- NestJS với MongoDB.


-----
## 📌 Giai đoạn 3: Tiền xử lý dữ liệu

🎯 Mục tiêu:

- Làm sạch và xử lý dữ liệu phi cấu trúc.
- Triển khai phân đoạn tài liệu để nhúng tốt hơn.
- Lưu trữ siêu dữ liệu có cấu trúc để truy xuất.

🔥 Các bước thực hiện:

1. Xóa các phần không cần thiết:

```javascript
function cleanText(text: string): string {
	return text.replace(/(Disclaimer|Footer|Further Support).*/g, '');
}
```

2. Chia nhỏ các tài liệu lớn:

```javascript
function chunkText(text: string, chunkSize = 500) {
	return text.match(new RegExp(`.{1,${chunkSize}}`, 'g'));
}
```

🛠 Công nghệ cần học:

- Tiền xử lý văn bản (Regex, Phân đoạn, Xóa từ dừng).
- LangChain để tách văn bản.


-----
## 📌 Giai đoạn 4: Đào tạo mô hình & tinh chỉnh (Tùy chọn)

🎯 Mục tiêu:

- Đào tạo mô hình OpenAI tùy chỉnh nếu cần.
- Tinh chỉnh các phản hồi cho các thuật ngữ cụ thể của ngành.

🔥 Các bước thực hiện :

1. Chuẩn bị dữ liệu đào tạo (Định dạng JSON):

```json
 {"messages": [{"role": "system", "content": "You are a financial assistant."}, {"role": "user", "content": "What is an ETF?"}, {"role": "assistant", "content": "An ETF is an exchange-traded fund."}]}
```

2. Tải lên và đào tạo trong OpenAI:

```bash
openai api fine_tunes.create -t dataset.jsonl -m gpt-4
```

🛠 Công nghệ cần học:

- Tinh chỉnh các mô hình OpenAI.
- Kỹ thuật nhanh chóng để có phản hồi tốt hơn.


-----
## 📌 Giai đoạn 5: Triển khai hệ thống truy xuất

🎯 Mục tiêu:

- Triển khai tìm kiếm vector để tìm dữ liệu có liên quan nhanh chóng.
- Sử dụng MongoDB Vector Search để tìm kiếm tài liệu phù hợp nhất.

🔥 Các bước thực hiện:

1. Thực hiện truy vấn tìm kiếm Vector:

```javascript
async function searchDocuments(query: string) {
	const queryEmbedding = await generateEmbedding(query);

	return await DocumentModel.find({
		$vectorSearch: {
			queryVector: queryEmbedding,
			path: 'embedding',
			numCandidates: 10,
			limit: 5,
		},
	});
}
```

2. Lấy dữ liệu và gửi đến OpenAI để phản hồi:

```javascript
async function generateAIResponse(query: string) {
	const relevantDocs = await searchDocuments(query);

	const response = await openai.chat.completions.create({
		model: 'gpt-4',
		messages: [
			{ role: 'system', content: 'Use the following documents to answer the user query:' },
			...relevantDocs.map(doc => ({ role: 'user', content: doc.content })),
			{ role: 'user', content: query },
		],
	});

	return response.choices[0].message.content;
}
```

🛠 Công nghệ cần học:

- Truy vấn tìm kiếm vectơ MongoDB.
- Thế hệ tăng cường truy xuất (RAG).


-----
## 📌 Giai đoạn 6: Phát triển API (NestJS)

🎯 Mục tiêu:

- Xây dựng REST API để xử lý các truy vấn AI.
- Hiển thị các điểm cuối để truy vấn các phản hồi do AI tạo ra.

🔥 Các bước thực hiện :
1. Tạo dịch vụ AI :

```javascript
@Injectable()
export class AIService {
	async processQuery(query: string) {
		return await generateAIResponse(query);
	}
}
```

2. Tạo bộ điều khiển:


```javascript
@Controller('ai')
export class AIController {
	constructor(private readonly aiService: AIService) {}

	@Post('query')
	async handleQuery(@Body() data: { query: string }) {
		return this.aiService.processQuery(data.query);
	}
}
```

🛠 Công nghệ cần học:

- Bộ điều khiển và dịch vụ NestJS.
- Thực hành tốt nhất về phát triển API.


-----
## 📌 Giai đoạn 7: Tích hợp giao diện (Next.js)

🎯 Mục tiêu:

- Tạo giao diện người dùng Next.js để tương tác với AI.
- Gửi truy vấn đến phần phụ trợ và hiển thị kết quả.

🔥 Các bước thực hiện:

1. Cuộc gọi API từ Next.js:

```javascript
async function fetchAIResponse(query: string) {
	const res = await fetch('/api/ai-query', {
		method: 'POST',
		body: JSON.stringify({ query }),
	});
	return res.json();
}
```

2. Tạo thành phần UI:

```javascript
export default function AIChat() {
	const [query, setQuery] = useState('');
	const [response, setResponse] = useState('');

	async function handleSubmit() {
		const data = await fetchAIResponse(query);
		setResponse(data);
	}

	return (
		<div>
			<input type="text" value={query} onChange={e => setQuery(e.target.value)} />
			<button onClick={handleSubmit}>Ask AI</button>
			<p>{response}</p>
		</div>
	);
}
```

🛠 Công nghệ cần học:

- Tuyến API Next.js.
- React Hooks và Quản lý trạng thái.


-----
## 📌 Giai đoạn 8: Triển khai

- Triển khai Next.js trên Vercel.
- Triển khai NestJS trên AWS/GCP.
- Sử dụng MongoDB Atlas để lưu trữ.


-----
📌 Phản hồi và Lặp lại của Người dùng (Giai đoạn Cuối cùng)

Giai đoạn Phản hồi & Lặp lại của Người dùng rất cần thiết để cải thiện ứng dụng chạy bằng AI của bạn dựa trên cách sử dụng thực tế. Nó đảm bảo hệ thống của bạn vẫn chính xác, thân thiện với người dùng và hiệu quả theo thời gian.

-----
🎯 Mục tiêu:

- Thu thập phản hồi của người dùng về phản hồi của AI.
- Phân tích các câu trả lời không chính xác của AI và cải thiện độ chính xác.
- Tối ưu hóa việc xử lý truy vấn, truy xuất và phản hồi mô hình.
- Thực hiện cải tiến liên tục bằng cách sử dụng vòng phản hồi.

-----
## 🔥 Các bước để cải thiện hệ thống AI của bạn

### **Bước 1: Thu thập phản hồi của người dùng**

Khuyến khích người dùng đánh giá phản hồi của AI hoặc báo cáo những thông tin không chính xác.

✅ Triển khai giao diện người dùng (Next.js UI)

- Thêm nút phản hồi vào phản hồi của AI.
- Thu thập đánh giá của người dùng (ví dụ: 👍/👎, 1-5 sao).

📌 Ví dụ (Giao diện phản hồi Next.js):

```javascript
export default function AIResponse({ response }) {
	const [feedback, setFeedback] = useState(null);

	async function sendFeedback(value) {
		await fetch('/api/feedback', {
			method: 'POST',
			body: JSON.stringify({ response, feedback: value }),
		});
		setFeedback(value);
	}

	return (
		<div>
			<p>{response}</p>
			<button onClick={() => sendFeedback('👍')}>👍</button>
			<button onClick={() => sendFeedback('👎')}>👎</button>
		</div>
	);
}
```

### **Bước 2: Lưu trữ phản hồi trong MongoDB**

Tạo bộ sưu tập phản hồi trong MongoDB.

📌 NestJS API để lưu trữ phản hồi:

```javascript
@Controller('feedback')
export class FeedbackController {
	@Post()
	async saveFeedback(@Body() data: { response: string; feedback: string }) {
		await FeedbackModel.create(data);
	}
}
```

### **Bước 3: Phân tích phản hồi AI không chính xác**

Thường xuyên xem xét phản hồi tiêu cực và phân loại lỗi:

✅ Các loại lỗi :

1. Sự thật không chính xác → Cải thiện mô hình truy xuất.
2. Kết quả không liên quan → Tăng cường nhúng vector.
3. Câu trả lời không rõ ràng → Tối ưu hóa kỹ thuật nhắc nhở.

📌 Truy vấn dữ liệu hiệu suất AI trong MongoDB:

```javascript
async function getNegativeFeedback() {
	return await FeedbackModel.find({ feedback: '👎' }).limit(100);
}
```

### **Bước 4: Tinh chỉnh hệ thống**

Dựa trên phân tích, cải thiện hệ thống bằng cách sử dụng:

1. Kỹ thuật nhanh chóng hơn

Ví dụ: Thêm ngữ cảnh vào lời nhắc của AI.

```javascript
const prompt = `
	You are an AI assistant for a legal firm.
	Use the following company documents to answer accurately:
	${retrievedDocuments}
`;
```

2. Cải thiện việc phân chia tài liệu

Nếu kết quả truy xuất không chính xác, hãy điều chỉnh kích thước khối.

```javascript
function chunkText(text: string, chunkSize = 300) {
	return text.match(new RegExp(`.{1,${chunkSize}}`, 'g'));
}
```

3. Đào tạo lại hoặc tinh chỉnh mô hình

- Nếu phản hồi của OpenAI có chất lượng thấp, hãy đào tạo một mô hình được tinh chỉnh tùy chỉnh.

### **Bước 5: Giám sát liên tục và cải tiến tự động**

1. Theo dõi hiệu suất AI bằng cách ghi nhật ký (ví dụ: ghi lại các câu trả lời không chính xác).
2. Sử dụng số liệu (ví dụ: theo dõi tần suất người dùng thích 👍 so với 👎).
3. Yêu cầu kiểm tra A/B (ví dụ: so sánh các định dạng yêu cầu AI khác nhau).
4. Lên lịch cập nhật mô hình (ví dụ: đào tạo lại nhúng hàng tháng).

📌 Ghi lại hiệu suất AI trong NestJS :

```javascript
async function logAIResponse(query: string, response: string) {
	await PerformanceModel.create({ query, response, timestamp: new Date() });
}
```


-----
Tham khảo:
- [AI Project Development Step By Step to learn in 2025)](https://dev.to/tak089/ai-project-development-step-by-step-to-learn-in-2025-1m0d)
- [25 Generative AI projects Ideas](https://dev.to/tak089/25-generative-ai-projects-ideas-3ahj)
- []()