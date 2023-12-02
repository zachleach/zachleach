## Windows shortcuts
- Copy selected text to clipboard: `Ctrl + C`
- Paste selected text to clipboard: `Ctrl + V`
- Copy selected text to clipboard and delete it: `Ctrl + X`
- Undo insertion/deletion: `Ctrl + Z`
- Cursor movement: `Ctrl`
   - Left one word: `Ctrl + Left Arrow`
   - Right one word: `Ctrl + Right Arrow`
   - Up one line: `Ctrl + Up Arrow`
   - Down one line: `Ctrl + Down Arrow`
- Text selection: `Ctrl + Shift`
   - Select entire box of text: `Ctrl + A`  
   - Cursor to the left one word: `Ctrl + Shift + Left Arrow` 
   - Cursor to the right one word: `Ctrl + Shift + Right Arrow`
   - Cursor up one line: `Ctrl + Shift + Up Arrow`
   - Cursor down one line: `Ctrl + Shift + Down Arrow`

## Google chrome shortcuts on Windows
- Swap between tabs: `Ctrl + [0..9]`
- Select text in search bar: `Ctrl + L`, `Alt + D`
  - Combo with typing a new search and pressing `Enter`
- Close current tab: `Ctrl + W`
  - Closes window if only one tab is open
- Open new tab: `Ctrl + T`
- Open new window: `Ctrl + N`
- Open new incognito window: `Ctrl + Shift + N`
- Duplicate current tab: `Alt + D` `Enter`

## ~/.bashrc
```bash
set -o vi
PS1="[\u@wsl]\w\n\$ "

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

## ~/.tmux.conf
```tmux
set -g default-terminal "${TERM}"
setw -g mode-keys vi
set -g escape-time 0
set -g status-right "#(TZ='America/Chicago' date '+%H:%M %Y.%m.%d')"

bind-key -n C-h select-pane -L
bind-key -n C-j select-pane -D
bind-key -n C-k select-pane -U
bind-key -n C-l select-pane -R

bind  %  split-window -h -c "#{pane_current_path}"
bind '"' split-window -v -c "#{pane_current_path}"
```

## ~/.vimrc
```vim
" Misc
set ttimeoutlen=0
set incsearch hlsearch
set clipboard=unnamedplus
set nocompatible
set nu rnu
set showmatch
set enc=utf-8 fenc=utf-8 termencoding=utf-8
set title ruler guioptions-=T
set nobackup nowritebackup noswapfile noundofile

" Coloration
set t_Co=16 bg=dark

" Command tab completion
set completeopt=menu,menuone,preview,noinsert
set wildmenu wildmode=list:longest,full

" Better `gf` navigation
set path+=~/notes suffixesadd+=.md
set hidden

" Syntax highlighting
filetype on
filetype plugin on
filetype indent on
syntax on

" Tabs/indentation/wrapping
set wrap lbr formatoptions-=t
set backspace=indent,eol,start
set autoindent tabstop=4 shiftwidth=4 softtabstop=4
au BufEnter * set fo-=cro
au FileType cpp set tabstop=8 shiftwidth=8 softtabstop=8
au FileType c set tabstop=8 shiftwidth=8 softtabstop=8

" C++ braces/multi-line comments
au filetype cpp inoremap {<CR> {<CR>}<ESC>ko
au filetype cpp inoremap /*<CR> /**/<left><left><CR><ESC>O<tab>

" Better scrolling/navigation
nnoremap <expr> { winheight(0)/4 . '<C-Y>'
nnoremap <expr> } winheight(0)/4 . '<C-E>'
nnoremap <expr> T 'zt' . winheight(0)/8 . '<C-Y>'
nnoremap H ^
vnoremap H ^
nnoremap L $
vnoremap L $
nnoremap K 5k
nnoremap J 5j
nnoremap j gj
nnoremap k gk

" Enable mouse scrolling
set mouse=a
map <ScrollWheelUp> 3<C-Y>
map <ScrollWheelDown> 3<C-E>

" Leader command shortcuts
let mapleader="\\"
nnoremap <leader>no :noh<CR>
nnoremap <leader>so :so $MYVIMRC<CR>
nnoremap <leader>qq :q!<CR>
nnoremap <leader>wq :wq<CR>
nnoremap <leader>wa :wa<CR>

" Open vimrc
nnoremap <F12> :w<CR><bar>:e $MYVIMRC<CR>
inoremap <F12> <ESC>:w<CR><bar>:e $MYVIMRC<CR>

" Save/quit
nnoremap <F4> :wq<CR>
inoremap <F4> <ESC>:wq<CR>
nnoremap <F2> :w<CR>
inoremap <F2> <ESC>:w<CR>

" Insert competitive programming template
autocmd filetype cpp nnoremap <F1> :%d<CR><bar>:-1read ~/.vim/cp.cpp<CR>:10<CR>
autocmd filetype cpp inoremap <F1> <ESC>:%d<CR><bar>:-1read ~/.vim/cp.cpp<CR>:10<CR>
autocmd filetype python nnoremap <F1> :%d<CR><bar>:-1read ~/.vim/cp.py<CR>:17<CR><end>
autocmd filetype python inoremap <F1> <ESC>:%d<CR><bar>:-1read ~/.vim/cp.py<CR>:17<CR>i<end>

" Compile/run
autocmd filetype cpp nnoremap <F9> :w <bar> !clear && g++ -std=c++17 -O2 -Wall % -o %:r && ./%:r.exe <CR>
autocmd filetype cpp inoremap <F9> <ESC>:w <bar> !clear && g++ -std=c++17 -O2 -Wall % -o %:r && ./%:r.exe <CR>
autocmd filetype c nnoremap <F9> :w <bar> !clear && gcc -Wall % -o %:r && ./%:r<CR>
autocmd filetype c inoremap <F9> <ESC>:w <bar> !clear && -Wall % -o %:r && ./%:r<CR>
autocmd filetype python nnoremap <F9> :w <bar> !clear && py %<CR>
autocmd filetype python inoremap <F9> <ESC>:w <bar> !clear && py %<CR>
```

## ~/.bash_aliases
```bash
alias cdwin="cd /mnt/c/Users/lacht/"
alias py="python3"
alias pip="pip3"

alias bashrc='vi ~/.bashrc'
alias vimrc='vi ~/.vimrc'
alias tmuxrc='vi ~/.tmux.conf'
alias aliases='vi ~/.bash_aliases'
alias sourcebash='source ~/.bashrc'
alias sourcetmux='tmux source-file ~/.tmux.conf'

alias gits='git status'
alias gitl='git log --oneline --graph --pretty'
alias gitaa='git add .'
alias gitau='git add -u'
alias gitai='git add -i'
alias gitc='git commit'
alias gitcp='git commit -m "$(date "+%Y-%m-%d %H:%M:%S")" && git push'
alias gitcpf='git commit -m "$(date "+%Y-%m-%d %H:%M:%S")" && git push -f'
alias gitp='git push'
alias gitpf='git push -f'
alias gitcl='git clean -fd'
alias gitacpf='git add . && git commit -m "$(date "+%Y-%m-%d %H:%M:%S")" && git push -f'
alias gitacp='git add . && git commit -m "$(date "+%Y-%m-%d %H:%M:%S")" && git push'

alias notes='cd ~/notes && vi +$(date +"%d") $(date +"%Y-%m-").md'
alias note='cd ~/notes && vi $(date +"%Y-%m-%d").md'
alias year='cd ~/notes && vi +$(date +"%m") $(date +"%Y-").md'
alias work='cd ~/notes && vi work.md'
```
