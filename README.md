<img width="295" height="120" alt="screenshot-2026-07-02_18-20-02" src="https://github.com/user-attachments/assets/2f94a558-4d92-431b-8221-211e2405ec25" />


# geass.nvim

local AI inline completions in Neovim.

## how it works

Hits your local model with prefix+suffix around the cursor, streams back a completion, shows it as ghost text. Accept with `<Tab>`, dismiss with `<Esc>`, trigger manually with `<M-CR>`(alt+enter).

## requirements

- Neovim >= 0.10 (uses `vim.text.diff`)
- [Ollama](https://ollama.com) running locally (default provider)

## install & setup

```lua
-- lazy.nvim
{
  "tseluka/geass.nvim",
  config = function()
    require("geass").setup({
      provider = "ollama",
      model = "qwen/qwen2.5-coder:1.5b",
      url = "http://localhost:11434/api/generate",
    })
  end,
}
```

## options

| key             | default              | description                        |
|-----------------|----------------------|------------------------------------|
| `provider`      | `"ollama"`           | backend (`"ollama"` / `"opencode"`)|
| `model`         | `"ibm/granite4:tiny-h"` | model name for the provider     |
| `debounce`      | `300`                | debounce window (ms)               |
| `throttle`      | `1000`               | throttle interval (ms)             |
| `context_window`| `16000`              | total chars sent to the model      |
| `context_ratio` | `0.75`               | fraction of window for prefix      |
| `enabled`       | `true`               | start enabled (toggle at runtime)  |

### commands

| command         | description                                  |
|-----------------|----------------------------------------------|
| `:Geass`        | toggle completions on/off (alias for `toggle`)|
| `:Geass toggle` | flip enabled state                           |
| `:Geass on`     | enable completions                           |
| `:Geass off`    | disable completions (cancels in-flight + preview) |

### keymaps

| action  | default     |
|---------|-------------|
| trigger | `<M-CR>`    |
| accept  | `<Tab>`     |
| dismiss | `<Esc>`     |

## roadmap

- [x] ollama provider
- [x] automatic trigger on CursorHoldI
- [ ] multi-candidate cycling
- [ ] tests
