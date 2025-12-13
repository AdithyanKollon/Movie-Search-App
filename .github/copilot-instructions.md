# Copilot / Agent Instructions for this repository

This is a small Create React App single-page application. Keep instructions concise and focused on patterns you can verify in the codebase.

- **Project type**: Create React App (CRA) SPA. Entry: [src/index.js](src/index.js#L1-L20). Main UI lives in [src/App.js](src/App.js#L1-L200).
- **Run / Build**: use npm scripts from `package.json`: `npm start` (dev), `npm test`, `npm run build`.
- **Dependencies**: lightweight—React, react-dom, react-scripts. Avoid changing dependency versions unless the change is necessary and tested.

Key patterns and integration points
- Single top-level component `App` (see [src/App.js](src/App.js#L1-L200)). No global state library; favor local React state/hooks when modifying behavior.
- Static assets (CSS and images) live in `src/` alongside components: `src/App.css` and `src/search.svg` are used by `App`.
- External API: OMDb is called using the base URL set in `src/App.js` (`API_URL='http://www.omdbapi.com?apikey=e5977ea8'`). Network usage is direct `fetch` calls from components.

Project-specific notes (actionable, discoverable)
- The `searchMovies` helper in `src/App.js` contains a template bug: the fetch URL uses `&s={title}` (literal braces). Use `&s=${title}` to interpolate the variable.
- The image import is misspelled as `seacrhIcon` in `src/App.js`. Keep existing names when editing, or rename consistently across imports and usage.
- `App` currently uses a hard-coded input `value="Superman"` and empty `onChange` / `onClick` handlers. If implementing interactive search, add state via `useState` and wire handlers.

Agent behavior & guardrails
- Prefer minimal, focused edits that fix visible issues (e.g., the fetch interpolation bug or wiring the input) rather than refactoring entire app structure.
- Don't modify `package.json` scripts or dependency versions unless required for a failing build/test and you document and test the change.
- Keep changes consistent with CRA conventions (keep `public/` for static index, `src/` for code). If adding new files, follow the existing layout: component files in `src/`.

Testing & verification
- Run `npm start` locally and verify the dev server opens at http://localhost:3000 and no console errors appear.
- After fixes, test the search path by calling `searchMovies('spiderman')` (already invoked in `useEffect`) — verify `console.log` output in dev tools shows `data.Search`.

Examples to reference when editing
- Fix fetch interpolation: in [src/App.js](src/App.js#L1-L200) change

```js
// bad
fetch(`${API_URL}&s={title}`)

// good
fetch(`${API_URL}&s=${title}`)
```

- Wire input state: add `const [query, setQuery] = useState('')`, replace `value="Superman"` with `value={query}` and implement `onChange={e => setQuery(e.target.value)}`.

When unsure, ask the repo owner for intent before making large design changes (e.g., introducing global state, routing, or changing the public API key handling).

If you update or add instructions, keep them short and reference concrete files or lines where possible.

---
If anything here is unclear or you'd like the agent to also apply the small fixes (fetch interpolation, input wiring), tell me which fixes to make and I will implement them and run the dev server checks.
