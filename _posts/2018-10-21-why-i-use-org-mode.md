---
layout: post
title: "Why I use org-mode"
headerImage: false
author: sainathadapa
tag:
  - org-mode
category: blog
description: "Few reasons why you should also use org-mode"
---

I tried Evernote, WorkFlowy, and OneNote for note-taking before settling on using [Org-mode](https://en.wikipedia.org/wiki/Org-mode). In this post, I list some of the reasons I finally chose org-mode (and been using it for more than 2 years now).


![org-mode-screenshot](/images/orgmode.png)
*The image shows an excerpt from my notes, illustrating the benefits of using org-mode*

### 1. Writing in plain text, Render with rich formatting
Org-mode stores notes in plain text, albeit in its own markup language. This prevents vendor lock-in. You can open the org-mode files in any text editor, when you do not have access to Emacs. You can also view the org-mode files through GitHub or GitLab, as both of these services render org files nicely à la markdown files. You can also export org files to HTML, Markdown, PDF, and a myriad of other formats.

### 2. Nested Notes, ability to collapse content
Like WorkFlowy, you can have nested notes in org-mode, and can easily fold/unfold notes at various depths. This was the initial reason why I moved to WorkFlowy from Evernote. But unlike Workflowy, you are not limited to just bullet points. You can write normal free-form text under any bullet point (heading). You can have nested lists in Evernote/OneNote, but long lists quickly become unwieldy as they do not allow collapsing notes.

### 3. Images in notes
With `org-download` plugin, it is easy to capture screenshots, save and display them in the notes.

### 4. Special characters, Superscript and Subscript
It it easy to write special characters - for example, you can write `\lambda` to display the λ character. Superscript can be achieved by inserting `^` between characters or words, for example `A^2`. Similarly, subscript can be done by inserting underscore between words.


## 5. Vim editing
I'm a big proponent of Vim, and use it everywhere even outside of programming. With Vim, you can quickly jump to different parts of text, you can move chunks of text or edit chunks of text quite easily, all with the help of a keyboard. With the help of the `evil` plugin, you can bring the Vim awesomeness to Emacs.

---

These are just few of the things that I like about org-mode. I didn't write about the other major benefit of using org-mode: Task management. This post started with an objective of writing about all the ways I use org-mode. The goal was ambitious and so I kept procrastinating (~6 months). Today, I decided to go with a short snippet of text, and either expand the article itself in the future with more details, or just write more short blog posts. 
