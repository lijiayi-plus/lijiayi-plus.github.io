---
title: "43 在linux中配置C环境"
date: 2026-11-01T14:03:24+08:00
# cover: "https://..."
# series: "一生一芯"
# weight: 10
# tags: ["学习记录"]
draft: false
---

### 安装配置环境：

下载包库
```bash
sudo apt update
sudo apt install -y build-essential neovim gdb cmake git
nvim --version
```
新建所需文件
```bash
mkdir -p ~/cpp
cd ~/cpp
```

### 开始使用的一些命令

```
cd ~/cpp
nvim hello.cpp

```
1. 然后按`i`进入编辑模式
2. 输入代码
3. 按`esc`退出编辑模式
4. 输入`:wq`，回车保存并退出

编译：
```bash
g++ -std=c++17 hello.cpp -o hello

./hello
```
预期输出：Hello C++!

示例的c代码：
```c++
#include <iostream>
using namespace std;

int main() {
    cout << "Hello C++!" << endl;
    return 0;
}
```