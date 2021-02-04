# HEAD、master和branch

## HEAD：

个人理解HEAD是一个引用，指向当前commit，具有唯一性，即每个仓库中有且只有一个HEAD。在每次提交时，HEAD都会自动向前移动到最新的commit。

## branch：

branch（分支）是一类引用，HEAD除了直接指向commit，也可以通过指向某个branch来间接指向commit。当HEAD指向一个branch时，commit发生时，HEAD会带着它指向的branch一起移动。

## master：

master是Git中默认的branch，它和其他branch的区别在于：

1.新建的仓库中的第一个commit会被master自动指向；

2.在git clone时，会自动checkout出master。

## branch的创建、切换和删除：

1.创建branch：git branch 名称 或 git checkout -b 名称（创建后自动切换）；

2.切换branch：git checkout 名称；

3.删除branch：git branch -d 名称 或 git branch -D 名称（强制删除分支）

