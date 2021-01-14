set nocompatible              " be iMproved, required
set ignorecase
filetype indent on
filetype off                  " required
set hidden                    " Without this option, whenever a changed buffer goes to "hidden". See: :h hidden
set diffopt+=vertical

set bs=2
" cursorline might not matter w/ Vim-airline on ?
set cursorline

" too confusing?
" set relativenumber

" Remove trailing whitespace on save
autocmd BufWritePre * %s/\s\+$//e

" Automatically source '~/.vimrc' whenever '~/.vimrc' is written to. This
" allows automagic updates whenever the config file is updated."
autocmd BufWritePost .vimrc source ~/.vimrc

set nowrap
set encoding=utf-8
set expandtab
set tabstop=4 softtabstop=4 shiftwidth=4
set hlsearch
set incsearch
set number
set noswapfile
set nobackup
set undodir=~/.vim/undodir
set undofile
"set ruler
set smartcase
set smartindent
set smarttab
set visualbell
set colorcolumn=80
set directory=/tmp

" Give more space for displaying messages.
" set cmdheight=2
set cmdheight=1

" Having longer updatetime (default is 4000 ms = 4 s) leads to noticeable
" delays and poor user experience.
set updatetime=50

set guifont=Fira\ Code:h20
colorscheme evening

call plug#begin('~/.vim/plugged')
Plug 'dhruvasagar/vim-table-mode'
Plug 'morhetz/gruvbox'
Plug 'tpope/vim-fugitive'
Plug 'vimlab/split-term.vim'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
Plug 'vimlab/split-term.vim'

" Neovim:
Plug 'pechorin/any-jump.vim'
Plug 'nvim-lua/diagnostic-nvim'
Plug 'neovim/nvim-lspconfig'
Plug 'nvim-lua/completion-nvim'
Plug 'tjdevries/lsp_extensions.nvim'
call plug#end()
lua require'nvim_lsp'.rust_analyzer.setup{ on_attach=require'completion'.on_attach }

colorscheme gruvbox
"if has('gui_running') && !empty(g:spacevim_guifont)
"endif

let mapleader = " "

"let g:airline_theme='base16_londontube'
"let g:airline_theme='base16'
"let g:airline_theme='nightowl'
let g:airline_theme='base16_solarized'
"Automatically displays all buffers when there's only one tab open.
let g:airline#extensions#tabline#enabled=1

nnoremap <leader>e :AnyJump<CR>
xnoremap <leader>e :AnyJumpVisual<CR>
" Normal mode: open previous opened file (after jump)
" nnoremap <leader>ab :AnyJumpBack<CR>
" Normal mode: open last closed search window again
" nnoremap <leader>al :AnyJumpLastResults<CR>

 " Sweet Sweet FuGITive
map <leader>gf :diffget //2<CR>
map <leader>gj :diffget //3<CR>
map <leader>gs :G<CR>

nmap <leader>h :wincmd h<CR>
nmap <leader>j :wincmd j<CR>
nmap <leader>k :wincmd k<CR>
nmap <leader>l :wincmd l<CR>

" TODO: look into https://github.com/dhruvasagar/vim-table-mode more
" Note: tdc deletes column - there's an add column too
noremap <silent> <leader>T :TableModeToggle<CR>
" To map <Esc> to exit terminal-mode:
tnoremap <Esc> <C-\><C-n>
noremap <silent> <leader>T :TableModeToggle<CR>

"map <C-x> :!pbc opy<CR>
"vmap <C-c> :w !pbcopy<CR><CR>
colorscheme gruvbox


" Set completeopt to have a better completion experience
" :help completeopt
" menuone: popup even when there's only one match
" noinsert: Do not insert text until a selection is made
" noselect: Do not select, force user to select one from the menu
set completeopt=menuone,noinsert,noselect

" Avoid showing extra messages when using completion
set shortmess+=c

" Configure LSP
" https://github.com/neovim/nvim-lspconfig#rust_analyzer
lua <<EOF

-- nvim_lsp object
local nvim_lsp = require'nvim_lsp'

-- function to attach completion and diagnostics
-- when setting up lsp
local on_attach = function(client)
    require'completion'.on_attach(client)
    require'diagnostic'.on_attach(client)
end

-- Enable rust_analyzer
nvim_lsp.rust_analyzer.setup({ on_attach=on_attach })

EOF

" Trigger completion with <Tab>
inoremap <silent><expr> <TAB>
  \ pumvisible() ? "\<C-n>" :
  \ <SID>check_back_space() ? "\<TAB>" :
  \ completion#trigger_completion()

function! s:check_back_space() abort
    let col = col('.') - 1
    return !col || getline('.')[col - 1]  =~ '\s'
endfunction
