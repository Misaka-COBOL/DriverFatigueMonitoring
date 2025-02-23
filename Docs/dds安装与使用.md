# Fast DDS 安装

## 个组件的作用：

Foonathan Memory：

Foonathan Memory 是一个内存分配库，专门为实时应用程序设计。它提供高效的内存管理，特别适用于像 Fast DDS 这样需要高性能和低延迟的系统。

Fast CDR：

Fast CDR 是一个高效的序列化/反序列化库，使用 CDR（Common Data Representation）格式。它用于在 DDS (Data Distribution Service) 中对数据进行序列化和反序列化，确保数据在网络上传输时的高效性和一致性。

Fast DDS：

Fast DDS 是一个符合 DDS 标准的发布-订阅中间件。它用于分布式系统中的数据通信，提供可靠且高效的数据传输。它实现了实时系统所需的 QoS (Quality of Service) 功能，并且支持各种网络和传输协议。

Fast DDS-Gen：

Fast DDS-Gen 是一个代码生成工具。它用于根据 IDL（Interface Definition Language）文件自动生成数据类型和代码，使开发者能够更方便地在 Fast DDS 中使用这些数据类型。


## 安装编译工具：
sudo apt install cmake g++ python3-pip wget git
## 安装 Fast DDS 依赖库：
sudo apt install libasio-dev libtinyxml2-dev

## 编译安装 Foonathan memory：
```bash

mkdir Fast-DDS
cd Fast-DDS
git clone https://github.com/eProsima/foonathan_memory_vendor.git
mkdir foonathan_memory_vendor/build
cd foonathan_memory_vendor/build
cmake .. -DCMAKE_INSTALL_PREFIX=~/Fast-DDS/install -DBUILD_SHARED_LIBS=ON
cmake --build . --target install

```
## 编译安装 Fast CDR：

```bash
cd ~/Fast-DDS
git clone https://github.com/eProsima/Fast-CDR.git
mkdir Fast-CDR/build
cd Fast-CDR/build
cmake .. -DCMAKE_INSTALL_PREFIX=~/Fast-DDS/install
cmake --build . --target install
```
## 编译安装 Fast DDS：

```bash
cd ~/Fast-DDS
git clone https://github.com/eProsima/Fast-DDS.git
mkdir Fast-DDS/build && cd Fast-DDS/build
cmake .. -DCMAKE_INSTALL_PREFIX=~/Fast-DDS/install
cmake --build . --target install
```
## 编译安装 Fast DDS-Gen：

```bash
sudo apt update
sudo apt install openjdk-11-jdk
cd ~/Fast-DDS
git clone https://github.com/eProsima/Fast-DDS-Gen.git
cd Fast-DDS-Gen
./gradlew assemble
```
## 配置环境变量：

``` bash
echo 'export LD_LIBRARY_PATH=/home/your_username/Fast-DDS/install/lib' >> ~/.bashrc
source ~/.bashrc
```
## 测试安装： 创建测试用例文件夹并运行 HelloWorld 示例：

```bash
mkdir -p ~/Fast-DDS/examples/C++/HelloWorld && cd ~/Fast-DDS/examples/C++/HelloWorld
echo 'struct HelloWorld { unsigned long index; string message; };' > HelloWorld.idl
~/Fast-DDS/Fast-DDS-Gen/scripts/fastddsgen -example CMake ./HelloWorld.idl
mkdir build && cd build
cmake .. -DCMAKE_PREFIX_PATH=~/Fast-DDS/install
make
```
##运行测试： 打开两个终端，分别运行 publisher 和 subscriber：

```bash
./HelloWorld publisher
./HelloWorld subscriber
```