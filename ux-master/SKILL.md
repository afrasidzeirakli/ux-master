---
name: "ux-master"
description: "Senior UX/UI design rules for designing, auditing, reviewing or restyling any screen or component so it never looks AI-made (dashboard, form, table, modal, mobile, dark mode). Use for UX/UI დიზაინი, აუდიტი, რევიუ, 'AI-ს ჰგავს', and design explainer videos."
---

# UX MASTER

Think like a senior UX designer: decide the screen before writing code. This skill is a rulebook distilled from 41 short design-engineering lessons (product teardowns, component systems, form UX, mobile, motion, visual systems). Every rule has a number or a test, so apply them literally and cite the rule when you explain a decision.

The first goal of every output: it must not look AI-made. Section 4 is the priority section.

Reply in the user's language (Georgian by default for this user). Keep rule names short and concrete.

## 1. How to work

Pick the mode from the request. If unclear, default to Design.

**Design (new screen or component)** - before any code, write a short decision list: 4 to 6 decisions, each one line in the form "decision -> why the user benefits". Cover: what is the single biggest thing on screen, the one primary action, the states (empty, loading, error, success, disabled), the mobile version, and what is hidden until needed. Then build.

**Audit (existing screen, screenshot or code)** - list what is broken as numbered findings. Each finding: the tell, the rule it breaks, the exact fix with values. Order by user impact. End with a count ("5 tells, 5 fixes").

**Review (a diff or PR)** - check only what changed against the rules below. Flag: missing states, outline none, targets under 44 px, inputs under 16 px on mobile, hover-only actions, fixed pixel radius everywhere, new colors or font sizes off the scale.

**Design system (tokens, foundations, audit of a system)** - follow section 3b: foundations first, then components with all states, then documentation, then motion and polish.

**Restyle (kill the AI look)** - follow the method in section 4: inventory the tells, fix them in order, keep content and features, report before and after values.

In every mode, run the section 4 final tests and the section 8 check before delivering. Never ship a screen that fails the swap test.

## 2. Core principles

1. One anchor per screen. The most important value is the largest text (a bank balance, the primary metric). Everything else steps down.
2. One solid primary button per screen. Every other control is ghost or a text link.
3. Color carries meaning, never decoration. Status is a small dot plus one word. Color never fills a whole card.
4. Show the last meaningful change, not a vanity chart (what shipped, when, by whom).
5. Hide secondary actions in one menu until reached for. Twenty cards must not become a wall of icons.
6. Every state is designed: empty, loading, error, success, disabled, offline, first run.
7. Reversibility beats confirmation. Undo for everything recoverable; friction only for the irreversible, scaled to the cost.
8. Feedback must be honest and immediate: the screen answers within 400 ms or shows real progress.
9. Systems, not one-offs: one type scale, one spacing unit, one radius scale, one icon stroke, one accent.
10. Touch is not a small desktop. Restructure, do not shrink.

## 3. Rules by topic

### Buttons
- Tap target at least 44 px tall even if the button looks smaller (visual can be 32 px).
- Label says the action: "Create workspace", never "Submit".
- One primary per screen; Cancel is ghost.
- Loading: keep the width, swap label for a spinner, ignore the second click.
- Focus ring always visible for keyboard. Never ship outline none.
- A disabled button says why ("Name your workspace first").

### Typography
- Default system font stack reads as a starter template. Pick a face from the product's world (a repair shop should not sound like a bank).
- Load the font for real (web font with display swap). Check on a machine where it is not installed, otherwise the fallback ships.
- One family, two weights. Build hierarchy from size and weight.
- Modular scale with a fixed ratio: caption, body, heading, display. No random sizes.
- Monospace only for strings the user copies (domain, commit hash, ID). Everything else sans.
- Numbers: tabular digits, one line, never wrap. Cap big figures on phones so a sign never lands alone.

### Color and gradients
- Palette methods: monochromatic (one hue, vary lightness), complementary (two opposites for contrast), analogous (three neighbors for harmony).
- One flat accent. Accent appears on the primary action and the active state only.
- Gradients: hues within 60 degrees on the wheel; 135 degrees reads premium, 0 flat, 45 and 90 forgettable; mesh (3 or more color points) beats two-color linear; gradient text on headlines only, body stays solid.
- Never rely on background tint alone for meaning: add an icon and a left border (about 6 percent of users cannot distinguish the tint).

