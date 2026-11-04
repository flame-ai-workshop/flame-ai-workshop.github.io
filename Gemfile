# frozen_string_literal: true

source "https://rubygems.org"

# Mirror the GitHub Pages production build. This repo uses the legacy
# "deploy from branch" build, which runs the github-pages gem
# (Jekyll 3.10.0 + whitelisted plugins). Local == production avoids
# "works locally, breaks on Pages" surprises.
#
# Pinned to 232 (same Jekyll 3.10.0 as 233): 233 pulls jekyll-remote-theme
# 0.6.x -> openssl gem 4.x, which segfaults on macOS Homebrew Ruby 3.2 when
# jekyll-github-metadata calls the GitHub API. 232 uses Ruby's bundled openssl.
gem "github-pages", "232", group: :jekyll_plugins

# Ruby >= 3.0 no longer bundles webrick, which `jekyll serve` needs.
gem "webrick", "~> 1.8"
