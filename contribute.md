---
layout: default
title: "How to Contribute"
permalink: /contribute/
---

# How to Contribute a Post

CS Perspectives welcomes contributions from all faculty in the Department of Computer Science. We publish short, accessible pieces on topics in computing—essays, reflections on teaching, technical explainers, opinion pieces, anything a curious colleague or student might find worth reading.

## What Makes a Good Post?

There is no rigid formula. Past posts have covered AI pedagogy, computability theory, and the gap between what ML models do and what we think they do. A post can be 500 words or 2,000. It can be technical or reflective, serious or playful. The main criterion: does it say something interesting about computer science, teaching, or both?

## Option 1: Use the Post Composer (Easiest)

We have an **online post composer** that lets you write your article with a live preview and generates the correctly formatted file when you are done. You do not need to know Markdown, Git, or Jekyll.

1. Open the [Post Composer]({{ '/compose/' | relative_url }}).
2. Fill in your name, title, and optional subtitle.
3. Write or paste your content in the editor. The preview updates as you type.
4. Click **Copy Markdown** to get the formatted post.
5. Email it to [Kevin Lundeen](mailto:lundeenk@seattleu.edu)—he will review and publish.

## Option 2: Write the Markdown Directly

If you are comfortable with Markdown, you can create the post file yourself. Name it with this pattern:

```
YYYY-MM-DD-your-title-in-lowercase.md
```

For example: `2026-04-15-why-i-stopped-using-autograders.md`

Start the file with this front matter block:

```yaml
---
layout: post
title: "Your Post Title"
subtitle: "An optional subtitle"
date: 2026-04-15
author: Your Name
author_title: "Associate Professor, Department of Computer Science"
---

Your content in Markdown goes here.
```

Standard Markdown formatting is supported: `**bold**`, `*italic*`, `[links](url)`, headings with `##`, code blocks with triple backticks, and so on.

Then either:

- Email the `.md` file to [Kevin](mailto:lundeenk@seattleu.edu), or
- Open a pull request against [klundeen/su-cs-blog](https://github.com/klundeen/su-cs-blog) on GitHub, adding your file to the `_posts/` directory.

## Option 3: Just Send a Draft

If you would rather not think about formatting at all, write your piece in whatever tool you like—Word, Google Docs, plain text, even an email—and send it to [Kevin](mailto:lundeenk@seattleu.edu). Include the title, any subtitle, and how you would like your byline to read. He will handle the rest.

## Images

If your post includes images, send them along with the draft. Use descriptive filenames (e.g., `neural-net-architecture.png` rather than `screenshot3.png`). For Markdown authors, reference images like this:

```markdown
![Description of the image](/su-cs-blog/assets/images/your-image.png)
```

## Review Process

There is no formal review board. Kevin will read your draft for formatting issues and basic clarity, but the goal is to publish your voice, not to edit it into something else. Expect a turnaround of a few days at most. If there are questions, he will follow up directly.

## Questions?

Email [lundeenk@seattleu.edu](mailto:lundeenk@seattleu.edu) or stop by Kevin's office.
