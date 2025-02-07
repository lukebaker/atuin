<h1 align="center">
  Atuin
</h1>

<p align="center">
<em>神奇的 shell 历史记录</em>
</p>

<p align="center">
  <a href="https://github.com/ellie/atuin/actions?query=workflow%3ARust"><img src="https://img.shields.io/github/workflow/status/ellie/atuin/Rust?style=flat-square" /></a>
  <a href="https://crates.io/crates/atuin"><img src="https://img.shields.io/crates/v/atuin.svg?style=flat-square" /></a>
  <a href="https://crates.io/crates/atuin"><img src="https://img.shields.io/crates/d/atuin.svg?style=flat-square" /></a>
  <a href="https://github.com/ellie/atuin/blob/main/LICENSE"><img src="https://img.shields.io/crates/l/atuin.svg?style=flat-square" /></a>
  <a href="https://discord.gg/Fq8bJSKPHh"><img src="https://img.shields.io/discord/954121165239115808" /></a>
</p>

<p align="center">
  <img src="../../demo.gif" alt="animated" width="80%" />
</p>

<p align="center">
<em>显示退出代码、命令持续时间、上次执行时间和执行的命令</em>
</p>

[English] | [简体中文]

Atuin 使用 SQLite 数据库取代了你现有的 shell 历史，并为你的命令记录了额外的内容。此外，它还通过 Atuin 服务器，在机器之间提供可选的、完全加密的历史记录同步功能。


除了搜索 UI，它还可以执行以下操作：

```
# 搜索昨天下午3点之后记录的所有成功的 `make` 命令
atuin search --exit 0 --after "yesterday 3pm" make
```

你可以使用我(ellie)托管的服务器，也可以使用你自己的服务器！或者干脆不使用 sync 功能。所有的历史记录同步都是加密，即使我想，也无法访问你的数据。且我**真的**不想。

## 特点

- 重新绑定 `up` 和 `ctrl-r` 的全屏历史记录搜索UI界面
- 使用 sqlite 数据库存储 shell 历史记录
- 备份以及同步已加密的 shell 历史记录
- 在不同的终端、不同的会话以及不同的机器上都有相同的历史记录
- 记录退出代码、cwd、主机名、会话、命令持续时间，等等。
- 计算统计数据，如 "最常用的命令"。
- 不替换旧的历史文件
- 通过 <kbd>Alt-\<num\></kbd> 快捷键快速跳转到之前的记录
- 通过 ctrl-r 切换过滤模式;可以仅从当前会话、目录或全局来搜索历史记录

## 文档

- [快速开始](#快速开始)
- [安装](#安装)
- [导入](./import.md)
- [配置](./config.md)
- [历史记录搜索](./search.md)
- [历史记录云端同步](./sync.md)
- [历史记录统计](./stats.md)
- [运行你自己的服务器](./server.md)
- [键绑定](./key-binding.md)
- [shell补全](./shell-completions.md)

## 支持的 Shells

- zsh
- bas
- fish
 
## 社区

Atuin 有一个 Discord 社区, 可以在 [这里](https://discord.gg/Fq8bJSKPHh) 获得

# 快速开始
  
## 使用默认的同步服务器
  
这将为您注册由我托管的默认同步服务器。 一切都是端到端加密的，所以你的秘密是安全的！
  
阅读下面的更多信息，了解仅供离线使用或托管您自己的服务器。

```
bash <(curl https://raw.githubusercontent.com/ellie/atuin/main/install.sh)

atuin register -u <USERNAME> -e <EMAIL> -p <PASSWORD>
atuin import auto
atuin sync
```
  
## 仅离线 (不同步)
  
```
bash <(curl https://raw.githubusercontent.com/ellie/atuin/main/install.sh)
            
atuin import auto
```

## 安装

### 脚本 (推荐)

安装脚本将帮助您完成设置，确保您的 shell 正确配置。 它还将使用以下方法之一，在可能的情况下首选系统包管理器（pacman、homebrew 等）。

```
# 不要以root身份运行，如果需要的话，会要求root。
bash <(curl https://raw.githubusercontent.com/ellie/atuin/main/install.sh)
```

### 使用cargo

最好使用 [rustup](https://rustup.rs/) 来设置 Rust 工具链，然后你就可以运行下面的命令:

```
cargo install atuin
```

### Homebrew

```
brew install atuin
```
  
### MacPorts

Atuin 也可以在 [MacPorts](https://ports.macports.org/port/atuin/) 中找到
  
```
sudo port install atuin
```

### Pacman

Atuin 在 Arch Linux 的 [社区存储库](https://archlinux.org/packages/community/x86_64/atuin/) 中可用。

```
pacman -S atuin
```

### 从源码编译安装

```
git clone https://github.com/ellie/atuin.git
cd atuin
cargo install --path .
```

## Shell 插件

安装二进制文件后，需要安装 shell 插件。 
如果你使用的是脚本安装，那么这一切应该都会帮您完成！

### zsh

```
echo 'eval "$(atuin init zsh)"' >> ~/.zshrc
```

或使用插件管理器:

```
zinit load ellie/atuin
```

### bash

我们需要设置一些钩子(hooks), 所以首先需要安装 bash-preexec :

```
curl https://raw.githubusercontent.com/rcaloras/bash-preexec/master/bash-preexec.sh -o ~/.bash-preexec.sh
echo '[[ -f ~/.bash-preexec.sh ]] && source ~/.bash-preexec.sh' >> ~/.bashrc
```

然后设置Atuin

```
echo 'eval "$(atuin init bash)"' >> ~/.bashrc
```

### fish

添加

```
atuin init fish | source
```

到 ~/.config/fish/config.fish 文件中的 is-interactive 块中

## ...这个名字是什么意思?

Atuin 以 "The Great A'Tuin" 命名, 这是一只来自 Terry Pratchett 的 Discworld 系列书籍的巨龟。


[English]: ../../README.md
[简体中文]: ./README.md