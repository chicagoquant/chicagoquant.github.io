
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

### Tagbar
```
if enabled_tagbar
  Plugin 'preservim/tagbar'

  nmap <F8> :TagbarToggle<CR>
  set tags=~/work/my-src/tags`
  " path to universal ctags
  let g:tagbar_ctags_bin = '~/my/bin/ctags'
endif
```

### Neoformat, does clang-format
```
" github.com/sbdchd/neoformat
let enabled_neoformat = 0
if enabled_neoformat
  Plugin 'sbdchd/neoformat'
  let g:neoformat_verbose = 1
  augroup fmt
    autocmd!
    autocmd BufWritePre *.h,*.c,*.cc,*.cpp,*.cxx undojoin | Neoformat clangformat
  augroup END
endif
```

### Clang format
```
if enabled_clang_format_vim
  function! ClangFormatOnSave()
    if !empty(findfile('.clang-format', '.;'))
      let l:formatdiff = 1 " only format lines that have changed
      py3f path-to/share/clang/clang-format.py
    endif
  endfunction
  augroup ClangFormatOnSave
    au!
    autocmd BufWritePre *.h,*.c,*.cc,*.cpp,*.cxx call ClangFormatOnSave()
  augroup END
endif
```

### YCM

see: [YCM Options Manual](https://ycm-core.github.io/YouCompleteMe/#options)
```
Plugin 'ycm-core/YouCompleteMe'

let g:ycm_global_ycm_extra_conf = 1
let g:ycm_extra_conf_globlist = ['~/work/.ycm_extra_conf.py']
let g:ycm_server_python_interpreter = 'path-to/bin/python3.11'

let g:ycm_use_clangd = 1
let g:ycm_clangd_binary_path = 'path-to/bin/clangd'
let g:ycm_clangd_args = ['--background-index', '--clang-tidy']

let g:ycm_enable_diagnostic_signs = 1
let g:ycm_autoclose_preview_window_after_completion = 1
let g:ycm_autoclose_preview_window_after_insertion = 1

let g:ycm_enable_semantic_highlighting = 1
let g:ycm_always_populate_location_list = 1

nnoremap <leader>gf :YcmCompleter Format<CR>
nnoremap <leader>gi :YcmCompleter GoToInclude<CR>
nnoremap <F12> :YcmCompleter GoToDefinitionElseDeclaration<CR>
nnoremap <F11> :YcmCompleter GoToCallers<CR>
nnoremap <F10> :YcmCompleter GoToReferences<CR>
nnoremap <F9> :YcmCompleter GoToDeclaration<CR>
nnoremap <leader>h :YcmCompleter GoToAlternateFile<CR>

let g:ycm_auto_hover = ''
nnoremap <leader>x <plug>(YCMHover)
nnoremap <F7> <plug>(YCMFindSymbolInWorkspace)

nnoremap <leader>yfw <plug>(YCMFindSymbolInWorkspace)
nnoremap <leader>yfd <plug>(YCMFindSymbolInDocument)
nnoremap <leader>yth <plug>(YCMTypeHierarchy)
nnoremap <leader>ych <plug>(YCMCallHierarchy)

"let g:ycm_auto_hover = 'CursorHold'    " after updatetime milliseconds, empty string to disable
"set updatetime=4000

"let g:ycm_server_python_interpreter = ''
"let g:ycm_global_ycm_extra_conf = ''
"let g:ycm_confirm_extra_conf = 1 " ask once per .ycm_extra_conf.py file if it is safe to be loaded
let g:ycm_extra_conf_globlist = ['~/work/*','!~/*']

"let g:ycm_use_ultisnips_completer = 0 " query the UltiSnips plugin for possible completions of snippet triggers
"let g:ycm_disable_for_files_larger_than_kb = 1000

"let g:ycm_use_clangd = 2
"let g:ycm_clangd_binary_path = ''
"let g:ycm_clangd_args = []
"let g:ycm_clangd_uses_ycmd_caching = 1 " Uses ycmd's caching and filtering logic
"let g:ycm_language_server = []
"let g:ycm_disable_signature_help = 1

" Enable debugging
let g:ycm_keep_logfiles = 1
let g:ycm_log_level = 'debug'
```

### Ripgrep
```
set grepprg=rg\ --vimgrep\ --smart-case\ --follow
set grepformat=%f:%l:%c:%m
nnoremap [q :cprev<CR>
nnoremap ]q :cnext<CR>
nnoremap <leader>co :copen<CR>
nnoremap <leader>cc :cclose<CR>
```

sample: `ycm_extra_conf.py`

```
# ~/work/blah-proj/.ycm_extra_conf.py
compilation_database_folder = ~/builds/blah-debug
```

```
cd ~/.vim/bundle/YouCompleteMe
python3.10 install.py \
  --build-dir /tmp/build-ycm \
  --clang-completer \
  --clangd-completer \
  --clang-tidy \
  --ninja \
  --verbose \

# cp -r /tmp/build-ycm/lib ~/.vim/bundle/YouCompleteMe/third_party/ycmd/third_party/clangd/cache
cp -r /tmp/build-ycm/lib ~/.vim/bundle/YouCompleteMe/third_party/ycmd/third_party/clang/lib

#  --system-libclang \
```
