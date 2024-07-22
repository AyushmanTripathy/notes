# GIT

from: oh my git, progit, [think like git](https://think-like-a-git.net/)

## Version Control systems types

1. Local version control
1. Centralized version control
1. Distributed version control (this is git)

## Graph Theory

-   seven bridges of konigsberg (prussia)
-   can you visit all the bridges but excatly once?
-   euler while solving this question, invented the feild.

## References

-   pointers to commits (40 bytes long)
-   references makes commits reachable
-   found in the `.git/refs/heads`
-   cheap branching, means easy to create branching because refs
-   types

1. Local branch references
1. Remote branch references
1. Tag references

-   tag references never change, see `tag`

## Branches

- are references, like savepoints for commits
- provide a easy way to jump between commits
- `rebase` and `merge` will not change existing commits
- so, making a temporary branch keeps you 100% safe

## Garbage Collection

-   ids of commits are SHA1 hash of contents and parent's ids
-   append changes to last commit, create a new commit

```
git commit --amend
```

-   the last is still their on the disk, but not visible on the log
-   you can get rid of all the commits (like one above) not involved in the tree by

```sh
git gc
```

-   starting from every branch and tag, walks through the graph, to get list of every reachable commit.
-   not reachable commits are removed

## Rebase

- consider 2 branches with endings E and H

```
A - B - C - D - E
    \- F - G - H
```

```bash
# on commit E
git cherry-pick H
```

- will gives all the changes in H combined with E as H'
- `cherry-pick` is moving a single commit

```
A - B - C - D - E - H'
    \- F - G - H
```

- rebase, moves multiple commits at onces

```
git rebase E H
```

- this would add all commits of H branch into E
- after rebase 

```
A - B - C - D - E - F' - G' - H'
```


## Mics

-   better printing of logs

```
git log --all --oneline --graph --decorate
```
