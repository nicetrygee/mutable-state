---
title: "Setting Up a Hugo Blog from Scratch"
date: 2026-07-11T14:45:20+10:00
draft: false
---

## Why I Chose Hugo

I've built websites using WordPress, static HTML, React, and a handful of other frameworks over the years. For a personal engineering blog, I wanted something much simpler. I didn't want to manage a server or worry about databases. I wanted to write Markdown, push to GitHub, and have a website miraculously appear. Enter Hugo.

At a high level, the architecture looks like this:

```text
Markdown files
        │
        ▼
     Hugo
        │
        ▼
 Static HTML
        │
        ▼
 GitHub Actions
        │
        ▼
 GitHub Pages
```

Everything lives in Git, every deployment is automated, and there's hardly anything to maintain.

---

## Step 1 – Install Hugo

```bash
brew install hugo
```

Check it's working.

```bash
hugo version
```

You should see something like this:

```text
hugo v0.151.1
```

---

## Step 2 – Create Somewhere for Your Projects

Navigate to where you want to save your blog:

```bash
cd ~/Projects
```

---

## Step 3 – Create the Hugo Site

Ask Hugo to scaffold an empty site.

```bash
hugo new site engineering-blog
```

Move into the new dir:

```bash
cd engineering-blog
```

If you open the folder in VS Code, you'll notice it contains folders:

```text
content/
layouts/
static/
assets/
themes/
```

These are placeholders. At this point Hugo has created the plumbing, but there's no design and no content yet.

---

## Step 4 – Put It Under Git

One of the reasons I like Hugo is that everything is code. Before doing anything else, initialise Git.

```bash
git init
```

Create the first commit.

```bash
git add .
git commit -m "Initial Hugo site"
```

Now every change you make is tracked and can be rolled back if needed.

---

## Step 5 – Create a Repo on GitHub

Go to GitHub and create a new repo for your blog.

Don't add:

- README
- Licence
- `.gitignore`

We'll push everything from our local copy instead.

---

## Step 6 – Connect GitHub

Copy the repository URL. Then back in the terminal:

```bash
git remote add origin https://github.com/<username>/engineering-blog.git
```

Push it.

```bash
git branch -M main
git push -u origin main
```

---

## Step 7 – Install a Theme

Without a theme Hugo doesn't have anything to render. For a basic theme, maybe install PaperMod:

```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
```

Tell Hugo to use it.

Open:

```text
hugo.toml
```

Add:

```toml
theme = "PaperMod"
```

---

## Step 8 – Start the Dev Server

Run:

```bash
hugo server
```

Open:

```text
http://localhost:1313
```

Whenever you save a file, the browser automatically refreshes. No restart needed.

---

## Step 9 – Write Your First Post

Create a new post:

```bash
hugo new posts/my-first-post.md
```

Hugo creates the file with some useful metadata included. Open it and change:

```yaml
draft: true
```

to:

```yaml
draft: false
```

Otherwise it won't appear on your website. 

---

## Step 10 – Add an Image?

Create a folder:

```text
static/images
```

Drop an image inside and reference it like this:

```md
![Architecture](/images/architecture.png)
```

---

## Step 11 – Commit Your Changes

Once you're happy:

```bash
git add .
git commit -m "Add first blog post"
```

Exactly the same workflow you'd use for any software project.

---

## Step 12 – Deploy Automatically

No need to manually update files. Instead, add a GitHub Actions workflow. Whenever I push to `main`, GitHub:

- Checks out the repository
- Installs Hugo
- Builds the site
- Deploys it to GitHub Pages

After that, publishing is simply:

```bash
git push
```

Within a second, the live blog updates itself.