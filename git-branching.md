Git branching guidelines:
=========================
###### Inspired by: http://nvie.com/posts/a-successful-git-branching-model/
---

## Features/Issues development
`devel/` is the prefix for feature development branches.
Followed by an explicit name in lower case, dash-separated.
Should start with issue-xxxx if linked to a specific referenced issue
Ex.:
```bash
git checkout -b devel/global-orders master
git checkout -b devel/issue-1234-fx-rejected master
```
These branches will usually derive from master, except an existing release branch needs a significant extra development (see below release branches):
```bash
git checkout -b devel/global-fx-new-flow release/v1.2.3-global
```

## Releases
`release/`
is the prefix for release branches.
Followed by a version number following the semantic versioning form (http://semver.org/): vMAJOR.MINOR.PATCH
With: MAJOR:branking changes, MINOR:non-breaking new features, PATCH: transparent fixes
And optionally a dash-separated title.
Release branches must always derive from master.
Ex.:
```bash
git checkout -b release/v1.2.3-global master
```
Development/issues branches should be merged together into a release branch before integration/UAT tests.
Small extra-work and hotfixes can be performed in the release branch, history rewrite/cleanup is recommended (git rebase -i)
Merging feature branches into release branches should be performed with --no-ff option in order to always create a merge commit, which allows easily reverting if necessary, and makes merging history traceable.
Ex.:
```bash
git checkout release/v1.2.3-global
git merge --no-ff devel/global-orders
```

## Hotfixes
`hotfix/` is the prefix for hotfix branches.
Followed by issue-number-title or appropriate name
Hotfix branches must derive from master. They are intended for small quick foxes of Production version.
Ex.
```bash
git checkout -b hotfix/issue-2345-convbond-imp-err
```
Merging feature branches should be performed with --no-ff option in order to always create a merge commit, which allows easily reverting if necessary, and makes merging history traceable.
Ex.:
```bash
git checkout master
git merge --no-ff hotfix/issue-2345-convbond-imp-err
```
If a release branch is currently being tested/prepared, the hotfix must be merged into it as well:
git checkout release/v1.2.3-global
git merge --no-ff hotfix/issue-2345-convbond-imp-err
 
Once merged, devel and hotfix branches should be cleaned up in order to avoid infinite growing of the branch list (safe as -d prevents deleting non-merged branches):
```bash
git branch -d devel/global-orders
```
And the remote branch:
```bash
git push --delete origin devel/global-orders
```

## Production
`master` is the current Production branch (protected: forced push blocked by gitlab)
Once validated, a release branch should be merged into master just before to deploy in Production.
git checkout master
```bash
git merge --no-ff release/v1.2.3-global
```
Finally, that commit on master must be tagged with the version number, easy future reference to this historical version:
```bash
git tag -a v1.2.3-global
```
