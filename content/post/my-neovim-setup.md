---
title: "My Neovim Setup (Konfigurasi Neovim untuk Web Development)"
date: 2023-03-22T11:44:12+07:00
draft: false
weight: 1
categories: ["Programming"]
tags: ["Neovim"]
---

Konfigurasi ini kebanyakan saya mengambil contoh dari artikel yang di tulis oleh Takuya Matsuyama. Bisa sobat cek langsung [disini](https://dev.to/craftzdog/my-neovim-setup-for-react-typescript-tailwind-css-etc-58fb).

Hanya ada beberapa perubahan dan penambahan plugin oleh saya sendiri. Jadi konfigurasi neovim milik saya ini, tidak sepenuhnya dari ide saya pribadi. Terima kasih buat mas [Takuya Matsuyama](https://www.craftz.dog/) yang sudah membuat artikel tentang setup neovim, dimana saya sangat terbantu dengan tulisan tersebut.

## Apa saja yang dibutuhkan?

- Neovim [install](https://github.com/neovim/neovim/wiki/Installing-Neovim).
- Black Box (terminal linux) [install](https://gitlab.gnome.org/raggesilver/blackbox).
- Packer.nvim (plugin manager untuk neovim) [install](https://github.com/wbthomason/packer.nvim)
- Beberapa plugin lainnya

## Struktur direktori

Adapun struktur direktori yang saya gunakan adalah seperti berikut :

```
📂 ~/.config/nvim
├── 📁 after
│  └── 📁 plugin
├── 📂 lua
│  └── 🌑 base.lua
├── 📁 plugin
└── 🇻 init.lua
```

## Basic konfigurasi

Buat file baru bernama `base.lua` di `.config/nvim/lua/base.lua`.

```
vim.cmd('autocmd!')

vim.scriptencoding = 'utf-8'
vim.opt.encoding = 'utf-8'
vim.opt.fileencoding = 'utf-8'
vim.opt.termguicolors = true

vim.wo.number = true

vim.opt.title = true
vim.opt.autoindent = true
vim.opt.hlsearch = true
vim.opt.backup = false
vim.opt.showcmd = true
vim.opt.cmdheight = 1
vim.opt.laststatus = 2
vim.opt.expandtab = true
vim.opt.scrolloff = 10
vim.opt.shell = 'zsh'
vim.opt.backupskip = 'tmp/*,/private/tmp/*'
vim.opt.inccommand = 'split'
vim.opt.ignorecase = true
vim.opt.smarttab = true
vim.opt.breakindent = true
vim.opt.shiftwidth = 2
vim.opt.tabstop = 2
vim.opt.ai = true -- Auto indent
vim.opt.si = true -- Smart indent
vim.opt.wrap = false -- No wrap lines
vim.opt.backspace = 'start,eol,indent'
vim.opt.path:append { '**' } -- Finding files - seacrh down in subfolders
vim.opt.wildignore:append { '*/node_modules/*' }

-- Turn of paste mode when leaving insert
vim.api.nvim_create_autocmd("InsertLeave", {
  pattern = '*',
  command = "set nopaste"
})

-- Add asteris in block comments
vim.opt.formatoptions:append { 'r' }
```

Buat file `highlights.lua` (untuk cursor line) di `.config/nvim/lua/highlights.lua`.

```
vim.opt.cursorline = true
vim.opt.termguicolors = true
vim.opt.winblend = 0
vim.opt.wildoptions = 'pum'
vim.opt.pumblend = 5
vim.opt.background = 'dark'
```

Buat file `maps.lua` di `.config/nvim/lua/maps.lua`.

```
local keymap = vim.keymap

-- Do not yank with x
keymap.set('n', 'x', '"_x')

-- Increment/Decrement
keymap.set('n', '+', '<C-a>')
keymap.set('n', '-', '<C-x>')

-- Delete a word backwards
keymap.set('n','dw', 'vb"_d')

-- Select all
keymap.set('n', '<C-a>', 'gg<S-v>G')

-- New tab
keymap.set('n', 'te', ':tabedit<Return>', { silent = true })
-- Split window
keymap.set('n', 'ss', ':split<Return><C-w>w', { silent = true })
keymap.set('n', 'sv', ':vsplit<Return><C-w>w', { silent = true })
-- Move window
keymap.set('n', '<Space>', '<C-w>w')
keymap.set('', 's<left>', '<C-w>h')
keymap.set('', 's<up>', '<C-w>k')
keymap.set('', 's<down>', '<C-w>j')
keymap.set('', 's<right>', '<C-w>l')
keymap.set('', 'sh', '<C-w>h')
keymap.set('', 'sk', '<C-w>k')
keymap.set('', 'sj', '<C-w>j')
keymap.set('', 'sl', '<C-w>l')

-- Resize window
keymap.set('n', '<C-w><left>', '<C-w><')
keymap.set('n', '<C-w><right>', '<C-w>>')
keymap.set('n', '<C-w><up>', '<C-w>+')
keymap.set('n', '<C-w><down>', '<C-w>-')
```

Kemudian buat file `init.lua` di `.config/nvim/init.lua` untuk me-load pengaturan yang sudah dibuat (diatas) agar dapat bekerja di neovim.

```
require('base')
require('maps')
require('highlights')
require('plugins')
```

