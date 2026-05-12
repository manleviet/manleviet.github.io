source "https://rubygems.org"

# Plain Jekyll + jekyll-scholar (jekyll-scholar is NOT on the GitHub Pages
# plugin whitelist, so we build via GitHub Actions instead of the GH Pages
# native builder — see .github/workflows/jekyll.yml).
gem "jekyll", "~> 4.3"

group :jekyll_plugins do
  gem "jekyll-seo-tag"
  gem "jekyll-scholar"           # BibTeX-driven publication lists.
                                 # IMPORTANT: do NOT wrap --query values in
                                 # double quotes inside {% bibliography %}
                                 # Liquid tags. jekyll-scholar's option
                                 # parser splits on option boundaries, not
                                 # shell-words — quotes become part of the
                                 # query string and cause bib[query] -> nil.
                                 # Correct:   --query @*[featured=true]
                                 # Broken:    --query "@*[featured=true]"
end

# Required on macOS / Windows
gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]
gem "wdm", "~> 0.1.1", platforms: [:mingw, :mswin, :x64_mingw]

# Webrick is no longer bundled in Ruby 3.0+
gem "webrick", "~> 1.8"
