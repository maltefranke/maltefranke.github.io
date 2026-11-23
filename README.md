# maltefranke.github.io

Source for my personal website, [maltefranke.github.io](https://maltefranke.github.io), built with Jekyll and the [al-folio](https://github.com/alshedivat/al-folio) theme.

- `_pages/` – site pages (about, research, publications, news)
- `_news/` – news items shown on the front page
- `_bibliography/papers.bib` – publications
- `assets/` – images, GIFs and the interactive Morph viewer

Pushing to `main` builds and deploys the site via `.github/workflows/deploy.yml`.

To preview locally (needs Homebrew Ruby: `brew install ruby imagemagick`):

```sh
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve   # then open http://localhost:4000
```
