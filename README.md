# vimrc

This is my config file for vim with spf-13.

Here is the step to fellow me:
## 0. Prepare
In Ubuntu, some packages are needed to be installed to complie Vim.
```
sudo apt install libncurses5-dev python-dev perl libperl-dev ruby ruby-dev lua5.3 liblua5.3 liblua5.3-dev
```

Install oh-my-zsh:
if you need install it offline and locally, please make sure your zsh version is correct.  

Maybe deprecated in fulture (use with-lua-prefix instead). 
Some time,headers and shared library should be soft linked to correct location.
```
sudo ln -sf /usr/include/lua5.3/*.* /usr/include
sudo ln -s /usr/lib/x86_64-linux-gnu/liblua5.3.so /usr/lib/liblua.so
```

## 1. Install Vim
In ArchLinux, Install Vim with `sudo pacman -S gvim`

In Ubuntu, you need to complie Vim form source,when config you need to run this
```
./configure --with-features=huge --enable-pythoninterp --enable-rubyinterp --enable-luainterp --enable-perlinterp --with-python-config-dir=/usr/lib/python2.7/config/ --enable-gui=gtk2 --enable-cscope --enable-fail-if-missing
```
remmber to change the `with-pyton-config-dir`


if python3 is wanted: (recommanded, may be used in YCM)

```
./configure --with-features=huge --enable-rubyinterp --enable-luainterp --enable-perlinterp --enable-gui=gtk2 --enable-cscope --enable-fail-if-missing --with-lua-prefix=/usr/local/ --enable-python3interp vi_cv_path_python3=/Library/Frameworks/Python.framework/Versions/3.7/bin/python3 vi_cv_path_python3_pfx=/Library/Frameworks/Python.framework/Versions/3.7/

```
If you want to compile vim offline, you need to remove ./src/auto/config.cache firstly and config it by you environment.

## 2. Install my conig
1.  git clone https://github.com/DuCheng2018/vimrc.git
2.  run ./install.py in vimrc directory

## 3. Install the changed [spf-13](https://github.com/rxy0424/spf13-vim)
The spf-13 i forked control plugins with vim-plug,you can install this version by 
```
curl https://raw.githubusercontent.com/rxy0424/spf13-vim/feature/vim-plug/bootstrap.sh -L > spf13-vim.sh && sh spf13-vim.sh
```
If you want to install offline, it is neccessary to firstly comment out "do_back" and "sync_repo" commands in bootstrap.sh, 
and use existed .vim, .spf13-vim-3 and spf13-vim folders copied from others.

## 4. Complie YouCompleteMe.
if you use ArchLinux or Macos
```
sudo pacman -S python-pip clang
cd ~/.vim/bundle/YouCompleteMe
./install.py --clang-completer --system-libclang
```

if you use Ubuntu
```
cd ~/.vim/bundle/YouCompleteMe
./install.py --clang-completer
```

```
if you need to compile clang, please use following cmake config
cmake -G "Unix Makefiles"  \
 -DCMAKE_C_COMPILER=gcc \
 -DCMAKE_CXX_COMPILER=g++ \
 -DCMAKE_BUILD_TYPE=Release \
 -DCMAKE_INSTALL_PREFIX=/home/chengdu01/clang  \
 -DLLVM_TARGETS_TO_BUILD=all  \
 -DLLVM_INCLUDE_EXAMPLES=OFF  \
 -DLLVM_INCLUDE_TESTS=OFF  \
 -DLLVM_INCLUDE_GO_TESTS=OFF  \
 -DLLVM_INCLUDE_DOCS=OFF  \
 -DLLVM_ENABLE_TERMINFO=OFF  \
 -DLLVM_ENABLE_ZLIB=OFF  \
 -DLLVM_ENABLE_LIBEDIT=OFF  \
 -DLLVM_ENABLE_LIBXML2=OFF  \
  ../
(A release build implies LLVM_ENABLE_ASSERTIONS=OFF)
Please reference the python script downloaded from https://github.com/ycm-core/llvm/releases
```

