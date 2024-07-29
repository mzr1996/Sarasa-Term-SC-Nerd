# `Sarasa Term SC Nerd` 字体

## 关于

`Sarasa Term SC Nerd` 字体是以 [Sarasa Term
SC](https://github.com/be5invis/Sarasa-Gothic)字体为基础，修改了[Nerd
fonts](https://github.com/ryanoasis/nerd-fonts)字体补丁程序，然后用该程序将`Nerd
fonts`合并入`Sarasa Term SC`, 再经过一些后处理，而最后形成的字体。该字体特别适合
**简体中文**用户在**终端**或者**代码编辑器**中使用。

**在 [laishulu/Sarasa-Term-SC-Nerd](https://github.com/laishulu/Sarasa-Term-SC-Nerd) 的基础上，更新了上游版本**

上游版本：

- Sarasa Term SC：1.0.16
- Nerd Font: 3.2.1
- Font Patcher: 4.13.1

## 字体效果

- 文字效果：以 Regular 样式为例

  ![文字效果](screenshots/character.png)
- 图标效果：Powerline 图标

  ![图标效果](screenshots/nerd.png)
- 对齐效果：终端里 emacs/org-mode 中的表格对齐

  ![对齐效果](screenshots/align.png)

## 特性

- `Sarasa Term SC` 是极少数做到中文和英文 2:1 严格对齐的字体，特别适合用来写代
  码, 以及中英文混合的字符式表格的对齐等。
- `Nerd fonts` 提供了很多图标字体，特别适合各种 Zsh/Bash/Vim/NeoVim/Emacs 主题，
  例如 zsh 的 [`p10k`](https://github.com/romkatv/powerlevel10k),
  [`Powerline`](https://github.com/powerline/powerline) 等等。
- 一些符号进行了纵向拉伸，不会出现`Powerline`条带中高低不一，无法上下对齐的情况。
- 原始`Sarasa Term SC`字体和`Sarasa Term SC Nerd`字体可以共存，不会产生冲突。
- 将 `OS/2` 表中的 `xAvgCharWidth` 属性进行了设置，避免了在 windows 系统下，一些
  不支持新版本 `OS/2` 表的软件中字距不正常的问题。
- 加入了`hdmx`表，解决了 windows 系统下的一些情况下无法严格对齐的问题。
- 修正了`OS/2`表中的`panose`和`post`表中的`isFixedPitch`，使得字体被系统认出是等
  宽字体。
- 删除了 `Material` 字符集中的部分字符，避免超出字体字符数量上限

## 安装

- 手工下载安装：
  - 前往 [release](https://github.com/mzr1996/Sarasa-Term-SC-Nerd/releases) 下载
    `sarasa-term-sc-nerd.ttc.tar.gz`。
  - 将 `sarasa-term-sc-nerd.ttc.tar.gz` 解压即可得到字体文件。

## 使用

在你的主题配置文件中，使用 `Sarasa Term SC Nerd`。

## 如何生成字体

**根据我的实践，在原流程基础上做了一些修改，以下流程仅针对 Ubuntu 环境，其他环境可自行调整**

1. 安装依赖
   ```bash
   sudo apt install python3-fontforge fontforge
   ```

2. 下载并进入 `nerd font` 源码目录，以下所有操作都在此目录下进行。
   ```bash
   git clone --filter=blob:none git@github.com:ryanoasis/nerd-fonts.git
   ```

3. 将本项目 `scripts` 目录下的文件（不含`script`目录自身）拷贝过去。

5. 安装 `python` 环境（建议使用 [Miniconda](https://docs.anaconda.com/miniconda/) 配置虚拟环境）
   ```
   pip install fonttools
   ```

6. 建立 `sarasa` 目录，下载并解压[SarasaTermSC-TTF.7z](https://github.com/be5invis/Sarasa-Gothic/releases/download/v1.0.16/SarasaTermSC-TTF-1.0.16.7z)，并解压文件放入该目录中。

4. 安装`fontpatcher`
   ```
   wget https://github.com/ryanoasis/nerd-fonts/releases/latest/download/FontPatcher.zip
   unzip FontPatcher.zip && rm -rvf FontPatcher.zip
   ```

7. 修改 `font-patcher`, 其中第一行改为 `#!/usr/bin/python3`，这是因为 `fontforge` 相关绑定安装在系统的 Python
   中，而不是虚拟环境的 Python 中；

   找到 `# Define the character ranges` 一行，这里定义了一系列附加字符集，由于数量较多，直接和 Sarasa 字体合并
   会导致字符数量超出 65535 上限从而失败，因此需要根据需要删减一部分，删减方式为修改需要删减部分的 `SymStart`
   或者 `SymEnd`。本库中 release 的字体将 `Material` 的 `SymEnd` 改为了 `0xF1708`。

6. 运行脚本 `./build`，在 `sarasa-nerd`目录下将生成`.ttf`字体文件。同时，所有的
   `.ttf`也被打包成一个`.ttc`字体合集文件。
