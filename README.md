# protobuf-tools
#### nodejs buffer http request tool (http请求工具)

`基于protobufjs的请求封装，您现在可以使用protobuf-tools进行http请求`

## 基础和proto文件
##### 您需要准备一份proto文件与数据库或他人进行传输

* 您需要一份支持proto3的proto文件；
* You need a protobuf file supported by "proto3";
* 使用 npm install protobuf-tools --save 进行安装；
* use npm install protobuf-tools --save to install
* 我们使用了es6的 Promise，nodejs低版本不兼容，尽量升级到nodejs最新版本。:) 
* now we use Promise for asynchronous request, so we recommend that you may use the latest version of nodejs.

## 使用方法

#### 1. 配置案例

使用protobuf-tools提供的init方法，对您的请求地址和请求头进行定义
-- use protofuf-tools for init;

```javascript
var protoBuffer = require("protoBuf-tools");
var path = require("path");
var filepath = path.join(__dirname,"./protos/XXXX.proto"); //您的proto文件地址

protoBuffer.init({
    headers:{}, //headers
    hostname: 'XX.XX.XX.XX', // domain or host only one can be used
    apiPort: yourAPIport,
    package: "teacher",  //proto packagename
    domain:"http://domain.com", // domain or host only one can be used
    protoReqList:{
        req:"resp"  // dictionnary for proto messages
    },
    filePath: filepath
});

```

#### 2. 单次请求案例

single request
```javascript

protoBuffer.singleRequest(
    "req",
    "POST",
    {
        id:"10000"
    },
    function(data){
        console.log(data);
        // signleRequest data .
    }
);


```

#### 3. 多次请求案例
multi requests
protobuf-tools提供单次请求和多次请求方法，如果您的应用需要多次请求并合并处理数据，我们提供的multipleRequests方法再适合不过了。

```javascript

protoBuffer.multiRequests([
    {
        reqProtoMessageName: "req",
        method:"POST",
        data:{
            id:"10000"
        }
    },
    {
        reqProtoMessageName: "req",
        method:"POST",
        data:{
            id:"10000"
        }
    },
],function(data){
    console.log(data);
    // multiRequest data .
});

```

快点尝试吧！