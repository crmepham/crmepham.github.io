If you are using GitFlow you will typically need to create a branch from 'Develop' to do your development work. To create the branch follow these steps:
<ol>
 	<li>Clone the respository <code class="EnlighterJSRAW" data-enlighter-language="shell">git clone git@bitbucket.org:example/example-repo.git</code></li>
 	<li>Create the branch in the remote repository.</li>
 	<li>Identify the repo with <code class="EnlighterJSRAW" data-enlighter-language="shell">git branch</code>  (optional)</li>
 	<li>Tell the local repo. about any remote branches that exist <code class="EnlighterJSRAW" data-enlighter-language="shell">git branch</code></li>
 	<li>Checkout the remote branch <code class="EnlighterJSRAW" data-enlighter-language="shell">git checkout feature/branch-namr</code></li>
</ol>
Now you can make local changes in this branch and push them to the remote branch.

When you have completed the branch development you will then want to submit a pull request so the work can be reviewed before being pulled into the 'Develop' branch.
