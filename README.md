## 添加子模块
```
git submodule add <submodule git url> <submodule path in main project>
```
注意主项目应当提交commit后再执行添加submodule，否则当将submodule放到嵌套目录时会报错。

## 克隆含有submodules的repo
```
git clone <main project> // 此时submodules目录下为空
git submodule init // 初始化本地配置文件
git submodule update // 进行submodule文件拉取
// 后两步可合并为：
git submodule update --init [--recursive]
```
以上三个命令可以合成一个：
```
git clone --recurse-submodules <main project>
```
## 拉取子模块更新
当在主项目执行`git pull`时并不会把子模块中的更新拉取到本地，因此要更新子模块还需要一些额外的操作：

- 方式一：
进入到子模块目录后执行`git fetch`和`git merge`。执行`git diff --submodule`可查看子模块中的更新。

- 方式二：
在主项目中执行
```
git submodule update --remote [path of submodule, 如果省略会拉取所有submodules更新]
```
需要注意的是，拉取了子模块更新后，子模块将留在一个称作"游离的HEAD"状态（有一个commit id），这样意味着没有本地的工作分支跟踪改动（main project仍可以推送子模块的更新到远程）。
如果需要在main project中修改子模块怎么办？解决这个问题需要额外做两件事：
- 进入子模块checkout出目标分支例如`master`
- 运行`git submodule update --remote --merge`来从上游拉取新工作并合并到本地分支上

