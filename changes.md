### fix

- Scroll the caret into view after Backspace (char delete / line merge at a viewport edge) (`core/event`)
- Normalize the edit range for Backspace/Delete too (not just Enter), fixing broken deletion when the caret container is the line element instead of a text node — the range normalization had only ever run for Enter, so the custom Backspace/Delete merge branches added in `v3.1.4` misfired on such carets (`core/event`)
- Prevent per-line placeholder (`placeholder_line`) from lingering on multiple lines after a batched multi-line insert (`core/logic`)
