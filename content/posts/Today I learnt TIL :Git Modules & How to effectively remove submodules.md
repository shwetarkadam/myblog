+++
title = "Today I learnt TIL :Git Modules & How to effectively remove submodules"
author = ["Shweta Kadam"]
date = 2023-01-01T00:30:00+05:30
tags = ["git", "submodule", "gitsubmodule", "github", "til"]
draft = false
+++

While I migrating this website, I came across many issues. One such issue was git submodule.So here is a post on it.


## what is a git submodule? {#what-is-a-git-submodule}

Git submodule is a way to include another repository in Git as a sub directory in one repository.

It allows you to keep another repo(your own repo or someone else) in your repo as a subdirectory
It is useful for track that repo's  changes and use that project repo as a reference.

```bash
git submodule add https://github.com/username/repo-name.git
```

It’s important to note the `username` of the repo you are adding.
Because whose username is present in the repo, the repo belongs to them. So they have ownership of the repo and the changes over it.


## What issue I faced ? {#what-issue-i-faced}

I use Hugo Papermod theme for this website.
I used the git submodule method for installing this theme in my Hugo repo.

```bash
git submodule https://github.com/adityatelange/hugo-PaperMod.git --depth=1
```

Instead of

```bash
git submodule https://github.com/MY-GITHUB-USERNAME/hugo-PaperMod.git --depth=1
```


## What did this lead to? {#what-did-this-lead-to}

For adding  GitHub comments feature, the changes had to be done inside `layout/partials/comments.html`

This file is present in the submodule directory.This lead to the below error:

```bash
warning: adding embedded git repository: themes/PaperMod
hint: You’ve added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint:
hint:     git submodule add <url> themes/PaperMod
hint:
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint:
hint:     git rm --cached themes/PaperMod
hint:
hint: See “git help submodule” for more information.
```

I couldn’t push my changes into repo since I did not have ownership over it


## How to solve this? {#how-to-solve-this}

There were two ways to solve this:-

1.  I make a PR of my changes in aditya subdirectory.

The owner approves my changes.
This is not possible in this case since these changes are custom to my repo and not feature enhancement or bug fix

1.  I remove all git submodule of Aditya ’s changes .Fork Aditya papermod theme(so now the forked repo belong to me ) and link the git submodule to my forked repo.

I went with the second route.

But turns out removing all references of git submodule can be quite annoying.

Every time I thought I removed all submodule references using stackoverflow answers I ended up on the same above error.
This meant there were still submodule references present.

Found this useful [Github Gist](https://gist.github.com/myusuf3/7f645819ded92bda6677)

-   Delete the relevant section from the .gitmodules file. Delete the relevant section from the `.gitmodules` file.

In my case entries looked like

```bash
│ [submodule “themes/PaperMod”]
    2   │     path = themes/PaperMod
    3   │     url = https://github.com/adityatelange/hugo-PaperMod.git
```

-   Stage the .gitmodules `changes git add .gitmodules`
-   Delete the relevant section from `.git/config`
    For me no submodule entries were present.

-   Run `git rm --cached path_to_submodule` (no trailing slash).In my case it was `git rm --cached themes/Papermod`

-   Run `rm -rf .git/modules/path_to_submodule` (no trailing slash).
-   Commit `git commit -m “Removed submodule ”`
-   Delete the now untracked submodule files `rm -rf path_to_submodule`

This removed my git submodules entries.
And then again created a submodule entry with my usernameAnd that's how the git submodule error was solved.
