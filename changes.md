### fix

- Scroll the caret into view on Backspace line merge/delete (selection delete, list merge, component delete, brLine/soft-break/empty-line merge, and other branches) (`core/event/rules/keydown.rule.backspace`)
- `selection.scrollTo` now accounts for the top sticky toolbar offset (`_toolbar_sticky`) — fixes the caret being hidden under the sticky toolbar when the editor sits in an outer scroll area (`core/logic/dom/selection`)
- `selection.scrollTo` no longer pulls a still-visible caret downward on Backspace-up in auto-height mode when it already cleared the top sticky toolbar (`core/logic/dom/selection`)
