# mongodb安装
mongodb下载地址：[mongodb][mongodb]

[mongodb]: https://www.mongodb.com/ "mongodb官网"

下载windows版本后为压缩包，直接解压即可，例如解压至：C:\mongodb-4.0.3

在根目录下创建conf和data目录，目前根目录下包含bin, conf, data三个目录，在data目录中出创建db和log目录

在conf目录下创建mongod.cfg文件，内容如下：

    systemLog:
        destination: file
        path: C:\mongodb-4.0.3\data\log\mongod.log
    storage:
        dbPath: C:\mongodb-4.0.3\data\db

在data\log目录下创建日志文件mongod.log

在环境变量中添加MONGO_HOME变量，值为`C:\mongodb-4.0.3`

添加path变量`%MONGO_HOME%\bin`

mongodb启动命令

    mongod --config C:\mongodb-4.0.3\conf\mongod.cfg

为方便使用，可以新建一个.bat文件，编辑以下内容：

    echo "MongoDB starting..."
    mongod --config C:\mongodb-4.0.3\conf\mongod.cfg
    pause