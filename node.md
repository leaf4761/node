# node环境搭建

window下搭建nvm环境
### 下载nvm
nvm下载地址：[nvm][nvm]

[nvm]: https://github.com/coreybutler/nvm-windows/releases "nvm下载地址"

下载免安装版本nvm-noinstall.zip，放到开发目录并解压

### 配置
1. 此处在H盘根目录新建nvm目录，把解压后的内容放入其中 H:/nvm
2. 编辑器打开H:/nvm/install.cmd文件，修改其中setx /M NVM_SYMLINK 路径为H:/node
3. 右键以管理员身份运行install.cmd，会提示输入NVM_PATH，输入H:/nvm
4. 执行完毕后，会在NVM_PATH目录下生成setting.txt文件，同时在path中修添加好%NVM_HOME%;%NVM_SYMLINK%"，修改setting.txt文件内容,setting.txt文件内容如下：

        root: H:\nvm 
        path: H:\nodejs 
        arch: 32 
        proxy: none
        node_mirror: http://npm.taobao.org/mirrors/node/
        npm_mirror: https://npm.taobao.org/mirrors/npm/

    注意：不要在path对应的目录下存在nodejs文件或者文件夹，因为后面nvm要创建名称为nodejs快捷方式，否则因为文件名称冲突而导致创建快捷方式失败
5. 查看配置环境变量，若第2步执行完后，path中并未添加NVM_HOME和NVM_SYMLINK，则手动添加。命令行nvm v 或者nvm version 查看nvm的版本号，验证是否安装配置成功
6. nvm常用命令

        nvm install latest //安装最新版本的node.js；node -v 查看node.js的版本号
        nvm list  //列出所有已经安装的node.js版本号
        nvm use [版本号] //使用哪一个版本的node.js；使用哪一个版本第二步的path下的nodejs快捷方式就指向哪个版本的nodejs模块
        nvm node_mirror [url] //设置node下载源,不写url设置回默认，默认是https://nodejs.org/dist/
        nvm npm_mirror [url] //设置npm下载源,不写url设置回默认，默认是https://github.com/npm/npm/archive/
        nvm install <version> [arch] //安装指定版本的node.js，version可通过上面的地址查看，acrh系统多少位(32或者64，不写默认64)
        nvm uninstall <version> //卸载制定的版本

### npm全局配置
以上是使用nvm可以安装和管理不同版本的node.js，而每一个版本的node.js都自带了一个npm模块

此时可以安装一个全局的npm，安装步骤如下：

1. 打开命令行，执行 npm config set prefix="H:\nvm\npm" 配置npm的全局安装路径，在当前用户目录下生成一个.npmrc文件，内容如下所示：prefix=H:\nvm\npm
2. 执行npm install npm -g，就会在prefix对应的路径下安装一个全局的npm包了，npm安装其他包的时候加上-g，也会安装在这个目录，而且使用的是这时全局的npm。如果不使用全局的npm安装其他包，使用node自带的指定版本的npm安装的包，nvm use切换到其他版本的npm就使用不了。 
3. 配置 NPM_HOME 环境变量
path环境变量添加%NPM_HOME%，注意：要将这个环境变量放在%NVM_SYMLINK% 的前面才有生效，否则被它抢先覆盖了。

npm install moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 不会将模块依赖写入devDependencies或dependencies 节点。
3. 运行 npm install 初始化项目时不会下载模块。

npm install -g moduleName 命令
1. 安装模块到全局，不会在项目node_modules目录中保存模块包。
2. 不会将模块依赖写入devDependencies或dependencies 节点。
3. 运行 npm install 初始化项目时不会下载模块。

npm install -save moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 会将模块依赖写入dependencies 节点。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行npm install --production或者注明NODE_ENV变量值为production时，会自动下载模块到node_modules目录中。

npm install -save-dev moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 会将模块依赖写入devDependencies 节点。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行npm install --production或者注明NODE_ENV变量值为production时，不会自动下载模块到node_modules目录中。

### nrm安装
nrm(npm registry manager)，即npm的下载源管理工具，安装步骤如下：

    npm install nrm -g //安装nrm
    nrm ls //显示所有可用的下载源
    nrm use [xxx] //使用指定的下载源
### npm安装软件过慢
可以使用其他源进行安装

1. 临时使用：

        npm --registry https://registry.npm.taobao.org install express
2. 永久使用：

        npm config set registry https://registry.npm.taobao.org
3. 安装cnpm

        npm install -g cnpm --registry=https://registry.npm.taobao.org
        cnpm install express