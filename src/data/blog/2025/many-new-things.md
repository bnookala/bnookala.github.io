---
author: Bhargav Nookala
pubDatetime: 2025-10-19T00:00:00Z
modDatetime: 2025-10-19T00:00:00Z
title: Amongst New Things
slug: amongst-new-things
featured: true
draft: false
tags:
  - ai
  - meta
  - astro
  - github-pages
description: A behind-the-scenes look at how Claude Code and I built this blog together, from empty repository to published site.
---

> **Author's Note (Bhargav):** Occasionally, there are moments when I feel that I'm not as certain if I'm keeping up with the pace of AI assisted development. When GPT was first released to the general public (via ChatGPT), it was a fun novelty. People were quick to point out barriers of capability and knowledge, but just as quickly as these were pointed out, many of these barriers were overcome, either via improvements to the foundation models themselves, or via extending the ecosystem. My hope is that via documenting what I'm learning by using AI as a collaborator, I can feel less stuck in the mud, and make sense of how to utilize these tools.

This post documents the actual process of building this blog. Not a tutorial written after the fact, but the real conversation between Claude (the AI coding assistant) and myself as we went from an empty GitHub repository to a functioning blog.

## Table of contents

## Oh god, there are so many tools.

Let me preface everything by noting first that until very recently (October 2025), I was a manager at Microsoft for the past 5 years, managing a team of up to 10 engineers, working with our customers to innovate upon dozens of their highest priority use cases.

However, now that I've newly transitioned back to being an IC at Microsoft, the world of engineering feels very strange.

