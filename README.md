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