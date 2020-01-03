# Fuzzy find and open files in vis

Use [fzf](https://github.com/junegunn/fzf) to open files in [vis](https://github.com/martanne/vis).

## Usage

In `vis`:
- `:fzf`: search all files in the current sub-tree.
- You can pass arguments to fzf, e.g. : `:fzf -p !.class`

While in `fzf`:

- `<Enter>` to open the selected file in current window
- `<C-s>` to open the selected file in a horizontal split
- `<C-v>` to open the selected file in a vertical split

## Configuration

In `visrc.lua`:

```lua
plugin_vis_open = require('plugins/vis-fzf-open/fzf-open')

-- Path to the fzf executable (default: "fzf")
plugin_vis_open.fzf_path = (
    "FZF_DEFAULT_COMMAND='ag --hidden --ignore .git -g \"\"' fzf"
)
-- Arguments passed to fzf (default: "")
plugin_vis_open.fzf_args = "-q '!.class ' --height=40%"

-- Mapping configuration example
vis.events.subscribe(vis.events.INIT, function()
    vis:command('map! normal <C-p> :fzf<Enter>')
end)
```

Complex example for `plugin_vis_open.fzf_args`:

```lua
my_fzf_args = string.gsub([[
    --bind=$my_fzf_key_bindings \
    --color fg:242,bg:236,hl:65,fg+:15,bg+:239,hl+:108 \
    --color info:108,prompt:109,spinner:108,pointer:168,marker:168 \
    --delimiter / --nth -1 \
    --height=70% \
    --inline-info \
    --no-mouse \
    --preview-window=up:70% \
    --preview="(
        bat --style=changes,grid,numbers --color=always {} ||
        highlight -O ansi -l {} ||
        coderay {} ||
        rougify {} ||
        cat {}
    ) 2> /dev/null | head -1000"
]], '%$([%w_]+)', {
    my_fzf_key_bindings=table.concat({
        "alt-j:preview-down",
        "alt-k:preview-up",
        "ctrl-f:preview-page-down",
        "ctrl-b:preview-page-up",
        "?:toggle-preview",
        "alt-w:toggle-preview-wrap",
        "ctrl-z:clear-screen"
    }, ",")
})

-- Arguments passed to fzf (default: "")
plugin_vis_open.fzf_args = my_fzf_args
```
