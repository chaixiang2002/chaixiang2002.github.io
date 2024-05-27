[Reddit - Dive into anything](https://www.reddit.com/r/LineageOS/comments/orm6ty/trying_to_sync_los_source_but_i_get_error/)

1.  `repo forall -vc "git reset --hard"`

2.  `repo sync`

这个命令 `repo forall -vc "git reset --hard"`是用来重置每个仓库到它们的初始状态，也就是说，它会丢弃所有未提交的修改。这可能有助于解决同步过程中遇到的问题。
