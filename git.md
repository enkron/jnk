# git
```bash
git log                      # show commits
git log --graph --decorate --pretty=oneline --abbrev-commit #more pretty log
git show <commit_id> --color # show commit detailed information
git log --follow -- <filename>  # show all commits related to certain file
git diff                     # see what exactly will change

#annotated tag
git tag -a v1.0 -m ‘Version 1.0’ <tagname>
git tag

git push origin --tags

git push --delete origin tagName - delete tag remotely
git tag -d tagName               - delete tag locally

#<tagname> - The object that the new tag will refer to,
#                usually a commit. Defaults to HEAD.

git push -o merge_request.create -o merge_request.target=branch_name
# create merge request with push option and choose target branch

git push --set-upstream origin feature/<some_branch_name>

git branch --set-upstream-to=origin/feature/<some_branch_name>
# setup to track remote branch 'feature/<some_branch_name>
git branch -vv
# check what which remote branch are tracking (connect local and remote branhces)

git commit --amend #do last commit again

git revert -n <bad_commit_number> #revert commit with needed changes
git commit <path/to/file/to/revert> -m 'reverted some file' #commit files that we want to change
git reset --hard Head #reset all changes to the last state

git branch --delete <branch_name> #delete branch localy
git push <remote_name(always: origin)> --delete <branch_name> #delete branch remotely

git reset --hard HEAD~1 #reset all changed to the commit previous HEAD

git config --global color.ui auto #color git output

git rev-list --count develop #count commits on certain branch

#delete all your commit history but keep the code in its current state
git checkout --orphan <tmp_branch> 
git add -A #add all the files
git commit -am "commit message"
git branch -D master
git branch -m master #rename the current branch to master
git push -f origin master #finally, force update your repository

#squashing commits into one
git rebase -i <commit_hash> #all commits above this hash up to HEAD will be merged into one
#in the pop-up editor window will be the commits list in !reverse-order!
#mark the old-one (at the top) as 'pick' and the rest of all commits as 'squash'
#save changes, make result final commit
git push --force #(--force-with-lease? in newer versions) to update upstream with local branch
#NOTE:  the pushed branch should only mirror your work, not be the authoritative branch,
#so 'force push' is acceptable.))

git checkout <some_branch_name> path/to/a/needed/file # merge a particular file into a working branch

git remote update origin --prune # update the local list of remote branches
```
