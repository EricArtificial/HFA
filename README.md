# HFA — Cross-border Health Hub (Single-page Demo)

**Project:** HFA Cross-border Health Hub — a single-file SPA demo (`index.html`) that demonstrates cross-border health services (Care Hub, Protection Hub, Wellness, Family, My HFA).

**Purpose:**
- Quick prototype / demo of a cross-border healthcare assistant for HK↔SZ users.
- Focus on internationalization (i18n), client-side rendering, and small UI interactions without a backend.

**Quick Start (local)**
- Open the project directory and serve the files with a simple HTTP server (recommended):

```bash
# From repo root
# Option 1: Python 3 built-in server
python3 -m http.server 8000
# Then open http://localhost:8000 in your browser

# Option 2: Node static server (if you have npm)
npx serve . -l 8000
```

**Files of interest**
- `index.html`: single-file SPA. All JS, CSS and markup live here.
- `index.html.bak`: backup copy (unchanged) kept for reference.

**Internationalization (i18n)**
- Translations are managed inline inside `index.html` in the `i18nData` object.
  - Keys are grouped by language code: `zh-CN`, `zh-HK`, `en-US`.
  - Use `window.i18n.t('key')` to retrieve translations in code.
- Static DOM elements use `data-i18n` attributes to map keys to elements. On language change, `window.i18n.setLang(lang)` updates those elements.
- Input placeholders use `data-i18n-placeholder` and are updated by `setLang` as well.

Where to add or update translations
- Open `index.html` and find the `i18nData` object (near the top of the inline script). Add or modify keys for each language.
- Example key:
```js
// inside i18nData['en-US']
"care.triage.btn": "Generate Plan",
```
- After editing, refresh the page and use the language selector to verify the UI changes.

**How the client-side language switching works**
- `window.i18n.setLang(lang)` updates:
  - Elements with `data-i18n` (innerHTML)
  - Elements with `data-i18n-placeholder` (placeholder attribute)
  - Re-renders dynamic areas by calling `window.logic.renderHospitals()`, `renderWellness()`, `renderFamily()` if `window.logic` exists.

**Development notes**
- The app is pure client-side. Data like hospitals, members, and wellness packages are stored as translation keys inside `state` and `i18nData`.
- For dynamic strings in logic (e.g., triage results, cost items), the code uses `t('key')` before inserting into the DOM.
- When adding dropdowns or saving values, prefer storing language-agnostic `value` codes (e.g., `value="tcm"` or `value="role.father"`) so UI can be switched without losing stored semantics.

**Testing manual flows**
- Switch languages via the language selector and verify:
  - All navigation labels, cards, modal titles and button text update.
  - Input placeholders change language.
  - Stored member roles and dropdown selections persist meaningfully across language changes.

**Next steps / suggestions**
- Add a minimal GitHub Actions workflow for basic linting or HTML checks.
- Optionally split JS and CSS into separate files for maintainability if this grows.
- Add unit tests for critical logic (symptom matching, cost calculation) if you extract logic into modules.

**Contact / Author**
- Repo owner: EricArtificial

---

If you'd like, I can:
- Commit the README and open a branch/PR.
- Extract the inline script into separate `app.js` and `i18n.js` files.
- Generate a small test harness for the prediction/cost logic.

Tell me which next step you prefer.