[//]: # (title: Branch Remote Run Trigger)
[//]: # (auxiliary-id: Branch Remote Run Trigger)

A _Branch Remote Run Trigger_ automatically starts a new [Personal Build](personal-build.md) each time TeamCity detects changes in particular branches of the VCS roots of the build configuration. At the moment, the Trigger supports only Git and Mercurial VCSes.

For non-personal builds off branches, see [Working with Feature Branches](working-with-feature-branches.md). When `branch specification` is configured for a VCS root, Branch Remote Run Trigger only processes branches not matched by the specification.

A trigger monitors branches with names that match specific patterns.    
Default patterns are:
* for Git repositories: `refs/heads/remote-run/*`
* for Mercurial repositories: `remote-run/*`

These branches are regular version control branches and TeamCity does not manage them (i.e. if you no longer need the branch you would need to delete the branch using regular version control means).

By default, TeamCity triggers a personal build for the user detected in the last commit of the branch. You might also specify TeamCity user in the name of the branch. To do that, use a placeholder `TEAMCITY_USERNAME` in the pattern and your TeamCity username in the name of the branch. For example, the pattern `remote-run/TEAMCITY_USERNAME/*` will match a branch `remote-run/joe/my_feature` and start a personal build for the TeamCity user `joe` (if such user exists).

<note>

At the moment there is no UI to show what's going on inside the trigger, so the only way to troubleshoot it is to look inside `teamcity-remote-run.log`. To see a more detailed log, enable `debug-vcs` logging preset on the __Administration | Diagnostics__ page.
</note>

In order to trigger a build branch should have at least one new commit comparing to the main branch.

### Example: Run a personal build from a command line.

#### Git


```Shell

% cd <your local git repo>
% git branch
* master
% git checkout -b my_feature
Switched to a new branch 'my_feature'
//code, commit; code, commit
% git push origin +HEAD:remote-run/my_feature
```



With the default pattern (`refs/heads/remote-run/*`) command `git branch -r` will list your personal branches. If you want to hide them, change the pattern to `refs/remote-run/*` and push your changes to branches like `refs/remote-run/my_feature`. In this case your branches are not listed by the above command, although you can see them anyway using `git ls-remote <url of git repository>`.

#### Mercurial


```Shell
% cd <your local hg repo>
% hg branch
default
% hg branch remote-run/my_feature
marked working directory as branch remote-run/my_feature
//code, commit; code, commit
% hg push -b remote-run/my_feature --new-branch

```



### Limitations

If your build configuration has more than one VCS root which support branch remote\-run, and you push changes to all of them, TeamCity will start several personal builds with changes from one VCS root each.

 __  __

__See also:__



__Administrator's Guide__: [Git](git.md) | [Mercurial](mercurial.md)
