## Layer5 

[Layer5](https://github.com/layer5io/layer5) is the open source, cloud-native management company behind Meshery and related projects. The website is built with Gatsby and React.

---

### 1. perf(images): Replace Kanvas `<img>` Tags with `StaticImage`

Addresses image rendering performance in the Kanvas section by replacing 27 raw HTML `<img>` tags with Gatsby's `StaticImage` component across `kanvas-catalog.js`, `index.js`, and `kanvas-modes.js`. Added `StaticImage` imports where needed, removed now-unneeded static image imports, and updated styled-component selectors from `img` to `.gatsby-image-wrapper` where layout depended on direct `<img>` targeting. Enables the full Gatsby image pipeline for these assets, improving optimized delivery and rendering consistency.

🔗 [View PR](https://github.com/layer5io/layer5/pull/7619)

---

### 2. fix(navigation): Clean Up Leaked Global Scroll Listeners

Fixes memory leaks caused by uncleaned global `scroll` listeners in SPA navigation flows. Two components attached `window.addEventListener("scroll", ...)` using anonymous callbacks inside `useEffect` without corresponding cleanup, causing listeners to accumulate across route transitions. Added named `handleScroll` and `handleHeaderScroll` functions with cleanup returns in `Navigation/index.js` and `Brand/index.js` respectively, enabling `window.removeEventListener(...)` on unmount and preventing stacked listeners, memory leaks, and scroll-jank over long sessions.

🔗 [View PR](https://github.com/layer5io/layer5/pull/7617)

---

### 3. fix(smi-table): Optimize Row Rendering with Memoized Rows

Resolves the SMI table rendering performance issue by isolating row rendering and collapse state per row. Refactored table row rendering from inline mapping into a separate `TableRow` component in `src/components/SMI-Table/index.js`, wrapped it with `React.memo()`, and moved collapse state from a parent-level array to per-row local `useState`. Clicking one row now updates only that row's state instead of triggering a full table body re-render, improving interaction responsiveness for larger datasets with no change to existing visual behavior.

🔗 [View PR](https://github.com/layer5io/layer5/pull/7618)

---

### 4. fix(a11y): Improve Alt Text in Features and Kanvas Visuals

Improves accessibility (WCAG-focused image semantics) by fixing missing, generic, and empty `alt` attributes across high-impact Components and Kanvas sections. Updated instructional images to use descriptive alt text, marked decorative images with `alt=""` and `aria-hidden="true"`, and replaced generic `"image"` alt values with context-aware descriptions. Changes span seven files across the Features, Academy, and Kanvas sections, improving screen-reader accessibility and reducing ambiguous image announcements.

🔗 [View PR](https://github.com/layer5io/layer5/pull/7620)

---

**Tech Stack:** `React` · `Gatsby` · `StaticImage` · `styled-components` · `Accessibility (WCAG)` · `Performance Optimization`
