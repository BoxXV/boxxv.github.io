source "https://rubygems.org"

# github-pages gem pins Jekyll and every allowed plugin to the same versions
# GitHub Pages uses, so no need to fetch pages.github.com/versions.json anymore.
gem "github-pages", group: :jekyll_plugins

# Needed to run `jekyll serve` on Ruby 3+
gem "webrick"

# Windows and JRuby do not include zoneinfo files
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end
