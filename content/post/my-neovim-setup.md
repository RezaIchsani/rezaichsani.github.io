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

## 

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

## 

## Install packer.nvim (plugin manager)

Unix, Linux instalation

```
git clone --depth 1 https://github.com/wbthomason/packer.nvim\
 ~/.local/share/nvim/site/pack/packer/start/packer.nvim
```

Lalu buat file `plugins.lua` di `.config/nvim/lua/plugins.lua`.

```
local status, packer = pcall(require, 'packer')
if (not status) then return end

vim.cmd [[packadd packer.nvim]]
return require('packer').startup(function(use)
  -- Packer can manage itself
  use 'wbthomason/packer.nvim'

  -- Plugin lainnya di install disini

end)
```

`:PackerInstall` atau `:PackerSync` untuk menginstall packer di neovim.



## Install tema (onedark.nvim)

Tema yang saya gunakan untuk neovim saya adalah [onedark.nvim](https://github.com/navarasu/onedark.nvim). Sobat bisa menggunakan tema yang lain sesuai selera sobat.

```
use 'navarasu/onedark.nvim'
```

Lalu buat file konfigurasinya `onedark.rc.lua` di `.config/nvim/after/plugin/onedark.rc.lua` dengan script berikut :

```
local status, onedark = pcall(require, 'onedark')
if (not status) then return end

require('onedark').setup {
  style = 'cool', -- Choose one 'dark', 'darker', 'cool', 'deep', 'warm', 'warmer' and 'light'
  transparent = true,
  term_colors = true,
  ending_tildes = false,        -- Show the end-of-buffer tildes.
  cmp_itemkind_reverse = false, -- reverse item kind highlight in cmp menu

  code_style = {
    comments = 'italic',
    keywords = 'none',
    functions = 'none',
    strings = 'none',
    variables = 'none'
  },

  -- Plugins Config
  diagnostics = {
    darker = true,
    undercurl = true,
    background = true,
  },
}

-- Enable theme
require('onedark').load()
```



## Install lualine (status line)

Lualine.nvim mirip seperti vim airline di vim. install [lualine.nvim](https://github.com/nvim-lualine/lualine.nvim) dengan packer.

```
use 'nvim-lualine/lualine.nvim'
```

Install juga [nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons) untuk icons.

```
use 'nvim-tree/nvim-web-devicons'
```

Buat file konfigurasi untuk lualine dan nvim-web-devicons di `.config/nvim/after/plugin`

**lualine.rc.lua** :

```
local status, lualine = pcall(require, 'lualine')
if (not status) then return end

require('lualine').setup {
  options = {
    icons_enabled = true,
    theme = 'solarized_dark',
    component_separators = { left = '', right = ''},
    section_separators = { left = '', right = ''},
    disabled_filetypes = {
      statusline = {},
      winbar = {},
    },
    ignore_focus = {},
    always_divide_middle = true,
    globalstatus = false,
    refresh = {
      statusline = 1000,
      tabline = 1000,
      winbar = 1000,
    }
  },
  sections = {
    lualine_a = {'mode'},
    lualine_b = {'branch', 'diff', 'diagnostics'},
    lualine_c = {'filename'},
    lualine_x = {
    { 
      'diagnostics',
      sources = { 'nvim_diagnostic' },
      symbols = {error = 'E', warn = 'W', info = 'I', hint = 'H'},
    },
      'encoding', 'fileformat', 'filetype'
    },
    lualine_y = {'progress'},
    lualine_z = {'location'}
  },
  inactive_sections = {
    lualine_a = {},
    lualine_b = {},
    lualine_c = {'filename'},
    lualine_x = {'location'},
    lualine_y = {},
    lualine_z = {}
  },
  tabline = {},
  winbar = {},
  inactive_winbar = {},
  extensions = {}
}

```

**nvim-web-devicons.rc.lua** :

```
local status, icons = pcall(require, 'nvim-web-devicons')
if (not status) then return end

icons.setup {
  override = {},
  default = true
}

```



## Install lspconfig

Install [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) dengan packer :

```
use 'neovim/nvim-lspconfig'
```

Buat file konfigurasi `lspconfig.rc.lua` di `.config/nvim/plugins/lspconfig.rc.lua` :

```
local status, nvim_lsp = pcall(require, 'lspconfig')
if (not status) then return end

local protocol = require('vim.lsp.protocol')

local on_attach = function(client, bufnr)
  -- Format on save
  if client.server_capabilities.documentFormattingProvider then
    vim.api.nvim_command [[augroup Format]]
    vim.api.nvim_command [[autocmd! * <buffer>]]
    vim.api.nvim_command [[autocmd BufWritePre <buffer> lua vim.lsp.buf.format()]]
    vim.api.nvim_command [[augroup END]]
  end
end

-- TypeScript & JavaScript configuration
nvim_lsp.tsserver.setup {
  on_attach = on_attach,
  cmd = { "typescript-language-server", "--stdio" },
  filetypes = { "javascript", "javascriptreact", "javascript.jsx", "typescript", "typescriptreact", "typescript.tsx" }
}

-- Lua configuration
nvim_lsp.lua_ls.setup {
  on_attach = on_attach,
  settings = {
    Lua = {
      diagnostics = {
        -- Get the language server to recognize the 'vim' global
        globals = { 'vim'}
      },

      workspace = {
        -- Make the server aware of Neovim runtime files
        library = vim.api.nvim_get_runtime_file("", true),
        checkThirdParty = false
      }
    }
  }
}

```



## Install lspkind & cmp

```
  use 'onsails/lspkind-nvim' -- vscode-like pictograms
  use 'hrsh7th/cmp-buffer'   -- nvim-cmp source for buffer words
  use 'hrsh7th/cmp-nvim-lsp' -- nvim-cmp source for neovim's built-in LSP
  use 'hrsh7th/nvim-cmp'     -- Completion

```

Buat file `lspkind.rc.lua` dan `cmp.rc.lua` di `.config/nvim/after/plugin/`.

**lspkind.rc.lua**

```
require('lspkind').init({
    -- DEPRECATED (use mode instead): enables text annotations
    --
    -- default: true
    -- with_text = true,

    -- defines how annotations are shown
    -- default: symbol
    -- options: 'text', 'text_symbol', 'symbol_text', 'symbol'
    mode = 'symbol_text',

    -- default symbol map
    -- can be either 'default' (requires nerd-fonts font) or
    -- 'codicons' for codicon preset (requires vscode-codicons font)
    --
    -- default: 'default'
    preset = 'codicons',

    -- override preset symbols
    --
    -- default: {}
    symbol_map = {
      Text = "",
      Method = "",
      Function = "",
      Constructor = "",
      Field = "ﰠ",
      Variable = "",
      Class = "ﴯ",
      Interface = "",
      Module = "",
      Property = "ﰠ",
      Unit = "塞",
      Value = "",
      Enum = "",
      Keyword = "",
      Snippet = "",
      Color = "",
      File = "",
      Reference = "",
      Folder = "",
      EnumMember = "",
      Constant = "",
      Struct = "פּ",
      Event = "",
      Operator = "",
      TypeParameter = ""
    },
})

```

**cmp.rc.lua**

```
local status, cmp = pcall(require, 'cmp')
if (not status) then return end
local lspkind = require 'lspkind'

cmp.setup ({
  snippet = {
    expand = function(args)
      require('luasnip').lsp_expand(args.body)
    end,
  },
  mapping = cmp.mapping.preset.insert({
    ['<C-d>'] = cmp.mapping.scroll_docs(-4),
    ['<C-f>'] = cmp.mapping.scroll_docs(4),
    ['<C-Space>'] = cmp.mapping.complete(),
    ['<C-e>'] = cmp.mapping.close(),
    ['<CR>'] = cmp.mapping.confirm({
      behavior = cmp.ConfirmBehavior.Replace,
      select = true
    }),
  }),
  sources = cmp.config.sources({
    { name = 'nvim_lsp' },
    { name = 'buffer' },
  }),
  formatting = {
    format = lspkind.cmp_format({ with_text = false, maxwidth = 50 })
  }
})

vim.cmd [[
  set completeopt=menuone,noinsert,noselect
  highlight! default link CmpItemKind CmpItemMenuDefault
]]
```

Kemudian install `luasnip` agar konfigurasi diatas dapat berjalan dengan normal.

```
use 'L3MON4D3/LuaSnip'
```



## Install ts-autotag & autopairs

```
use 'windwp/nvim-ts-autotag'
use 'windwp/nvim-autopairs'
```

Buat file konfigurasi di `.config/nvim/after/plugin/` dengan nama `ts-autotag.rc.lua` dan `autopairs.rc.lua`.

**ts-autotag.rc.lua**

```
local status, autotag = pcall(require, 'nvim-ts-autotag')
if (not status) then return end

autotag.setup({})
```

**autopairs.rc.lua**

```
local status, autopairs = pcall(require, 'nvim-autopairs')
if (not status) then return end

autopairs.setup({
  disable_filetype = { 'TelescopePrompt', 'vim' },
})
```



## Install treesitter

```
use {
    'nvim-treesitter/nvim-treesitter',
    run = ':TSUpdate'
  }
```

Buat file `treesitter.rc.lua` di `.config/nvim/after/plugin/`.

```
local status, ts = pcall(require, 'nvim-treesitter.configs')
if (not status) then return end

ts.setup {
  highlight = {
    enable = true,
    disable = {},
  },
  indent = {
    enable = true,
    disable = {},
  },
  ensure_installed = {
    'tsx',
    'toml',
    'fish',
    'php',
    'json',
    'yaml',
    'swift',
    'css',
    'html',
    'lua'
  },
  autotag = {
    enable = true,
  },
}

local parser_config = require "nvim-treesitter.parsers".get_parser_configs()
parser_config.tsx.filetype_to_parsername = { "javascript", "typescript.tsx" }
```



## Install telescope (fuzzy finder)

```
use 'nvim-lua/plenary.nvim'
use 'nvim-telescope/telescope.nvim'
use 'nvim-telescope/telescope-file-browser.nvim'
```

Buat file `telescope.rc.lua` di `.config/nvim/after/plugin/`.

```
local status, telescope = pcall(require, 'telescope')
if (not status) then return end

local actions = require('telescope.actions')

function telescope_buffer_dir()
  return vim.fn.expand('%:p:h')
end

local fb_actions = require 'telescope'.extensions.file_browser.actions

telescope.setup {
  defaults = {
    mappings = {
      n = {
        ['q'] = actions.close
      }
    }
  },
  extensions = {
    file_browser = {
      theme = 'dropdown',
      -- disables netrw add use telescope-file-browser in its place
      hijack_netrw = true,
      mappings = {
        -- your custome insert mode mappings
        ['i'] = {
          ['<C-w>'] = function() vim.cmd('normal vbd') end,
        },
        ['n'] = {
          ['N'] = fb_actions.create,
          ['h'] = fb_actions.goto_parent_dir,
          ['/'] = function()
            vim.cmd('startinsert')
          end
        }
      }
    }
  }
}

telescope.load_extension('file_browser')

local opts = { noremap = true, silent = true }
vim.keymap.set('n', ';f', '<cmd>lua require("telescope.builtin").find_files({ no_ignore = false, hidden = true })<cr>',
  opts)
vim.keymap.set('n', ';r', '<cmd>lua require("telescope.builtin").live_grep()<cr>',
  opts)
vim.keymap.set('n', '\\\\', '<cmd>lua require("telescope.builtin").buffers()<cr>',
  opts)
vim.keymap.set('n', ';t', '<cmd>lua require("telescope.builtin").help_tags()<cr>',
  opts)
vim.keymap.set('n', ';;', '<cmd>lua require("telescope.builtin").resume()<cr>',
  opts)
vim.keymap.set('n', ';e', '<cmd>lua require("telescope.builtin").diagnostics()<cr>',
  opts)
vim.keymap.set('n', 'sf', '<cmd>lua require("telescope").extensions.file_browser.file_browser({ path = "%:p:h", cwd = telescope_buffer_dir(), respect_git_ignore = false, hidden = true, grouped = true, previewer = false, initial_mode = "normal", layout_config = { height = 40 } } )<cr>',
  opts)
```



## Install bufferline (tab)

```
use 'akinsho/bufferline.nvim'
```

Buat file `bufferline.rc.lua` di `.config/nvim/after/plugin/`.

```
local status, bufferline = pcall(require, 'bufferline')
if (not status) then return end

require('bufferline').setup ({
  options = {
    mode = 'tabs',
    separator_style = 'slant',
    always_show_bufferline = false,
    show_buffer_close_icons = true,
    show_close_icon = true,
    color_icons = true
  },
  highlights = {
    separator_selected = {
      fg = '#525252',
    },
    separator_visible = {
      fg = '#073642',
    },
    separator = {
      fg = '#525252',
    },
    background = {
      fg = '#657b83',
    },
    buffer_selected = {
      fg = '#fdf6e3',
      bold = true,
      underline = false,
    },
    fill = {
      bg = '#1d2d50',
      --bg = '#073643',
    },
  },
})

vim.keymap.set('n', '<Tab>', '<Cmd>BufferLineCycleNext<CR>', {})
vim.keymap.set('n', '<S-Tab>', '<Cmd>BufferLineCyclePrev<CR>', {})
```

## Install nvim-colorizer

```
use 'norcalli/nvim-colorizer.lua'
```

Buat file `colorizer.rc.lua` di `.config/nvim/after/plugin/`.

```
local status, colorizer = pcall(require, 'colorizer')
if (not status) then return end

colorizer.setup {
  '*';
}
```

## Install lspsaga

```
use 'glepnir/lspsaga.nvim'
```

Buat file `lspsaga.rc.lua` di `.config/nvim/plugins/lspsaga.rc.lua`.

```
local status, lspsaga = pcall(require, 'lspsaga')
if (not status) then return end

--require('lspsaga').setup({})
lspsaga.setup {
  server_filetype_map = {
    typescript = 'typescript'
  }
}

local opts = { noremap = true, silent = true }
vim.keymap.set('n', '<C-j>', '<Cmd>Lspsaga diagnostic_jump_netx<CR>', opts)
vim.keymap.set('n', 'K', '<Cmd>Lspsaga hover_doc<CR>', opts)
vim.keymap.set('n', 'gd', '<Cmd>Lspsaga lsp_finder<CR>', opts)
vim.keymap.set('i', '<C-k>', '<Cmd>Lspsaga signature_help<CR>', opts)
vim.keymap.set('n', 'gp', '<Cmd>Lspsaga preview_definition<CR>', opts)
vim.keymap.set('n', 'gr', '<Cmd>Lspsaga rename<CR>', opts)
```

## Install prettier & null-ls

Pertama install [prettierd](https://github.com/fsouza/prettierd) terlebih dahulu menggunakan npm ataupun homebrew.

```
npm install -g @fsouza/prettierd
```
```
brew install fsouza/prettierd/prettierd
```

Kemudian install prettier dan null-ls dengan packer.

```
  use 'jose-elias-alvarez/null-ls.nvim'
  use 'MunifTanjim/prettier.nvim' 
```

Buat file `null-ls.rc.lua` dan `prettier.rc.lua`.

**null-ls.rc.lua** :

```
local status, null_ls = pcall(require, 'null_ls')
if (not status) then return end

null_ls.setup({
  on_attach = function(client, bufnr)
    if client.server_capabilities.documentFormattingProvider then
      vim.api.nvim_command [[augroup Format]]
      vim.api.nvim_command [[autocmd! * <buffer>]]
      vim.api.nvim_command [[autocmd BufWritePre <buffer> lua vim.lsp.buf.format()]]
      vim.api.nvim_command [[augroup END]]
    end
  end,
  sources = {
    null_ls.builtins.diagnostics.eslint_d.with({
      diagnostics_format = '[eslint] #{m}\n(#{c})'
    }),
    null_ls.builtins.diagnostics.fish
  }
})
```

**prettier.rc.lua** :

```
local status, prettier = pcall(require, 'prettier')
if (not status) then return end

prettier.setup {
  bin = 'prettierd',
  filetypes = {
    'html',
    'css',
    'javascript',
    'javascriptreact',
    'typescript',
    'typescriptreact',
    'json',
    'scss',
    'less'
  }
}
```

## Install gitsigns

```
use 'lewis6991/gitsigns.nvim'
```

Buat file `gitsigns.rc.lua` di `.config/nvim/after/plugin/gitsigns.rc.lua`.

```
local status, gitsigns = pcall(require, 'gitsigns')
if (not status) then return end

require('gitsigns').setup{
  signs = {
    add          = { text = '│' },
    change       = { text = '│' },
    delete       = { text = '_' },
    topdelete    = { text = '‾' },
    changedelete = { text = '~' },
    untracked    = { text = '┆' },
  },
}
```

## Install git

```
use 'dinhhuy258/git.nvim'
```

Buat file `git.rc.lua` di `.config/nvim/after/plugin/git.rc.lua`.

```
local status, git = pcall(require, 'git')
if (not status) then return end

git.setup({
  keymaps = {
    -- Open blame window
    blame = '<Leader>gb',
    -- Open file/folder in git repository
    browse = '<Leader>go',
  }
})
```

## Install mason (portable package manager)

```
use 'williamboman/mason.nvim'
use 'williamboman/mason-lspconfig.nvim'
```

Buat file `mason.rc.lua` di `.config/nvim/after/plugin/mason.rc.lua`.

```
local status, mason = pcall(require, 'mason')
if (not status) then return end
local status2, lspconfig = pcall(require, 'mason-lspconfig')
if (not status) then return end

mason.setup({

})

lspconfig.setup {
  ensure_installed = { 'tailwindcss' },
}
```

Yaps.. sampai disini, semua plugin untuk kebutuhan web development sudah terinstall semua.

Berikut ini adalah beberapa plugin tambahan yang saya tambah agar semakin lengkap.

## Neotree

```
use {
  'nvim-neo-tree/neo-tree.nvim',
  branch = 'v2.x',
  requires = {
    'MunifTanjim/nui.nvim',
  }
}
```

Buat file `neo-tree.rc.lua` di `.config/nvim/after/plugin/neo-tree.rc.lua`.

```
local status, neotree = pcall(require, 'neo-tree')
if (not status) then return end

require('neo-tree').setup({
  default_component_configs = {
    container = {
      enable_character_fade = true
    },
    indent = {
      indent_size = 2,
      padding = 1, --extra padding on left hand side
      -- indent guides
      with_markers = true,
      indent_marker = '│',
      last_indent_marker = '└',
      highlight = 'NeoTreeIndentMarker',
      -- expander config, needed for nesting file
      with_expanders = 1,
      expander_collapsed = "",
      expander_expanded = "",
      expander_highlight = "NeoTreeExpander",
    },
    icon = {
      folder_closed = "",
      folder_open = "",
      folder_empty = "ﰊ",
      default = "*",
      highlight = "NeoTreeFileIcon"
    },
    modified = {
      symbol = "[+]",
      highlight = "NeoTreeModified",
    },
    name = {
      trailing_slash = false,
      use_git_status_colors = true,
      highlight = "NeoTreeFileName",
    },
    git_status = {
      symbols = {
        -- Change type
        added     = '✚',
        modified  = '',
        deleted   = '✖',
        renamed   = '',
        -- Status type
        untracked = '',
        ignored   = '',
        unstaged  = '',
        staged    = '',
        conflict  = '',
      }
    },
  },
  window = {
    position = 'left',
    width = 25,
    mapping_options = {
      noremap = true,
      nowait = true,
    },
    mappings = {
          ["<space>"] = {
        "toggle_node",
        nowait = false,
      },
          ["<2-LeftMouse>"] = "open",
          ["<cr>"] = "open",
          ["<esc>"] = "revert_preview",
          ["P"] = { "toggle_preview", config = { use_float = true } },
          ["l"] = "focus_preview",
          ["S"] = "open_split",
          ["s"] = "open_vsplit",
          ["t"] = "open_tabnew",
          ["w"] = "open_with_window_picker",
          ["C"] = "close_node",
          ["z"] = "close_all_nodes",
          ["a"] = {
        "add",
        config = {
          show_path = "none"
        }
      },
          ["A"] = "add_directory",
          ["d"] = "delete",
          ["r"] = "rename",
          ["y"] = "copy_to_clipboard",
          ["x"] = "cut_to_clipboard",
          ["p"] = "paste_from_clipboard",
          ["c"] = "copy",
    }
  },
  nesting_rules = {},
  filesystem = {
    visible = false,
    hide_dotfiles = true,
    hide_gitignored = true,
    hide_hidden = true,
    hide_by_name = {
      --"node_modules"
    },
    hide_by_pattern = {
      --"*.meta",
      --"*src/*/tsconfig.json",
    },
    always_show = {
      --".gitignored",
    },
    never_show = {
      --".DS_Store",
      --"thumbs.db",
    },
    never_show_by_pattern = {
      --".null_ls_*",
    },
  },
  follow_current_file = false,
  group_empty_dirs = false,
  hijack_netrw_behavior = "open_default", -- "open_current", "disabled",
  use_libuv_file_watcher = false,
  buffers = {
    follow_current_file = true,
    group_empty_dirs = true,
    show_unloaded = true,
    window = {
      mappings = {
            ["bd"] = "buffer_delete",
            ["<bs>"] = "navigate_up",
            ["."] = "set_root",
      }
    },
  },
  git_status = {
    window = {
      position = "float",
      mappings = {
            ["A"] = "git_add_all",
            ["gu"] = "git_unstage_file",
            ["ga"] = "git_add_file",
            ["gr"] = "git_revert_file",
            ["gc"] = "git_commit",
            ["gp"] = "git_push",
            ["gg"] = "git_commit_and_push",
      }
    }
  }
})

vim.cmd([[noremap \ :Neotree reveal<cr>]])
```

## Comment nvim

```
use {
  'numToStr/Comment.nvim',
  config = function()
    require('Comment').setup()
  end
}
```

Buat file `comment.rc.lua` di `.config/nvim/after/plugin/comment.rc.lua`.

```
local status, Comment = pcall(require, 'Comment')
if (not status) then return end

require('Comment').setup({
  --Add a space b/w comment and the line
  padding = true,
  --Whether the cursor should stay at its position
  sticky = true,
  --Lines to be ignored while (un)comment
  ignore = nil,
  --LHS of toggle mappings in Normal mode
  toggler = {
    --Line-comment toggle keymap
    line = 'gcc',
    --Block-comment toggle keymap
    block = 'gbc',
  },
  opleader = {
    --Line-comment keymap
    line = 'gc',
    --Block-comment keymap
    block = 'gb',
  },
  --LHS of extra mappings
  extra = {
    --Add comment on the line above
    above = 'gcO',
    --Add comment on the line bellow
    below = 'gco',
    --Add comment at the end of line
    eol = 'gcA',
  },
  --Enable keybindings
  --Note: if given 'false' then the plugin won't create any mappings
  mappings = {
    --Operator-pending mapping; 'gcc' 'gbc' 'gc[count]{motion}' 'gb[count]{motion}'
    basic = true,
    --Extra mapping; 'gco', 'gcO', 'gcA'
    extra = true,
  },
  --Function to call before (un)comment
  pre_hook = nil,
  --Function to call after (un)comment
  post_hook = nil,
})
```

## Markdown preview

```
use {
  "iamcco/markdown-preview.nvim",
  run = function()
    vim.fn["mkdp#util#install"]()
  end,
  ft = "markdown",
  cmd = { "MarkdownPreview" },
  requires = { "zhaozg/vim-diagram", "aklt/plantuml-syntax" },
}
```

Buat file `preview.rc.lua` di `.config/nvim/after/plugin/preview.rc.lua`.

```
local status, preview = pcall(require, 'markdown-preview.nvim')
if (not status) then return end

require('preview').setup {
  mkdp_auto_start = 0
}
```

## Mini nvim (startup)

```
use 'echasnovski/mini.nvim'
```

Buat file `mini.rc.lua` di `.config/nvim/after/plugin/mini.rc.lua`.

```
local status, starter = pcall(require, 'mini.starter')
if (not status) then return end

local starter = require('mini.starter')
starter.setup({
  items = {
    starter.sections.telescope(),
  },
  content_hooks = {
    starter.gen_hook.adding_bullet(),
    starter.gen_hook.aligning('center', 'center'),
  },
})
```

***

Itulah beberapa plugin dengan konfigurasinya yang saya gunakan di neovim saya untuk belajar web dev.

Untuk source code nya bisa sobat cek langsung di github saya [neovim-setup](https://github.com/RezaIchsani/neovim-setup). Terima kasih, semoga bermanfaat :) .





















