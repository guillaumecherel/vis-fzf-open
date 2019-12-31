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
plugin_vis_open =require('plugins/vis-fzf-open/fzf-open')

-- Path to the fzf executable (default: "fzf")
plugin_vis_open.fzf_path = (
    "FZF_DEFAULT_COMMAND='ag --hidden --ignore .git -g \"\"' fzf"
)
-- Arguments passed to fzf (default: "")
plugin_vis_open.fzf_args = "-q '!.class ' --height=40%"
```
