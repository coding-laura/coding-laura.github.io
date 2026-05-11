# frozen_string_literal: true

source "https://rubygems.org"

# github-pages 223 pins Liquid 4.0.3 (uses String#tainted?, removed in Ruby 3.2+).
# 232+ ships Jekyll 3.10 and Liquid 4.0.4. The Pages stack (commonmarker) is not Ruby 4–ready yet—use Ruby 3.3 locally and in CI.
ruby "~> 3.3.0"

# Silence Liquid’s Ruby 3.4+ warning about bigdecimal leaving default gems.
gem "bigdecimal"

gem "github-pages", "~> 232", group: :jekyll_plugins
gem "jekyll-gfm-admonitions", group: :jekyll_plugins
