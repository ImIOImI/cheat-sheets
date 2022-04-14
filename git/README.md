### Pruning local branches
This deletes all local branches that don't have unmerged changes and whose remotes were deleted 
from the remote

```shell
git fetch -p ; git branch -r | awk '{print $1}' | egrep -v -f /dev/fd/0 <(git branch -vv | grep origin) | awk '{print $1}' | xargs git branch -d
```
