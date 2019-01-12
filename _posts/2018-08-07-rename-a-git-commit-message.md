---
classes: wide
tags: [git]
---
To rename the last commit message simply use the following Git command:

<code class="EnlighterJSRAW" data-enlighter-language="shell">git --amend -m"The new commit message."</code>

To rename a previous commit message that isn't the last commit:
<ol>
 	<li style="list-style-type: none;">
<ol>
 	<li style="list-style-type: none;">
<ol>
 	<li>Type the following command: <code class="EnlighterJSRAW" data-enlighter-language="shell">git rebase -i HEAD~n</code> , where n is the number of commits to list, this should include the commit you want to change.</li>
 	<li>Locate the commit you want to edit and change the first word from <em>pick</em> to <em>reword</em>, then save the file and exit.</li>
 	<li>The commit you want to edit should immediately open where you can change the message on the first line. Then save the file.</li>
 	<li>Lastly push the commit with <code class="EnlighterJSRAW" data-enlighter-language="shell">git push -f</code> .</li>
</ol>
</li>
</ol>
</li>
</ol>
