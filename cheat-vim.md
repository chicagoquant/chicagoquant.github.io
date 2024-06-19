
# VIM config

## Linux VIMRC

```
set wrap
set ai
set ts=4
set sw=4
set ic
set expandtab
set viminfofile=NONE
set nobackup
set nowritebackup
set noswapfile
set nostartofline
set hlsearch
set belloff=all
syntax off
set cursorline

iabbrev zzpy def main(args):<CR>    if args.input_file:<CR>    pass<CR><C-d><CR><CR><C-d>if __name__ == "__main__":<CR>    import argparse<CR>p = argparse.ArgumentParser()<CR>p.add_argument("-i")<CR>args = p.parse_args()<CR><CR>main(args)
iabbrev zzcpp #include <iostream><CR>#include <vector><CR>#include <string><CR>#include <algorithm><CR>#include <functional><CR>#include <chrono><CR><CR>using namespace std;<CR><CR>int main(int argc, const char* argv[])<CR>{<CR>    std::cout << "Hello world!" << std::endl;<CR><C-d>}
```

## Windows VIMRC
```
" ~/.vimrc
filetype off
set shellslash
set rtp+=~/vimfiles/bundle/Vundle.vim
call vundle#begin('~/vimfiles/bundle')

Plugin 'VundleVim/Vundle.vim'     " let Vundle manage Vundle, required
Plugin 'junegunn/fzf'
Plugin 'junegunn/fzf.vim'
Plugin 'scrooloose/nerdtree'
Plugin 'mattn/emmet-vim'
Plugin 'bling/vim-airline'

" All of your Plugins must be added before the following line, i.e. between vundle#begin and vundle#end
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

set nowrap
set ai
set ts=4
set sw=4
set ic
set expandtab
"set $HOME="C:\\Users\\$USERNAME"         " HOMEPATH | USERPROFILE
"set $HOMEDRIVE="C:"
set viminfofile=NONE
set nobackup
set nowritebackup
set noswapfile
set nostartofline
set hlsearch
set belloff=all
set lines=50 columns=120
"set guifont=Lucida_Console:h9:cANSI:qDRAFT   " default?
set guifont=Courier_New:h14:cANSI:qDRAFT
syntax on
set cursorline

" NerdTree Begin
"nnoremap <leader>n :NERDTreeFocus<CR>
"nnoremap <C-n> :NERDTree<CR>
"nnoremap <C-t> :NERDTreeToggle<CR>
"nnoremap <C-f> :NERDTreeFind<CR>
" NerdTree End

" Emmet Begin
let g:user_emmet_mode='n'    "only enable normal mode functions.
let g:user_emmet_mode='inv'  "enable all functions, which is equal to
let g:user_emmet_mode='a'    "enable all function in all mode.

" only enable Emmet for certain file types
let g:user_emmet_install_global = 0
autocmd FileType html,css EmmetInstall

" redefine the trigger key (you still need to enter the trailing ,)
let g:user_emmet_mode='a'
" let g:user_emmet_install_global=0
" autocmd FileType html,css EmmetInstall
let g:user_emmet_leader_key='<C-Z>'
" Emmet End
```

## Useful plugins

Neoformat, does clang-format