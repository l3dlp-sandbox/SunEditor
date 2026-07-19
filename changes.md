### fix

- Enter now falls back to the synchronous `keydown` path in environments that drop `beforeinput` at runtime (some corporate security SW / DLP / VDI), restoring the mobile virtual-keyboard focus-shuffle on that path (`core/event`, `helper/env`)
