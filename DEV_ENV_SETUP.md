# Dev Environment Setup

Short, opinionated defaults for this workflow.

## Preferred tools

- **WezTerm** for the terminal: fast, scriptable, good font/rendering support.
- **herdr** for local dev orchestration when a project needs repeatable background services.
- **pi agent** for coding-agent work in the terminal.

## WezTerm

Keep it boring: readable font, sane scrollback, no distracting chrome.

```lua
-- ~/.wezterm.lua
local wezterm = require("wezterm")

return {
  color_scheme = "Catppuccin Mocha",
  font = wezterm.font("JetBrains Mono"),
  font_size = 13.0,
  window_decorations = "RESIZE",
  hide_tab_bar_if_only_one_tab = true,
  scrollback_lines = 10000,
  enable_kitty_keyboard = true,
}
```

## pi agent

Prefer fast defaults, then raise thinking only when the task needs it.

```json
// ~/.pi/agent/settings.json
{
  "defaultThinkingLevel": "low",
  "hideThinkingBlock": false
}
```

Useful pi keys:

- `Ctrl+C` clears the current input; press again on empty input to exit.
- `Shift+Tab` cycles thinking level.
- `Ctrl+L` opens model select.
- `Ctrl+P` cycles models.
- `Ctrl+G` opens the prompt in `$EDITOR` / external editor.

Optional keybindings:

```json
// ~/.pi/agent/keybindings.json
{
  "tui.editor.historyPrevious": "ctrl+p",
  "tui.editor.historyNext": "ctrl+n",
  "tui.editor.deleteWordBackward": ["ctrl+w", "alt+backspace"]
}
```

After changing pi config, run `/reload` inside pi.

## herdr

Use herdr for small, repeatable project service setup. Keep project commands named plainly and avoid hidden global state.

Suggested shape:

```text
start   # run the app and required local services
stop    # stop project services
logs    # tail the useful logs
reset   # reset local state only when intentionally requested
```

## Defaults

- Prefer project-local config over machine-global magic.
- Keep setup files short enough to audit quickly.
- Document anything surprising in the repo, not in memory.