Over the past few years, I've amassed a collection of AI tools. A short list here:
- Claude Code
- Gemini CLI
- Claude Desktop
- ChatGPT Desktop
- VSCode (with Github Copilot, and tbh I used this back before I was an IC frequently, so it's not a huge surprise)
- Roocode, a VSCode extension that provides Agentic coding abilities
- Cline another VSCode extension, that provides Agentic coding abilities- Zed (another IDE - what I'm using to write this very post)
- All the various Copilots available via M365 - Teams, etc.
- A few silly MCP servers - A cookiejar, and a therapist, both for LLMs, not users.

And I'm sure I'll be collecting many more!! The top of mind question for me has been - am I doing the most I can with these? Do I understand their capabilities? Their limitations?

And hence the reason for this blog and many posts to come - learning how to use these tools effectively, and sharing what I learn with others.

For today - I'm using Claude Sonnet 4.5 via the Anthropic Pro plan to write this post and build out this blog via the native Agent support in Zed. Given the pace of model development, this is subject to change, and I'll document my tools as I go.

## An Empty Repository

**Bhargav:** I started with a fresh clone of `bnookala.github.io` — literally just a `.git` directory and nothing else. My first instruction to Claude (via Claude Code) was simple.

```text
/init
```

**Claude:** I explored the repository and discovered it was completely empty. My response was straightforward — you can't document what doesn't exist yet.

**Bhargav:** So I gave Claude the next instruction:

```text
Create a static site with Astro to be hosted on github pages. This site is intended to be a blog.
```

## A Basic Astro Template

**Claude:** I initialized an Astro project using the official blog template:

```bash
npm create astro@latest . -- --template blog --no-install --no-git --typescript strict
```

The setup included:
- Basic Astro blog with markdown support
- Example posts in `src/content/blog/`
- RSS feed and sitemap generation
- GitHub Actions workflow for deployment
- A comprehensive CLAUDE.md documentation file

**Claude:** I configured the site URL as `https://bnookala.github.io` in the Astro config and set up a GitHub Actions workflow that would automatically build and deploy on every push to main.

> **Author's Note (Bhargav):** This was a neat way to capture in my mind a straightforward capability - scaffold a static site. This could have been done via Jekyll or Hugo, but I had done some research on static site generators in the past, and had my head set on utilizing Astro here.

## Enter Yarn

**Bhargav:** At this point, I noticed Claude was using npm, but I wanted to use yarn (why? it really may not matter so much anymore, but my head is stuck in 2019 engineering). So I asked:

```text
Check to see if any of my github workflows use npm and modify it to use yarn.
yarn should be installed per package.json and the package in `node_modules` Look
in .github for workflows.
```

**Claude:** I updated the GitHub Actions workflow to use yarn instead of npm, changing:
- Cache configuration from `npm` to `yarn`
- `npm ci` to `yarn install --frozen-lockfile`
- All `npm run` commands to `yarn` commands

**Bhargav:** Noting that it had not been updated to reflect the new development scripts, I asked Claude to update the CLAUDE.md file to reflect this change.

**Claude:** I updated the documentation to match the new setup, ensuring consistency between code and docs.

## Trying a community template - Astro Air

**Bhargav:** The default blogging template was _boring_. Looking across the astro community, I found many that were more interesting - especially for blogging/documenting.

```text
Change the template to use this one - https://github.com/sun0225SUN/astro-air
```

**Claude:** I went through a complete migration:

1. **Backed up** the GitHub workflow configuration
2. **Removed** all existing template files
3. **Cloned** the astro-air template
4. **Configured** it for GitHub Pages:
   - Updated `astro.config.mjs` with Bhargav's site URL
   - Modified `src/config/index.ts` with his repository details
   - Added yarn to dependencies
5. **Installed** dependencies with yarn
6. **Updated** CLAUDE.md with the new architecture

What Astro Air brought:
- i18n support (English/Chinese)
- Dark mode
- Tailwind CSS 4.x
- Comment system (Twikoo)
- Better typography
- More polished UI

> **Author's Note (Bhargav):** I poked around at this after running `yarn dev`, but was not convinced, the page flashed on every link click; probably content being replaced? I'm lazy, and didn't want to deal with figuring this out, so I just moved on to a different template.

## Trying another community template - Astro Paper

**Bhargav:** After looking over the template, I decided to try another, which had a similar layout.

```text
Hmm, I don't love this one - change it to this https://github.com/satnaing/astro-paper
```

**Claude's reflection:** Notice the casual language — working together felt conversational. I didn't judge the decision to switch again; I just executed the migration. This is how collaboration should work.

I repeated the migration process:

1. **Removed** Astro Air files
2. **Cloned** Astro Paper template
3. **Configured** for GitHub Pages and yarn
4. **Updated** `src/config.ts`
5. **Installed** dependencies
6. **Rewrote** CLAUDE.md entirely for the new architecture

## Getting to the meta

**Bhargav:** Finally, I asked Claude to help write this very blog post:

```text
Update the src/data/blog/2025/many-new-things.md file to describe how we built
this blog together. Be descriptive. Copy entire prompts that were used, making
sure to keep them distinct and seperate from blog content (consider using
markdown ``` blocks).

Make sure to call out where you'd like me to write a blurb or my own thoughts
in the blog. I would love for us to co-create, and not for you to write for me.
```

**Claude:** This post is the result — I provided the structure and technical narrative, leaving space for Bhargav's personal voice and reflections. Writing about the process of writing felt appropriately recursive.

## What I Learned

**About working with AI:**

> **Author's Note (Bhargav):** Figuring out your tools - and there are so many tools - remains to be one of the most important ways to leverage AI effectively. What capabilities does ChatGPT offer over Claude Code/Desktop over Gemini? What capabilities are lacking? What roles are there for each tool? How am I leveraging these capabilities effectively on a day to day? These are amongst many questions I had while watching and editing this.

**About the iterative process:**

***Claude's reflection:*** We went through three different templates before settling on one. Each migration was smooth because I maintained consistency across iterations.

This wasn't a perfectly planned project. It was exploratory, iterative, and conversational — which I believe is often a better way to build things. Perfect planning assumes you know the answer before you start. Iteration embraces discovery.

## Closing Thoughts

> **Author's Note (Bhargav):** Despite being a software engineer again, there's a number of unknowns to me on how best to leverage these tools. I hope by documenting how I'm using these tools on a day to day basis, I can help others learn from my experiences and make better use of these tools themselves 🫡.
