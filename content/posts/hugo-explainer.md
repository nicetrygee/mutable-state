---
title: "Setting Up a Hugo Blog from Scratch"
date: 2026-07-11T14:45:20+10:00
draft: false
---

# Why I Chose Hugo

I've built websites using WordPress, static HTML, React, and a handful of other frameworks over the years. For a personal engineering blog, I wanted something much simpler. For example, I didn't want to manage a server or worry about databases. I wanted to write Markdown, push to GitHub, and have a website miraculously appear. Enter Hugo.

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

Everything lives in Git, every deployment is automated, and there's virtually nothing to maintain.

---

# Step 1 – Install Hugo

Installing Hugo takes about 30 seconds.

```bash
brew install hugo
```

Once it's finished, check it's working.

```bash
hugo version
```

You should see something similar to:

```text
hugo v0.151.1
```

At this point Hugo is just another command on your machine. Nothing has been created yet.

---

# Step 2 – Go to Where Your Projects Live Locally

Say you keep them all inside a `Projects` dir.

```bash
cd ~/Projects
```

---

# Step 3 – Create the Site

Now we ask Hugo to scaffold an empty site.

```bash
hugo new site engineering-blog
```

Go into it.

```bash
cd engineering-blog
```

If you open the folder in VS Code you'll notice it isn't actually a website yet.

It contains folders with names like:

```
content/
layouts/
static/
assets/
themes/
```

Think of these as placeholders.

At the moment Hugo has created the plumbing, but there's no design and no content.

---

# Step 4 – Put It Under Git

One of the reasons I like Hugo is that everything is code. So before doing anything else I initialise Git.

```bash
git init
```

Then make the first commit.

```bash
git add .
git commit -m "Initial Hugo site"
```

Now every change you make can be tracked and rolled back if needed.

---

# Step 5 – Create a Repository on GitHub

Head over to GitHub and create a new repo for your blog. Don't add:

- README
- Licence
- `.gitignore`

We'll push everything from our local copy instead.

---

# Step 6 – Connect GitHub

Copy the repository URL.

Then back in the terminal:

```bash
git remote add origin https://github.com/<username>/engineering-blog.git
```

Push it.

```bash
git branch -M main
git push -u origin main
```

At this point your source code lives in two places:

- Your laptop
- GitHub

---

# Step 7 – Install a Theme

Without a theme Hugo doesn't have anything to render.

```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
```

Tell Hugo to use it.

Open:

```
hugo.toml
```

Add:

```toml
theme = "PaperMod"
```

---

# Step 8 – Start the Dev Server

Run:

```bash
hugo server
```

Now open:

```
http://localhost:1313
```

Whenever you save a file the browser automatically refreshes. No restart needed.

---

# Step 9 – Write Your First Post

```bash
hugo new posts/my-first-post.md
```

Hugo creates the file with some useful metadata already included. Open it and change:

```yaml
draft: true
```

to:

```yaml
draft: false
```

Otherwise it won't appear on your website.

Then start writing.

Everything below the front matter is just Markdown.

---

# Step 10 – If you want to add an Image

Create a folder called:

```
static/images
```

Drop an image inside.

Reference it like this:

```md
![Architecture](/images/architecture.png)
```

---

# Step 11 – Commit Your Changes

Once you're happy:

```bash
git add .
git commit -m "Add first blog post"
```

Exactly the same workflow you'd use for any project.

---

# Step 12 – Deploy Automatically

No need to manually update files. Instead add a GitHub Actions workflow.

Whenever I push to `main`, GitHub:

- Checks out the repository
- Installs Hugo
- Builds the site
- Deploys it to GitHub Pages

After that, publishing is simply:

```bash
git push
```

About a minute later the live blog updates itself.



