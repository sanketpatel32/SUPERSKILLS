# Minimal UI/UX

Use this rule for UI, UX, frontend polish, layout, design-system, component, page, form, dashboard, and navigation work.

## Direction

Default aesthetic: clean, minimal, calm, readable, and user-focused.

The interface should be simple enough for a non-technical 60-year-old user to understand without explanation.

Hard defaults:
- no decorative gradients unless the user explicitly asks
- no AI-looking glow blobs, glass panels, purple hero gradients, or noisy backgrounds
- no animation that distracts from the task
- no UI change that risks crashing or destabilizing the app
- no hiding important actions just to make the page look cleaner

## Before Designing

Inspect the app first:
- existing component library
- existing design system or tokens
- current layout, spacing, typography, and navigation patterns
- available prebuilt components
- routes/pages and where the new UI belongs

Prefer what already exists in the app. If the app lacks the needed component, use a reputable prebuilt component or UI library when it reduces risk. Do not add a new UI library without a clear reason.
If adding a library, explain why existing components are insufficient and how the dependency will avoid extra complexity.

## Layout Rules

- Put the most important action where users naturally look first.
- Keep page hierarchy obvious: title, short explanation, primary action, content, secondary actions.
- Treat top and bottom placement carefully: headers, sticky bars, footers, and bottom actions must not hide content or keyboard focus.
- Use whitespace to separate groups, not gradients or heavy borders.
- Keep navigation labels plain and predictable.
- Make page location clear with active nav state, breadcrumbs, tabs, or heading context when needed.
- Avoid dense screens. If a page feels crowded, reduce choices or split sections.

## Interaction Rules

Every clickable control needs visible states:
- default
- hover
- focus-visible
- active/pressed
- disabled
- loading when async

Cursor rules:
- clickable buttons and links use `cursor: pointer`
- disabled controls use `cursor: not-allowed` only when they are truly disabled
- draggable areas use a drag/grab cursor only when drag is actually supported

Buttons must feel clickable without being flashy. Use subtle color, border, background, or elevation changes. Do not rely on color alone.

## Accessibility Rules

- Use semantic HTML and native controls first.
- Text contrast must be strong enough to read comfortably.
- Focus indicators must be visible and not hidden by sticky UI.
- Targets should be comfortable to click or tap; prefer at least 44px height for primary controls.
- Forms need labels, helper text where useful, clear errors, and recovery instructions.
- Drag interactions need a click or keyboard alternative.
- Respect `prefers-reduced-motion`.

## Motion Rules

Use motion only to clarify cause and effect:
- button press feedback
- menu open/close
- loading/progress
- lightweight page or section reveal

Keep animations short, subtle, and interruptible. Disable or reduce them for users who prefer reduced motion.

Avoid:
- bouncing
- parallax
- long delays
- motion that blocks interaction
- decorative page-load animations

## Copy Rules

- Use plain language.
- Prefer verbs users understand: `Save`, `Continue`, `Cancel`, `Delete`, `Try again`.
- Error messages must say what happened and what to do next.
- Empty states should explain why the page is empty and offer the next useful action.

## Verification

Before finishing UI work:
- run the repo's lint/typecheck/build command when relevant
- open the page in a browser when a local target is available
- check desktop and mobile widths
- click the primary actions
- check keyboard tab order and focus visibility
- check loading, empty, error, disabled, and success states when applicable

If verification cannot run, report exactly what was not checked.

## Good Result

A good result feels:
- obvious
- quiet
- stable
- readable
- easy to scan
- hard to misuse

If the UI looks impressive but an older non-technical user would hesitate, simplify it.

Final self-check:
- Can the primary action be found in five seconds?
- Can the page be used without reading a paragraph of explanation?
- Can the user recover from error/loading/empty states?
- Did the UI remain stable on mobile and desktop?
