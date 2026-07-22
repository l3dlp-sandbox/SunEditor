### fix

- Enter now falls back to the synchronous `keydown` path in environments that drop `beforeinput` at runtime (some corporate security SW / DLP / VDI), restoring the mobile virtual-keyboard focus-shuffle on that path (`core/event`, `helper/env`)
- Percentage-sized media components (image/video/audio/iframe) no longer reset to 100% after a clean() round-trip (code view toggle, `setValue`, paste); the container's `width`/`height`/`min-width` is now preserved via the new `@component` `tagStyles` category (`core/logic/dom/html`, `tagStyles`)
- Block handle now aligns to the vertical center of the block's first line instead of the block's top edge, so its buttons no longer sit a few pixels below the line (and headings/padded blocks are centered correctly too), making them easier to click (`core/logic/panel/blockHandle`)
- Fixed Shift+Enter (soft line break), which broke after Enter moved to the `beforeinput` path — it no longer does nothing on empty lines, splits the paragraph on Safari, or stops when the key is held (`core/event`)
- Backspace/Delete now removes a soft line break (Shift+Enter) in a single press (`core/event`)
- The per-line "Type '/' for commands" placeholder no longer shows inside table cells (`core/logic/shell/ui`)
- Editor-internal buttons that were missing an explicit `type` no longer default to `type="submit"`, so clicking them no longer submits an enclosing `<form>` (`modules/contract/Browser`, `core/logic/shell/ui`, `modules/ui/CommandMenu`) (#1675)
- Empty heading lines no longer serialize to a bare `####` in the markdown view (`helper/markdown`)
