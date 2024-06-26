# 微服务系统中的DAI-gRPC客户端子模块

本项目为微服务系统中其他使用Python语言开发的服务提供gRPC客户端代码。我们利用Protocol Buffers (protobuf) 定义了服务接口，并通过gRPC生成了相应的Python客户端和服务端代码。此外，我们在生成的代码基础上进一步封装了一层API，以简化服务间通信的开发工作。

该项目作为子模块使用，对于使用该子模块的项目，gRPC代码按照下述方式生成和管理

## 生成gRPC代码

请确保已安装Protocol Buffers编译器(protoc)和gRPC Python插件。使用以下命令生成每个模块的gRPC代码：

```
protos=(
    module1
    module2
)

for proto in "${protos[@]}"
do
    mkdir -p ./generated/protos/$proto/
    cp ./resources/protos/$proto.proto ./generated/protos/$proto/
    python3 -m grpc_tools.protoc -I . --python_out=. --grpc_python_out=. ./generated/protos/$proto/$proto.proto
    rm ./generated/protos/$proto/$proto.proto
done
```

## 项目结构

```
.
├── generated                 # 自动生成的gRPC代码目录
│   ├── protos                # 按模块分组的protobuf定义文件和生成的代码
│   │   ├── module1           # module1 的gRPC Python代码
│   │   │   ├── module1_pb2.py          # protobuf消息类
│   │   │   └── module1_pb2_grpc.py     #gRPC服务类和客户端存根
│   │   ├── module2           # module2 的gRPC Python代码
│   │   │   ├── module2_pb2.py
│   │   │   └── module2_pb2_grpc.py
```

## gRPC依赖版本

```
grpcio==1.60.0
grpcio-tools==1.60.0
protobuf==4.21.6
```
