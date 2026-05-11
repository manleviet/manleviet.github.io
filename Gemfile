source "https://rubygems.org"

# GitHub Pages gem — bundles Jekyll + plugins ở đúng version mà GitHub Pages dùng
gem "github-pages", group: :jekyll_plugins

# Plugins cần thiết
group :jekyll_plugins do
  gem "jekyll-remote-theme"
  gem "jekyll-seo-tag"
end

# Cần thiết trên macOS / Windows
gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]
gem "wdm", "~> 0.1.1", platforms: [:mingw, :mswin, :x64_mingw]

# Webrick không còn được bundle sẵn từ Ruby 3.0
gem "webrick", "~> 1.8"
