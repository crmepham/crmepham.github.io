---
ID: 942
post_title: Branch from another Git branch
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/branch-from-another-git-branch/
published: true
post_date: 2018-05-25 08:27:58
---
This will be needed when you want to start a development branch where the code is based on code that was committed in another branch and not the 'Develop' branch.

<em>Aside: If you already created the new branch incorrectly you can delete it using</em> <code class="EnlighterJSRAW" data-enlighter-language="shell">git branch -D feature/name-of-branch</code>

1. To see the list of currently checked out branches, and which branch you are currently in, use <code class="EnlighterJSRAW" data-enlighter-language="shell">git branch</code>. Ensure you are currently in the branch that you want to branch from.

2. To create the new branch use <code class="EnlighterJSRAW" data-enlighter-language="shell">git checkout -b feature/name-of-new-branch</code>.

3. Push the branch to remote using <code class="EnlighterJSRAW" data-enlighter-language="shell">git push --set-upstream origin feature/name-of-new-branch</code>.

You will automatically be switched to the newly created branch. If you wish to switch branch, use the command <code class="EnlighterJSRAW" data-enlighter-language="shell">git checkout feature/name-of-new-branch</code>.