# kid-vim-setting
Setup vim as an IDE

#vim程式開發環境設定
## Setup vim as an IDE
***

1. install ctags and cscope

    ```shell
        sudo apt-get install exuberant-ctags cscope
    ```
2. install plugin management tool -- Vundle

    ```shell
        git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
    ```
3. install fonts (optional)

    ```shell
        git clone https://github.com/powerline/fonts
        cd fonts && ./install.sh
    ```

    * install fonts if you would like to use airline plugin which requires some special characters to display status information.
    * 如果需要使用airline plugin，則必須安裝字型，以顯示特殊字元。

4. set ~/.vimrc

    * you can just copy my vim setting as follow; if you do so
        * modify the plugin list as needed
        * download the color schemes as needed <sup>[How-to](#myfootnote1)</sup>

    ```shell
        "=================================================================
        " 安裝相關軟體，Vundle和airline字型
        "=================================================================
        "sudo apt-get install exuberant-ctags cscope vim-gtk git
        "git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
        "git clone https://github.com/powerline/fonts
        "cd fonts && ./install.sh
        " 剪貼下面的文字並放到 ~/.vimrc

        "=================================================================
        " Start vundle
        "=================================================================
        set nocompatible              " be iMproved, required
        filetype off                  " required

        " set the runtime path to include Vundle and initialize
        set rtp+=~/.vim/bundle/Vundle.vim
        call vundle#begin()

        " alternatively, pass a path where Vundle should install plugins
        "call vundle#begin('~/some/path/here')

        " let Vundle manage Vundle, required
        Plugin 'VundleVim/Vundle.vim'

        "===============================================================
        " Write your plugins here
        "===============================================================
        " indent對齊參考線
        Plugin 'Yggdroot/indentLine'
        " 顯示行尾空白
        Plugin 'ntpeters/vim-better-whitespace'
        " 顯示狀態資訊 (包含git版本)
        "Plugin 'vim-airline/vim-airline'
        " 在vim中使用git命令
        "Plugin 'tpope/vim-fugitive'
        " 把cscope指令對應到hotkey
        Plugin 'chazy/cscope_maps'
        " 列出檔案中所有symbols，並可以跳至symbol處
        Plugin 'vim-scripts/taglist.vim'
        " 顯示目錄結構
        Plugin 'scrooloose/nerdtree'
        " 切割視窗列出function定義
        Plugin 'wesleyche/SrcExpl'
        " 控管SrcExpl, taglist, nerdtree視窗
        Plugin 'wesleyche/Trinity'
        " taglist加強
        Plugin 'majutsushi/tagbar'

        "================================================================
        " Run vundle
        "================================================================
        " All of your Plugins must be added before the following line
        call vundle#end()            " required
        filetype plugin indent on    " required
        " To ignore plugin indent changes, instead use:
        "filetype plugin on
        "
        " Brief help
        " :PluginList       - lists configured plugins
        " :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
        " :PluginSearch foo - searches for foo; append `!` to refresh local cache
        " :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
        "
        " see :h vundle for more details or wiki for FAQ
        " Put your non-Plugin stuff after this line

        "====================================================================
        " airline Settings 目前未安裝此plugin
        "===================================================================
        " 指定安裝的字型 (airline會需要一些特殊符號字型)
        set guifont=Inconsolata\ for\ Powerline\ 20
        "let g:airline_powerline_fonts = 1
        "set laststatus=2

        "====================================================================
        " Trinity Settings
        "====================================================================
        "Open/close the Tagbar separately
        nmap <F6> :TagbarToggle<CR>
        "Open/close the Source Explorer separately
        nmap <F7>  :TrinityToggleSourceExplorer<CR>
        "Open/close the Taglist separately
        nmap <F8> :TrinityToggleTagList<CR>
        "Open/close the NERDTree separately
        nmap <F9> :TrinityToggleNERDTree<CR>
        "Open/close SrcExpl, Taglist, Nerdtree
        nmap <F10>  :TrinityToggleAll<CR>

        "====================================================================
        " Editor Settings
        "====================================================================
        " 配色
        " using Molokai Color Scheme for Vim
        " from https://github.com/tomasr/molokai
        " set t_Co=256
        " colorscheme molokai

        " set solarized colorscheme
        " from https://https://github.com/altercation/vim-colors-solarized
        " syntax enable
        " set background=dark
        " set background=light
        " set t_Co=256
        " let g:solarized_termcolors=256
        " colorscheme solarized

        " set background=light
        " colorscheme wombat256mod

        set t_Co=256
        set background=dark
        colorscheme gruvbox

        " colorscheme jellybeans

        " 設定gvim 的字型和大小
        set guifont=inconsolata\ 20

        " highlight找到的字串
        set hlsearch

        " search時即時顯示結果
        set incsearch

        " highlight游標所在row
        set cursorline

        " 第80字元地方顯示高亮度區塊（這是連續兩個描述)
        set colorcolumn=80
        highlight ColorColumn guibg=#202020

        " 顯示行號
        set nu
        " 為方便複製，用<F2>開啟/關閉行號顯示
        nnoremap <F2> :set nonumber!<CR>

        " 顯示tab （這是連續兩個描述)
        set listchars=tab:\|.
        set list

        " 強制tab space為4個字元
        set tabstop=4

        " 使用space代替tab
        set expandtab

        " 當編寫Makefile時，取消expandtab設定 (Makefile需區分tab與space)
        autocmd FileType make setlocal noexpandtab

        " auto indent的移動字元量
        set shiftwidth=4

        " 設置自動縮進
        set autoindent

        " 使用C/C++ 語言的自動縮排方式：
        set cindent

        " 智能縮排
        set smartindent

        " 在狀態欄顯示正在輸入的命令
        set showcmd

        " 設置匹配模式，顯示匹配的括號
        set showmatch

        " 智能補全
        set completeopt=longest,menu

        " 括號/引號補全
        " :inoremap ( ()<ESC>i
        :inoremap {
             {
                 <CR>}<ESC>O
                     :inoremap [ []<ESC>i]]
             }
        }
    ```

    <a name="myfootnote1">How-to</a>:
    * [vim color scheme](http://www.vim.org/scripts/script_search_results.php?script_type=color+scheme)
    * [~/.vim/colorsbeta](http://vimcolors.com/)

5. install plugin
    * in vim normal mode

    ```shell
        :PluginInstall
    ```

6. and then you could:
    * Press &lt;F6&gt; to open/close Tagbar
    * Press &lt;F7&gt; to open/close SrcExpl
    * Press &lt;F8&gt; to open/close Taglist
    * Press &lt;F9&gt; to open/close NERDTree separately
    * Press &lt;F10>&gt; to open/close SrcExpl, Taglist, NERDTree at the same time
    * cscope hotkey:

        Press ```Ctrl``` + ```\``` with:
        * c: Find functions calling this function
        * d: Find functions called by this function
        * e: Find this egrep pattern
        * f: Find this file
        * g: Find this definition
        * i: Find files #including this file
        * s: Find this C symbol
        * t: Find this text string

* Chinese Ref:
   - [Trace C 程式碼的vim設定](http://wen00072.github.io/blog/2016/11/26/vim-setup-for-trace-c-code/)