### Spacing and grid
- Base unit 4 px, layout rhythm on 8 px. Steps 4, 8, 12, 16, 24, 32, 48, 64 (see section 3b). Apply to every gap and padding; never eyeball.
- The grid is a ratio system, not 12 equal columns: 4+8 gives hierarchy, 6+6 equal, 3+9 pushes to one side.
- Breakpoints reconfigure the grid: 12 -> 6 -> 4 -> 1 columns.
- Gutter is a choice: 8 px tight and technical, 24 balanced, 40 editorial and luxurious.
- Break the grid on purpose only: full-bleed hero, pull quote into the margin.
- Atoms (color, type, spacing, radius) -> molecules (button) -> organisms (card).

### Corner radius
- Nested corners are concentric: inner = outer minus padding (12 outer, 8 padding, 4 inner).
- Radius follows size: small 4, medium 8, large 16. One scale, every element on it.
- Full radius is a shape, not a number: pills for single-line chips, avatars, toggles. Multi-line containers get a real number.
- An element touching a screen edge has no corner there (bottom sheet: top corners rounded, bottom zero).
- Selection or focus ring drawn outside: outer = inner plus the gap (8 in, 10 out).
- Images: let the card clip them (overflow hidden); inset images subtract the padding.

### Icons
- One stroke width across the product: 1.5 or 2, never both. Mixed sets are the top tell of cheap UI.
- Optical beats geometric: a 16 px glyph in a 20 px box; arrows and play icons shift 1 px toward their direction.
- Sizes lock to type: 16 next to 14 px text, 20 next to 16, 24 next to headings. Never a random 18.
- Icon color is text color: secondary gray by default, full text color on hover, accent only when active.
- Never mix outline and filled, except filled means selected.

