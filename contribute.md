---
layout: page
title: How to Contribute a Post
subtitle: Fork, write, PR. You know the drill.
permalink: /contribute/
---

The repo is [klundeen/su-cs-blog](https://github.com/klundeen/su-cs-blog) on GitHub. It is a standard Jekyll site hosted on GitHub Pages.

## Write a Post

Create a Markdown file in `_posts/` named with this pattern:

```
YYYY-MM-DD-your-title-in-lowercase.md
```

Start the file with front matter:

```yaml
---
layout: post
title: "Your Post Title"
subtitle: "An optional subtitle or framing question"
date: 2026-04-15
author: Your Name
author_title: "Associate Professor, Department of Computer Science"
---

Your content in Markdown goes here.
```

The site uses kramdown with GFM. Everything you would expect works: `**bold**`, `*italic*`, `[links](url)`, `##` headings, fenced code blocks, footnotes, block quotes, tables.

For images, add them to `assets/images/` and reference them as:

```markdown
![Alt text]({{ '/assets/images/your-image.png' | relative_url }})
```

## Submit a PR

1. Fork [klundeen/su-cs-blog](https://github.com/klundeen/su-cs-blog).
2. Add your post to `_posts/`.
3. To preview locally: `bundle install && bundle exec jekyll serve`.
4. Open a PR against `main`.

That is it. Kevin will merge promptly.

## Use the Post Composer

If you would rather skip the Git workflow, the [Post Composer]({{ '/compose/' | relative_url }}) lets you write with a live preview and generates the correctly formatted Markdown file. Copy the output, email it to [Kevin](mailto:lundeenk@seattleu.edu), and he will commit it for you.

## What to Write About

Anything at the intersection of computer science, teaching, and ideas. See the [Roadmap]({{ '/roadmap/' | relative_url }}) for series we are building out. A post can be 500 words or 2,000. The bar is simple: *would this be interesting to a smart person who is not necessarily in your subfield?*

## Questions?

Open an [issue](https://github.com/klundeen/su-cs-blog/issues), or email [lundeenk@seattleu.edu](mailto:lundeenk@seattleu.edu).
