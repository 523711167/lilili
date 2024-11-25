Git revert

git revert -n hashId hashId hashId

还原hashId提交内容，保存在暂存区，revert多个，如果遇见冲突，解决冲突后，

git revert --continue继续还原。