### Dark mode
- Near black, not pure black (around #0B0D10 to #121212) so layers have room. Pure black saves OLED battery but kills depth.
- Elevation by lightness, not shadow: the higher the surface, the lighter. A heavy black box-shadow on a dark page is invisible.
- Text is white at three alphas: 87 percent primary, 60 secondary, 38 disabled. Never pure white.
- Lighten and desaturate the brand color; saturated color glows past its edges.
- Hairlines: 1 px white at 8 percent alpha, not a fixed gray.
- Photos dimmed to about 90 percent brightness. Illustrations get a dark variant, not a filter.

### Forms and validation
- Validate on blur, not on keystroke and not only on submit. Once a field is wrong, switch it to live and clear the error the instant it is fixed.
- Confirm right, not only wrong: a green check after effort.
- Multi-step: about 3 fields read without effort, 12 in a row cause fatigue. Group by context (personal, shipping, payment, review), not by count. Show progress (bar, numbered dots or labels - pick one). Validate inside the step and block Next. Save state on every step; Back and refresh keep the data.
- Mobile inputs at least 16 px (smaller makes iOS Safari zoom) with the right keyboard and autocomplete per field.
- Passwords: strength is entropy, length beats symbols. Show the checklist while typing, ticking live. A growing meter coaches. Eye toggle, never block paste, offer a generated password in one tap.
- Card numbers: group 4 by 4 while typing, detect brand from the first digit (4 Visa, 5 Mastercard), keep the caret where it was, strip pasted dashes instead of rejecting, show formatted and store raw digits.

### Tables, lists, pagination
- Phone: under about 640 px rows become cards. Rank columns by use (identity, value, state); the ID leaves first.
- Two lines per row: name left, amount right, status and date below. Amounts keep one right-aligned slot so the list still compares as a column.
- Label only the ambiguous ("Due Mar 4"; a dollar amount needs no label). Sorting moves to a control.
- Hidden is not deleted: tap expands two fields in place; the full record opens in a bottom sheet, never a new page for a glance.
- The breakpoint belongs to the table: use a container query (six columns need about 700 px), so the same table in a side panel also becomes cards.
- Pagination: cursor based (after this ID), not offset, to avoid duplicates when data shifts. Numbered for jumping, Load more for control, infinite for feeds. Truncate links: first, gap, current neighbors, gap, last. Restore scroll position on Back. Page number lives in the URL.

### Dashboards and product teardown patterns
- One primary metric big, three secondary small. Four identical cards is a spreadsheet with padding.
- Name the period, use a sparkline instead of a percent badge.
- Finance and trust: the balance is the biggest text; every row shows who, how much and a sign (plus for incoming so a refund never looks like a payment); one review screen before money moves (who, how much, fee, when it lands); visible status pending then completed; emergency actions (freeze card) one tap away on the object itself.

### Kanban
- Drag preview lifts: shadow plus about 3 degree tilt.
- Drop placeholder equals the card height so the column opens once.
- WIP limit lives on the column header and changes color when hit.
- Collapse columns to a vertical label with a count; horizontal scroll is the failure mode.
- Swimlanes before a second board. Two boards means two truths.

### Calendar and date picking
- Week view: 7 columns, one hour per row, hour labels on the line, a red now-line, open scrolled to now.
- Color per calendar as a 3 px left stripe with the fill at 10 percent.
- Overlaps sit side by side (half, third), never stacked or hidden behind +1.
- Height is duration: 60 px per hour; 15 minutes still shows one clipped line.
- Drag on empty space draws an event, snap 15 minutes, move by the body, resize by the bottom edge, time label updates while dragging.
- All-day events in a pinned row above the grid.
- Date range picker: presets cover 90 percent of cases (today, yesterday, last 7, last 30, last quarter, custom). Hover previews, click start, click end, drag edges. Two months side by side (three on wide screens). Typing the date works; arrows move, Enter validates, Escape closes, Page Up a month, Shift Page Up a year. On mobile it is a full-screen sheet with vertical scroll and a big confirm button at the bottom.

### Chat
- Same sender within 2 minutes is one group with one avatar: 4 px gap inside, 16 px between groups.
- No timestamp on every bubble: a divider on date change, exact time on hover.
- Optimistic send: the bubble lands on Enter, sent state fades in, failure shows inline with retry. No spinner.
- The list does not jump while reading: a pill counts new messages; auto-anchor only when already at the bottom.
- Typing indicator lives in the flow where the next message lands.
- Composer grows to 5 lines then scrolls; Enter sends, Shift+Enter breaks; attachments preview above the text.

### Overlays: modal, sheet, drawer
- One question decides: must the page stay visible (sheet) or is a full stop needed (modal)?
- Sheet has three snap points: peek, half, full. Released between two, it springs to the nearest.
- Dismiss reads velocity, not only distance: a flick closes from anywhere, a slow drag must cross halfway.
- Desktop: the sheet becomes a side drawer, min 320 px, max 40 percent of the screen.
- Never stack two sheets: replace the content and add a back arrow.
- Premium modal: spring scale-in with slight overshoot, staggered content, scale-down and fade on exit; blurred backdrop plus deep shadow; buttons respond to hover and press.

### Notifications and toasts
- Severity picks the surface: toast (new message), banner (system degraded), modal (card declined, needs a choice), badge (unread count). Never by habit.
- Toast position: bottom right on desktop, top on mobile, never center.
- Timing by type: info 4 s, warning 7 s, error until acknowledged. Destructive toasts carry Undo.
- Stack max 3 visible; new ones push old ones with a spring (damping 20, stiffness 180).
- Always dismissible: close button, swipe on mobile, pause on hover.
- Each type gets an icon plus a left border color.

### Loading and perceived speed
- Under about 300 ms show nothing: a flash of loading state reads as a bug.
- Skeleton when the shape is known (cards, lists, articles) and the wait is longer.
- Spinner for short unknown waits under 3 s, inside the control; never for full pages.
- Progress bar when the percentage is known or the wait is over 3 s: show percent and time left.
- Under 400 ms feels instant. Optimistic UI for likes, saves, bookmarks, toggles: render now, reconcile, roll back on failure. Never for payments, transfers or anything irreversible - show the truth there.
- Uploads: the drop zone answers back (border, glow, copy change); honest progress; inline retry that keeps the file; preview with thumbnail, type and size; each file has its own lane so one failure never blocks the rest.

### Destructive actions and undo
- Undo beats "Are you sure": act instantly, show a toast with Undo for about 5 seconds.
- Soft delete: a deleted flag, 30 days in trash. Deletion is a state, not an event.
- Irreversible actions earn friction: type the name to confirm; the button stays disabled until it matches.
- An undo stack (Cmd or Ctrl+Z through every step) where the product edits content.
- Delayed send: a 10 second grace period.

### Settings
- Toggles for preferences apply instantly. Identity fields (email, name) get a save bar with Cancel. Match the model to the blast radius.
- Group by task, not by table; hide advanced behind one click.
- Search: one input finds any setting, highlights the match and shows its path.
- Every changed setting shows a dot and a per-setting reset.
- Danger zone quarantined at the bottom with a red border.

### Search
- Placeholder is onboarding: "Search by name, SKU or brand", not "Search".
- On focus show recent searches; one click fills the bar.
- Autocomplete ranks by clicks, not alphabet; each option has a category badge; three good results beat ten.
- Arrows navigate, Enter selects, Escape closes, focus stays visible.
- Zero results is never a dead end: suggest alternatives, popular searches or category jumps.

### Dropdowns and tabs
- Dropdown: obvious trigger (chevron, hover state, 44 px target); flips upward at the viewport edge; full keyboard support; over 10 items add search, over 100 virtualize; open animation under 150 ms.
- Tabs: the underline slides, never teleports, and matches the content fade; with many tabs scroll horizontally with edge fades (chevrons on desktop), never wrap to two lines; arrows move, Home and End jump, Tab leaves the group; focus ring and active state never share a color; on mobile use a segmented control under 5 tabs and a bottom sheet over 5; content fades out, pauses about 80 ms, fades in, with matched height to avoid layout shift.

### Toggle switch
- Rail width = 2 x knob diameter; padding = knob radius.
- Morph four properties together in 250 ms ease-out: rail color, knob slide, knob shadow, label crossfade.
- Space toggles, focus ring visible, role switch with aria-checked.
- Flip first, spinner inside the knob, roll back with a message if the server refuses.

### Touch and gestures
- Touch has no hover. Guard hover styles with the hover media query and grow targets under pointer coarse. Ask the pointer, do not sniff the device.
- Hover reveals extras, never the primary action. On mobile move those actions into the card, a swipe, or a bottom sheet.
- Pad the hit area to 44 px and keep the icon small. Dense layout stays for mouse.
- Fixed bottom bars: pad with the safe-area inset and leave room below the content so the last row is reachable.
- Swipe rows: two thresholds - a short pull reveals buttons, a long pull commits on release. Rubber-band resistance, a haptic tick at the commit point. Right is safe (archive, mark read), left is destructive. Teach it once by peeking the first row on first launch. Full-swipe delete needs an Undo toast.

### Empty states
- Four kinds, each designed separately: first run, no results, error, filtered out.
- A small illustration instead of a void; human copy, not a log line.
- Always one primary action that is the real next step, never "Refresh".
- First-run empty state teaches what the feature does.

### Motion and transitions
- Shared-element morphs with the View Transitions API: give the card image and the page header the same view-transition-name; every list item needs a unique name (duplicates cancel the transition); theme toggle as a circular clip-path reveal from the button; a modal grows from the button that opened it; cross-document transitions work without a framework. Unsupported browsers get an instant swap.
- Durations: dropdowns under 150 ms, toggles 250 ms, springs for stacks and modals.
- Glass surface recipe: semi-transparent background, backdrop blur (about 20 px), 1 px low-opacity white border, soft shadow.

## 3b. Design system blueprint

Use this when building a product from scratch, setting up tokens, or auditing a design system. A design system is a single source of truth built in four layers: foundations (color, type, spacing, motion) -> patterns (layout, navigation, forms) -> components (buttons, cards, modals, inputs) -> products. Decide the lower layer before touching the upper one.

### Color tokens
- Never hardcode hex in components. Use semantic tokens with meaningful names (color: var(--text-primary), not color: #1a1a2e). This makes theme switching trivial.
- One primary scale of 9 steps, 100 (lightest) to 900 (darkest), with 500 as the brand color.
- Minimum semantic set: bg.primary, bg.surface, border.default, text.primary, text.muted, brand.primary, status.success, status.error. Add status.warning when needed.
- Reference dark values, to adapt not copy: bg.primary #09090B, bg.surface #131316, border.default #27272A, text.primary #FAFAFA, text.muted #A1A1AA, success #22C55E, error #EF4444.
- The brand hue must come from the product (section 4). Indigo or violet is only acceptable when it is a deliberate choice.

### Type scale tokens
- Eight steps, each with a fixed size and weight: text-xs 11/500, text-sm 13/400, text-base 15/400, text-lg 18/400, text-2xl 22/600, text-3xl 28/700, text-4xl 36/700, text-5xl 48/800.
- Weights available: 400, 500, 600, 700, 800. A single screen still uses two, three at most.
- Line height: headings 1.1 to 1.3, body 1.5 to 1.7, UI labels 1.0 to 1.2. Tighter for large text, looser for small readable text.

### Spacing and grid tokens
- Base unit 4 px; every margin, padding and gap is a multiple of 4. Scale: space-1 4, space-2 8, space-3 12, space-4 16, space-6 24, space-8 32, space-12 48, space-16 64.
- Layout sits on an 8 px grid. Column grid: 12 columns, gutter 16 to 24 px, margin 24 to 48 px.

### Components
- Define every state for every component: default, hover, active, disabled, focus. Designing only the happy path is the most common gap.
- Buttons: variants primary, secondary, ghost, destructive, disabled; sizes small, medium, large.
- Inputs: label above the field, placeholder as an example value, visible focus ring, a distinct disabled style.
- Badges: a small semantic set (new, active, pending, error, default) as a tinted pill with matching text color.
- Build atomic components first (button, input, badge), then composites (card, modal, dropdown). Document props, variants and responsive behavior for each.

### Icon tokens
- Sizes by role: 16 inline, 20 default, 24 navigation, 32 feature, 48 hero.
- Consistent stroke (2 px at a 24 x 24 bounding box), rounded caps and joins, optical alignment on the grid, fills use currentColor.
- Pick one library and stay with it: Lucide, Phosphor, Heroicons or Radix Icons.
- A 20 px icon still gets a 44 x 44 interactive area.

### Motion tokens
- Easing by intent: ease-out for enter and appear, ease-in-out for move and resize, ease-in for exit and leave.
- Duration scale: 100 ms micro (hover, toggle, fade), 200 ms small (button press, tooltip), 300 ms medium (modal, dropdown), 400 ms large (page transition, slide), 500 ms for complex orchestration.
- Three tests: purposeful (guides attention, shows relationships), fast (never blocks the user, 300 ms max for interactions), natural (follows physics).

### Do and do not
- Consistent spacing from the scale, never eyeballed gaps.
- A limited palette (one hue in a few steps), never every color you like.
- A type scale with clear steps, never a heading and body of almost the same size.
- Documented states, never the default state only.
- Semantic tokens, never raw hex.

### Build order (also the audit checklist)
1. Foundations: color palette (primary, neutral, semantic), type scale (sizes, weights, line heights), spacing system, grid (columns, gutters, breakpoints), icon library and sizing rules.
2. Components: atomic components, all states, composite components, props and variants, responsive rules.
3. Documentation: usage guidelines per component, code examples, naming conventions for tokens and classes, a contribution guide.
4. Motion and polish: easing curves and duration scale, transition rules for interactive elements, dark and light theme tokens, loading and empty states.

When a value here differs from a component rule in section 3 (for example a 250 ms toggle, or a 1.5 icon stroke), the specific component rule wins; this section sets the defaults.

## 4. Killing the AI look (priority section)

Apply this to everything you build, not only when asked to restyle.

A screen reads as AI-made when every choice is a default, so nothing on it says anything about this particular product. Test each element with one question: could this sit unchanged in any other app? If yes, it is a tell. "Copy that fits any app fits none."

The five root causes: template defaults (font, radius, shadow, purple gradient), decoration instead of information, no hierarchy, no real states, generic copy and fake data.

### Method
1. Inventory first: number every tell on the screen (1, 2, 3...) and name it in two words ("gradient blob", "3 equal", "generic", "no errors", "96 px").
2. Fix in this order: hierarchy and structure, then color, then surfaces (radius, shadow, border), then type, then copy and data, then states.
3. Keep the content and features. Change what the screen says, not what it does.
4. Report as "N tells, N fixes", each with the before value and the after value (16 -> 8, 96 px -> 24 px).

### Dashboard tells and exact fixes
- Gradient on header, button and chart fill -> flat header on the page surface, one flat accent on the primary button only, chart as a thin line with no area fill. "Gradients with nothing to say."
- An icon in a colored tile per card (blue, green, purple, orange) -> remove the tiles. Small label in secondary text, the number is the hero. "Four colors for four numbers is decoration."
- Four identical cards (same size, same weight, same badge) -> one primary card about two columns wide: big number (roughly twice the secondary size), its change spelled out ("+12.5% vs Jul"), a sparkline next to it, a breakdown underneath (Subscriptions / One-time). The three secondary metrics stack compactly beside it.
- The same green "+12.5%" pill on every card -> real, different deltas with the right unit: percent for counts and money, points for rates ("+0.4 pt"), negatives where they happen. Plain text, not a pill.
- 16 px radius and a drop shadow on cards, inputs, badges and the chart -> radius by size (cards 12, inputs and buttons 8, chips 4), hairline borders, shadow only on what opens above the page. "When everything floats, nothing does."
- "Welcome back, Jordan" with a waving hand -> a title that names the content and the period: "Revenue - Aug 1 to Aug 31, 2026".
- Amounts right-aligned on one edge with tabular digits. Statuses vary and are quiet (Paid, Pending, Refunded).

### Login and auth tells
- A card floating on blurred gradient blobs -> solid surface, split layout: form on the left, the real product on the right (actual UI with real-looking data, not an illustration and not marketing).
- Three equal provider buttons (same height, same weight) -> the provider most users actually pick becomes the one solid primary button; the others become text links on one line ("or continue with GitHub - Apple"). Decide from usage, not alphabet. "Three equal buttons is a menu, not a login."
- A gradient "Sign in" button -> outline. Only one solid button on the screen.
- "Welcome back! Sign in to continue" -> "Sign in to {Product}" plus one line of concrete value ("Your books, closed in a day.").
- No error states -> design all three: wrong credentials ("Email or password is incorrect." and never which one, because that tells an attacker the account exists), lockout after 5 tries with a countdown and a disabled button ("Too many attempts. Try again in 4:59"), unverified email with an inline resend link. "A login with no error state is a demo."
- A 96 px centered logo -> 24 px logo with the name, top left. The form is the hero. A big logo with a tagline and a CTA is a landing page, not a door.

### Typography tells
- The default system stack makes three different products look like one starter template; people read "template" before they read the content.
- Choose the face from the product's world: write two adjectives first ("sturdy, warm"), then pick. A serif says bank, a geometric sans says fintech, a warm grotesque says workshop. The wrong world is as bad as the default.
- Load it for real: font link with display swap, confirm the font file request succeeds, and test in a browser that does not have the font installed. Otherwise your machine shows the font and visitors get the fallback.
- One family, two weights (400 and 700). A real scale, for example 14/400 meta, 18/400 secondary, 24/700 title, 40/700 hero. Three families on one card is a tell.
- Make the entity the headline, not the greeting: small "Good morning," above a large product or customer name.

### Color, surface and motion tells
- Purple or indigo as the unexamined default accent; more than one accent; accent used on things that are not actions or active states.
- Pure black with pure white text, a saturated button that glows, a heavy black shadow on a dark page (see Dark mode).
- Cheap gradients: hues far apart, 0 or 90 degree angle, gradient text in body copy (see Color and gradients).
- Glass, glow and blur without a reason. Use an effect on one focal surface at most.
- Mixed icon sets, mixed stroke widths, emoji used as icons.
- Overlays that just appear with a flat dark scrim, and buttons with no hover or press response.

### Copy and data tells
- Generic labels: "Dashboard", "Welcome back", "Search anything", "Submit", "Get started", "Nothing to show".
- Fake data: round numbers, identical percentages, placeholder people and companies, lorem ipsum, dates without a range.
- Fix: use the product's own nouns, irregular realistic values with units, named periods, varied statuses, and buttons named by action plus object ("New booking", not "Create").

### Final tests
- Squint test: exactly one thing lands first.
- Swap test: put another product's logo on the screen. If it still fits, the screen is still generic.
- Count test: one accent, one solid button, one font family, at most three radius values, shadows only on overlays.
- State test: error, empty, loading and disabled exist and use real copy.

### Quick checklist
1. Purple-to-blue gradients on header, button and chart -> one flat accent.
2. Icon in a pastel tile per card, a different color each -> drop the tiles, the number is the hero.
3. Identical cards with the same size, weight and green badge -> one primary, the rest secondary.
4. 16 px radius and drop shadow on everything -> hairline borders, radius by size, shadow only on what floats above the page.
5. "Welcome back, Name" with a waving hand, "+12.5% from last month" -> name the period, tabular digits, sparkline.
6. Default font stack -> a face chosen for the product, properly loaded.
7. Card floating on a gradient blob -> solid surface or split layout.
8. Three equal-weight buttons -> one primary plus text links.
9. Generic copy that fits any app -> product name plus one line of concrete value.
10. No error, empty or loading states -> design them.
11. Mixed icon sets and stroke widths; emoji as icons -> one set, one stroke.
12. Oversized logo -> 24 px, the task is the hero.

## 5. Default visual direction

Use when the user gives no brand. This is the calm, technical dark style the lessons are presented in.
- Background near black with a faint radial glow of the accent behind the focal element.
- Surfaces one or two steps lighter, 1 px alpha hairlines, radius on the 4 / 8 / 16 scale, almost no shadows.
- One accent (mint-teal family) for the correct state, primary action and active element. Coral red for wrong, destructive and "before". Amber for warnings. Nothing else is colored.
- Tight, bold geometric sans for headlines; the same family at regular weight for body; monospace only for values, code and small uppercase eyebrow labels with wide tracking.
- Generous empty space, one focal object per view, realistic sample data (real names, amounts, commit messages), never lorem ipsum.
If the user has a brand or design system, that wins; keep the rules, swap the tokens. Do not reuse this direction for every product: it is a default for explainers and tools, and section 4 still requires a font and accent chosen for the product's world.

## 6. Explaining design (posts, carousels, short videos)

When the user wants content that teaches a design idea, use this structure:
- Hook in the first 2 seconds: a short claim that names the pain or a contrast ("Your button breaks six rules.", "Same modal. Different feeling.", "Why X feels expensive").
- 4 to 6 numbered rules or decisions, 6 to 10 seconds each, one idea per screen. Total 45 to 85 seconds, vertical 9:16.
- Each screen: small uppercase eyebrow ("DECISION 2 - LAST SHIPPED"), one bold headline of 3 to 6 words written as a rule, one live UI demo in the middle, a one-line takeaway chip at the bottom ("pad the hit area, not the icon").
- Show wrong then right on the same object: red outline and label for the mistake, accent for the fix; the eyebrow pill turns from red to accent when the tell is fixed. Annotate with numbered markers, thin leader lines and exact values (44 px, 250 ms, 87 percent).
- A progress indicator (dots, "decision 3/5").
- Voiceover in short declarative sentences with a consequence: rule, then why the user benefits.
- End with a recap grid of all rules as a checklist, then one call to action ("Save this for your next dashboard").
- Headline patterns: "X is a system.", "Y, done right.", "Never a dead end.", "Hidden is not deleted."

## 7. Output format

- Design: decision list first, then the build. Name tokens (colors, type scale, spacing, radius) once at the top.
- Audit and review: a numbered list of findings, each as tell -> rule -> fix with values. No generic advice.
- State trade-offs in one line when two rules conflict; user's brand and platform conventions win over the defaults here.

## 8. Final check before delivering

- One anchor, one primary button.
- All states exist: empty, loading, error, success, disabled.
- Works at 375 px: no horizontal scroll, 44 px targets, 16 px inputs, safe-area padding, no hover-only actions.
- Keyboard: visible focus, arrows, Enter, Escape where relevant.
- One type scale, 8 px spacing, radius scale, one icon stroke, one accent.
- Destructive actions have undo or proportional friction.
- Feedback under 400 ms or honest progress.
- Passes the squint, swap, count and state tests from section 4.
- Real copy and realistic data.