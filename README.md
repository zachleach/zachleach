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
alias coworkers='cd ~/notes && vi coworkers.md'
alias strangers='cd ~/notes && vi strangers.md'
alias family='cd ~/notes && vi family.md'
alias friends='cd ~/notes && vi friends.md'
alias l3h='cd ~/notes && vi l3harris.md'
alias csmc='cd ~/notes && vi csmc.md'

alias brucel='cd ~/notes && vi bruceleach.md'
alias sharonl='cd ~/notes && vi sharonleach.md'
alias cynthiac='cd ~/notes && vi cynthiacrowe.md'
alias andyc='cd ~/notes && vi andycrowe.md'
alias andrewl='cd ~/notes && vi andrewleach.md'
alias brycel='cd ~/notes && vi bryceleach.md'
alias brookel='cd ~/notes && vi brookeleach.md'
alias brendanl='cd ~/notes && vi brendanleach.md'
alias chrisl='cd ~/notes && vi chrisleach.md'
alias kennetha='cd ~/notes && vi kennethantilla.md'
alias kanishkg='cd ~/notes && vi kanishkgarg.md'
alias sashak='cd ~/notes && vi sashakaplan.md'
alias raiyyans='cd ~/notes && vi raiyyansiddiqui.md'
alias mitchc='cd ~/notes &wa& vi mitchellclark.md'
alias jordanf='cd ~/notes && vi jordanfrimpter.md'
alias dianal='cd ~/notes && vi dianale.md'
alias cynthiad='cd ~/notes && vi cynthiadiep.md'
alias joannak='cd ~/notes && vi joannak.md'
alias micahm='cd ~/notes && vi micahmatsuno.md'
alias hopec='cd ~/notes && vi hopecollins.md'
alias jeremeyc='cd ~/notes && vi jeremycoddington.md'
alias oomj='cd ~/notes && vi oomjonathan.md'
alias huntta='cd ~/notes && vi taylorhunt.md'
alias appenzj='cd ~/notes && vi joshappenzeller.md'
alias woodd='cd ~/notes && vi dentonwood.md'
alias jeromec='cd ~/notes && vi jeromecala.md'
alias brendanl='cd ~/notes && vi brendanlim.md'
alias laurenk='cd ~/notes && vi laurenkornblum.md'
alias anthoney='cd ~/notes && vi anthoney.md'
alias jasons='cd ~/notes && vi jasonsmith.md'
alias michaelu='cd ~/notes && vi michaelugochukwu.md'
alias virtuea='cd ~/notes && vi virtueadowei.md'
alias brianp='cd ~/notes && vi brianpham.md'
alias huyn='cd ~/notes && vi huynguyen.md'
alias josem='cd ~/notes && vi josemolina.md'
alias sethf='cd ~/notes && vi sethfriesen.md'
alias hannahe='cd ~/notes && vi hannaheason.md'
alias anandv='cd ~/notes && vi anand.md'
alias jayitam='cd ~/notes && vi vemuganti.md'
alias kumailb='cd ~/notes && vi kumail.md'
alias manishm='cd ~/notes && vi kumailbukhari.md'
alias michaelz='cd ~/notes && vi michaelzhao.md'
alias ninan='cd ~/notes && vi ninarao.md'
alias davidt='cd ~/notes && vi davidtepeneu.md'
```
