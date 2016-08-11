---
layout: post
title: "Sharing My .vimrc"
location: "Japan"
categories: ["Code"]
comments: true
---

Vim has always been my go to editor/IDE when Im outside of Visual Studio. Heres my base `_vimrc` for Windows.

{% highlight conf %}
set wrap
set fileencodings=utf-8
set nocompatible
set noswapfile
set shortmess+=I
set ignorecase
set rtp+=$HOME/vimfiles/bundle/Vundle.vim/
set guioptions-=T
set guioptions-=r
set guioptions-=m
set splitright
set splitbelow
set ruler
call vundle#begin('$USERPROFILE/vimfiles/bundle/')
Plugin 'VundleVim/Vundle.vim'
Plugin 'fatih/vim-go'
Plugin 'PProvost/vim-ps1'
call vundle#end()
filetype plugin indent on
" To ignore plugin indent changes, instead use:
" filetype plugin on
" let g:netrw_liststyle=3

" Enable powershell syntax plug
autocmd BufNewFile,BufReadPost *.ps1 set filetype=ps1

" Search for the word under cursor in the current dir (recursively)
command CSM :execute "vimgrep /" . expand("<cword>") . "/j ** <Bar> :cw"
nnoremap <leader>ms :CSM<CR>

" Simple mappings for window manipulations
nnoremap <leader>wq <C-W>q
nnoremap <leader><left><left> <C-W><left>
nnoremap <leader><right><right> <C-W><right>
nnoremap <leader><up><up> <C-W><up>
nnoremap <leader><down><down> <C-W><down>

nnoremap <leader>b :ls<CR>:
nnoremap <leader>s :w<CR>
{% endhighlight %}

And heres my base `.vimrc` for Linux and OSX.

{% highlight conf %}
let mapleader = " "

filetype off
syntax on
colorscheme elflord
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
Plugin 'Valloric/YouCompleteMe'
Plugin 'jelera/vim-javascript-syntax'
Plugin 'fatih/vim-go'
Plugin 'majutsushi/tagbar'
call vundle#end()
filetype plugin indent on

" Save marks to up to 100 files, save global marks as well (f1). To disable, f0
set viminfo='100,f1

set tabstop=4
set shiftwidth=4
set softtabstop=4
set expandtab
set autoindent
set nu
set encoding=utf-8
set noswapfile
set shortmess+=I
set backspace=2
set nocompatible
set ignorecase
set splitright
set splitbelow
set ruler
" Temporary enable/disable YouCompleteMe. Active = disable, commented = enable
" let g:loaded_youcompleteme = 1
let g:ycm_global_ycm_extra_conf = "~/.ycm_extra_conf.py"
let g:ycm_disable_for_files_larger_than_kb = 0
let g:ycm_autoclose_preview_window_after_completion = 1

" Options for netrw
let g:netrw_liststyle = 0
let g:netrw_altv = 1

" 1. :PluginInstall
" 2. :GoInstallBinaries (gotags, vim-go)
" 3. Install 'ctags'
" 4. go get -u github.com/jstemmer/gotags
let g:tagbar_type_go = {
    \ 'ctagstype' : 'go',
    \ 'kinds'     : [
        \ 'p:package',
        \ 'i:imports:1',
        \ 'c:constants',
        \ 'v:variables',
        \ 't:types',
        \ 'n:interfaces',
        \ 'w:fields',
        \ 'e:embedded',
        \ 'm:methods',
        \ 'r:constructor',
        \ 'f:functions'
    \ ],
    \ 'sro' : '.',
    \ 'kind2scope' : {
        \ 't' : 'ctype',
        \ 'n' : 'ntype'
    \ },
    \ 'scope2kind' : {
        \ 'ctype' : 't',
        \ 'ntype' : 'n'
    \ },
    \ 'ctagsbin'  : 'gotags',
    \ 'ctagsargs' : '-sort -silent'
\ }

nnoremap <F8> :TagbarToggle<CR>

" Search for the word under cursor in the current dir (recursively)
command CSM execute ":vimgrep /" . expand("<cword>") . "/j ** <Bar> :cw"
nnoremap <leader>ms :CSM<CR>
set wildignore+=jennah

" Simple mappings for window manipulations
nnoremap <leader>wq <C-W>q
nnoremap <leader>ws <C-W>s
nnoremap <leader>wv <C-W>v
nnoremap <leader><left><left> <C-W><left>
nnoremap <leader><right><right> <C-W><right>
nnoremap <leader><up><up> <C-W><up>
nnoremap <leader><down><down> <C-W><down>

" Display buffers, then prep the colon for the next command
nnoremap <leader>b :ls<CR>:

" Shortcut for save
nnoremap <leader>s :w<CR>
{% endhighlight %}
