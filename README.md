# A File Explorer For Neovim Written In Lua

[![CI](https://github.com/nvim-tree/nvim-tree.lua/actions/workflows/ci.yml/badge.svg)](https://github.com/nvim-tree/nvim-tree.lua/actions/workflows/ci.yml)

<img align="left" width="199" height="598" src="https://user-images.githubusercontent.com/1505378/232662694-8dc494e0-24da-497a-8541-29344293378c.png">
<img align="left" width="199" height="598" src="https://user-images.githubusercontent.com/1505378/232662698-2f321315-c67a-486b-85d8-8c391de52392.png">

   Automatic updates

   File type icons

   Git integration

   Diagnostics integration: LSP and COC

   (Live) filtering

   Cut, copy, paste, rename, delete, create

   Highly customisable

<br clear="left"/>
<br />

Take a look at the [wiki](https://github.com/nvim-tree/nvim-tree.lua/wiki) for Showcases, Tips, Recipes and more.

Community support: [matrix](https://matrix.to/#/#nvim-tree:matrix.org)

## New Mapping Method 2023-02-27

[:help nvim-tree.view.mappings](doc/nvim-tree-lua.txt) have been deprecated in favour of [:help nvim-tree.on_attach](doc/nvim-tree-lua.txt). Please visit [Migrating To on_attach](https://github.com/nvim-tree/nvim-tree.lua/wiki/Migrating-To-on_attach) to transition.

## Requirements

[neovim >=0.8.0](https://github.com/neovim/neovim/wiki/Installing-Neovim)

[nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons) is optional and used to display file icons. It requires a [patched font](https://www.nerdfonts.com/). Your terminal emulator must be configured to use that font, usually "Hack Nerd Font"

## Install

Please install via your preferred package manager. See [Installation](https://github.com/nvim-tree/nvim-tree.lua/wiki/Installation) for specific package manager instructions.

`nvim-tree/nvim-tree.lua`

`nvim-tree/nvim-web-devicons` optional, for file icons

## Quick Start

Disabling [netrw](https://neovim.io/doc/user/pi_netrw.html) is strongly advised, see [:help nvim-tree-netrw](doc/nvim-tree-lua.txt)

Setup the plugin in your `init.lua`

```lua
-- disable netrw at the very start of your init.lua
vim.g.loaded_netrw = 1
vim.g.loaded_netrwPlugin = 1

-- set termguicolors to enable highlight groups
vim.opt.termguicolors = true

-- empty setup using defaults
require("nvim-tree").setup()

-- OR setup with some options
require("nvim-tree").setup({
  sort_by = "case_sensitive",
  view = {
    width = 30,
  },
  renderer = {
    group_empty = true,
  },
  filters = {
    dotfiles = true,
  },
})
```

Optionally customise your mappings, see [:help nvim-tree-mappings](doc/nvim-tree-lua.txt)

```lua
  local function my_on_attach(bufnr)
    local api = require "nvim-tree.api"

    local function opts(desc)
      return { desc = "nvim-tree: " .. desc, buffer = bufnr, noremap = true, silent = true, nowait = true }
    end

    -- default mappings
    api.config.mappings.default_on_attach(bufnr)

    -- custom mappings
    vim.keymap.set('n', '<C-t>', api.tree.change_root_to_parent,        opts('Up'))
    vim.keymap.set('n', '?',     api.tree.toggle_help,                  opts('Help'))
  end

  -- pass to setup along with your other options
  require("nvim-tree").setup {
    ---
    on_attach = my_on_attach,
    ---
  }
```

Open the tree:  `:NvimTreeOpen`

Show the mappings:  `g?`

For complete list of available configuration options see [:help nvim-tree-setup](doc/nvim-tree-lua.txt)

Each option is documented in `:help nvim-tree.OPTION_NAME`. Nested options can be accessed by appending `.`, for example [:help nvim-tree.filters.dotfiles](doc/nvim-tree-lua.txt)

## Commands

See [:help nvim-tree-commands](doc/nvim-tree-lua.txt)

Basic commands:

`:NvimTreeToggle` Open or close the tree. Takes an optional path argument.

`:NvimTreeFocus` Open the tree if it is closed, and then focus on the tree.

`:NvimTreeFindFile` Move the cursor in the tree for the current buffer, opening folders if needed.

`:NvimTreeCollapse` Collapses the nvim-tree recursively.

## Mappings

`g?` toggles help, showing all the mappings and their actions.

To customise your mappings see [:help nvim-tree.on_attach](doc/nvim-tree-lua.txt) and [:help nvim-tree-mappings](doc/nvim-tree-lua.txt)

## Roadmap

nvim-tree is stable and new major features will not be added. The focus is on existing user experience.

Users are encouraged to add their own custom features via the public [API](#api).

Development is focused on:
* Bug fixes
* Performance
* Quality of Life improvements
* API / Events
* Enhancements to existing features

## API

nvim-tree exposes a public API. This is non breaking, with additions made as necessary. See [:help nvim-tree-api](doc/nvim-tree-lua.txt)

See wiki [Recipes](https://github.com/nvim-tree/nvim-tree.lua/wiki/Recipes) and [Tips](https://github.com/nvim-tree/nvim-tree.lua/wiki/Tips) for ideas and inspiration.

Please raise a [feature request](https://github.com/nvim-tree/nvim-tree.lua/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=) if the API is insufficient for your needs. [Contributions](#Contributing) are always welcome.

You may also subscribe to events that nvim-tree will dispatch in a variety of situations, see [:help nvim-tree-events](doc/nvim-tree-lua.txt)

## Contributing

PRs are always welcome. See [wiki](https://github.com/nvim-tree/nvim-tree.lua/wiki/Development) to get started.

See [bug](https://github.com/nvim-tree/nvim-tree.lua/issues?q=is%3Aissue+is%3Aopen+label%3Abug) and [PR Please](https://github.com/nvim-tree/nvim-tree.lua/issues?q=is%3Aopen+is%3Aissue+label%3A%22PR+please%22) issues if you are looking for some work to get you started.

### Help Wanted

Developers with the following environments:

* Apple macOS
* Windows
  * WSL
  * msys
  * powershell

Help triaging, diagnosing and fixing issues specific to those environments is needed, as the nvim-tree developers do not have access to or expertise in these environments.

Let us know you're interested by commenting on issues and raising PRs.

## Screenshots

See [Showcases](https://github.com/nvim-tree/nvim-tree.lua/wiki/Showcases) wiki page for examples of user's configurations with sources.

Please add your own!