## 5. Install tmux >= 2.1
install tmux >=2.1 and [oh-my-tmux](https://github.com/gpakosz/.tmux), you need xsel for copying to system clipboard,

If you use ubuntu install
```
sudo apt-get install libevent-dev automake
git clone https://github.com/tmux/tmux.git
cd tmux
sh autogen.sh
./configure && make
```

To install oh-my-tmux
```
cd
git clone https://github.com/gpakosz/.tmux.git
ln -s -f .tmux/.tmux.conf
```

To compline

## 6. Plugin in my config

### 6.1 fzf
`<ctrl-r>` in shell is updated by fzf, give it a try. 

`vim **<tab>` show file in pwd, `<ctrl-j>` for down and `<ctrl-j>` for up, `<tab>` for select, similar for ssh. Particular, `kill -9 <tab>` does need `**`

### 6.2 vim-dirvish
Under normal mode, `-` opens the current file directory

   `<CR>        `    Opens file at cursor.

   `{Visual}I   `

   `{Visual}<CR>`    Opens selected files.
   
   `o           `    Opens in horizontal split.

   `{Visual}O   `    Opens selected files in horizontal splits.

   `a           `    Opens in vertical split.

   `{Visual}A   `    Opens selected files in vertical splits.

   `K           `    Shows file info.

   `{Visual}K   `    Shows info about selected files.

   `p           `    Previews file at cursor.

   `CTRL-N      `    Previews the next file.

   `CTRL-P      `    Previews the previous file.

### 6.3 YouCompleteMe
`<leader>jc` jump to Declaration.

`<leader>jd` jump to Definition.

`<leader>ji` jump to include.

`<tab>` for select for completion, `<c-k>` for the previous one.

### 6.4 UltiSnips
`<c-e>` expand snips

`<c-j>` jump forward

`<c-k>` jump backward

### 6.5 LeaderfF

`<c-p>` list for files in project

`<leader>m` list for most recent used file

`<leader>f` list for functions in this file

`<leader>b` list for buffers in vim

`<leader>t` list for tags in this file

Once LeaderF is launched:

| Command                    | Description
| -------                    | -----------
| `<C-C>`<br>`<ESC>`         | quit from LeaderF
| `<C-R>`                    | switch between fuzzy search mode and regex mode
| `<C-F>`                    | switch between full path search mode and name only search mode
| `<Tab>`                    | switch to normal mode
| `<C-V>`<br>`<S-Insert>`    | paste from clipboard
| `<C-U>`                    | clear the prompt
| `<C-J>`<br>`<Down>`        | move the cursor downward in the result window
| `<C-K>`<br>`<Up>`          | move the cursor upward in the result window
| `<2-LeftMouse>`<br>`<CR>`  | open the file under cursor or selected(when multiple files are selected)
| `<C-X>`                    | open in horizontal split window
| `<C-]>`                    | open in vertical split window
| `<C-T>`                    | open in new tabpage
| `<F5>`                     | refresh the cache
| `<C-LeftMouse>`<br>`<C-S>` | select multiple files
| `<S-LeftMouse>`            | select consecutive multiple files
| `<C-A>`                    | select all files
| `<C-L>`                    | clear all selections
| `<BS>`                     | delete the preceding character in the prompt
| `<Del>`                    | delete the current character in the prompt
| `<Home>`                   | move the cursor to the begin of the prompt
| `<End>`                    | move the cursor to the end of the prompt
| `<Left>`                   | move the cursor one character to the left in the prompt
| `<Right>`                  | move the cursor one character to the right in the prompt
| `<C-P>`                    | preview the result

### 6.6 vim-gutentags

generate tags for you in project in ~/.cache/tags, and add it to tags path in vim

`ctags` is needed.

### 6.7 ctrlsf

`ripgrep` is needed for this plugin.

1. Run `:CtrlSF [pattern]`, it will split a new window to show search result.

2. If you are doing an asynchronous searching, you can explore and edit other files in the meanwhile, and can always press `Ctrl-C` to stop searching.

3. In the result window, press `Enter`/`o` to open corresponding file, or press `q` to quit.

4. Press `p` to explore file in a preview window if you only want a glance.

5. You can edit search result as you like. Whenever you apply a change, you can save your change to actual file by `:w`.

6. If you change your mind after saving, you can always undo it by pressing `u` and saving it again.

7. `:CtrlSFOpen` can reopen CtrlSF window when you have closed CtrlSF window. It is free because it won't invoke a same but new search. A handy command `:CtrlSFToggle` is also available.

8. If you prefer a quickfix-like result window, just try to press `M` in CtrlSF window.

## 7. Have fun
You are welcome to PR.

<!-- ## ATTENTION -->
<!-- Because of the version dependance config file for tmux, `bc` need to be installed. -->

