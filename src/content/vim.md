---
layout: post
title: "Configuring Vim"
author: Pranay Aryal
tags: ["Vim"]
image: img/testimg1.jpg
date: "2018-05-06T23:46:37.121Z"
draft: false
---

👋 Welcome, I can show you how to configure vim to make it look prettier and improve file browsing. You will also find tips on how to set up your .vimrc file plugins.vim file

1. Making Vim Prettier. Inside your .vim directory make a directory called "colors"
```shell
cd ~/.vim
mkdir colors
wget https://raw.githubusercontent.com/gosukiwi/vim-atom-dark/master/colors/atom-dark-256.vim
```

2. Your `.vimrc` file.
Paste <a href="https://gist.githubusercontent.com/pranayaryal/95cd000b91c7b841cbf0b63d82f7f588/raw/577817f3222f976642bdac9da2812c9497640869/new_gist_file_0" target="_blank">this code</a> in your .vimrc file


3. Then do
```bash
touch .vim/plugins.vim
```

4. Install a plugin manager like Vundle
```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

5. Then in your ~/.vim/plugins.vim file.
Paste <a href="https://gist.githubusercontent.com/pranayaryal/010cdee74b705092fb0b516fe880e472/raw/d1546ae6611e80e195d389859e5700effa24833f/new_gist_file_0" target="_blank" >this code</a> inside plugins.vim.
Then install the plugins using this command inside the ~/.vim/plugins.vim file
```shell
:PluginInstall
```
This should install all your plugins

6. Download ctags
Then type this in the project you want to be searchable. You might have to create a tags/ directory in your project
```shell
ctags -R
```
I hope this helps

