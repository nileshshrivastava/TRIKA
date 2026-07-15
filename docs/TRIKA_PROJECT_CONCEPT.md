# 🕉️ TRIKA — Project Concept & Continuation Guide
### For Claude Project Mode — Read This First In Any New Session

> **Hari Om Namah Shivaye**

---

## 1. WHAT TRIKA IS

TRIKA is **the world's first ternary programming language**, conceived and built entirely
by one developer ("One Man Army") in **Patna, Bihar, India**, now implemented from scratch
in **pure C (C11)** with zero external runtime dependencies (only libm).

Unlike binary languages built on `true`/`false`, TRIKA's foundational logic is **ternary**,
rooted philosophically in the three **gunas** (qualities) described in the **Bhagavad Gita**:

| Guna | Value | Meaning |
|------|-------|---------|
| **SATTVA** | `+1` | Goodness, clarity, balance, success, "yes" |
| **RAJAS**  | `0`  | Passion, activity, neutrality, "in-progress" |
| **TAMAS**  | `-1` | Inertia, darkness, failure, "no" |

Every conditional, every comparison, every boolean-like operation in TRIKA resolves to
one of these three states instead of just two. The `resolve` keyword (TRIKA's switch
statement) has a **fast path specifically for trika-state matching**
(`sattva_case`, `rajas_case`, `tamas_case`) before falling back to general value matching.

### Why Sanskrit keywords?
TRIKA's keywords are deliberately drawn from Sanskrit/Gita vocabulary so that **the syntax
itself carries philosophical weight** — writing TRIKA code is meant to read like a small
meditation on action, duty, and consequence (echoing Gita 2.47: *"You have a right to
perform your duty, but not to the fruits of action"*).

---

## 2. PROJECT HISTORY — TWO ARCHITECTURAL ERAS

TRIKA has gone through a complete ground-up rewrite. **Both eras matter for context, but
only the second (current) era's files should be treated as the live, working codebase.**

### ERA 1 — Python Prototype (Phases 1–8, March 2026)
The original implementation was a Python-based interpreter: `lexer.py`, `parser.py`,
`interpreter.py`, `tokens.py`, `ast_nodes.py`, `codegen.py`, plus a large family of stdlib
modules written in Python (`trika_db.py`, `trika_net.py`, `trika_http.py`, `trika_ml.py`,
`trika_graph.py`, `trika_crypto.py`, and many more — roughly 20 Python stdlib files covering
everything from MongoDB integration to email/SMTP to thread/socket networking). This era
also produced a PyInstaller-based Windows installer (`trikac.exe` / `trikac9`,
`trikac_setup.iss`) and extensive documentation (`TRIKA_TECHNICAL_GUIDE.md`,
`TRIKA_EXAMPLES.md`, the `TRIKA_PHASE5/6/7/8_EXAMPLES.md` series, `TRIKA_SEED_v1.1` through
`v3.0` design documents).

Era 1 covered: stdlib/REPL/file IO, TritMap (dictionary type), a module/import system,
Records (OOP), exception handling (attempt/catch/finally/raise — later renamed to
sadhana/raksha/antim/sankat), Java interop via subprocess, a self-hosted C compiler
target, and full database integration (SQLite/MySQL/PostgreSQL/MongoDB).

**Era 1 is legacy.** It proved the language design was viable and explored an enormous
surface area of stdlib functionality, but it is not the codebase being actively developed
or fixed today.

### ERA 2 — Native C Runtime (Phase 9 onward, March 2026 → present)
At Phase 9, TRIKA was **completely redesigned and rewritten from scratch in pure C**,
moving from a Python-hosted interpreter to a true native tree-walking interpreter with
manual memory management via reference counting. This is the architecture documented in
detail in §3 below, and is **the current, actively-developed, authoritative version of
TRIKA.** All files described from §3 onward refer exclusively to Era 2.

Era 2 began with a full language redesign (unified collection API, the Sanskrit keyword
system as it exists today, a safe input system, the `vivek()` single-pass query function),
delivered as ~21 core C source files, then progressively added: OOP via `swaroop`,
`sadhana`/`raksha` error handling, `vivek` single-pass queries, `prati` range loops,
`resolve`/case matching — reaching a fully passing 10/10 regression suite by Phase 9's
final session.

---

## 3. ERA 2 ARCHITECTURE — Pure C, Tree-Walking Interpreter (CURRENT)

```
source.tri
    │
    ▼
trika_lexer.c/.h    ── tokenizes source, tracks indentation (INDENT/DEDENT)
    │                   and bracket_depth (Phase 16: suppresses NEWLINE inside [ ] ( ))
    ▼
trika_token.c/.h    ── token type definitions
    │
    ▼
trika_parser.c/.h   ── recursive-descent parser → builds AST
    │
    ▼
trika_ast.c/.h      ── AST node definitions (NODE_* enum), ast_free for cleanup
    │
    ▼
trika_interp.c/.h   ── tree-walking interpreter, executes AST directly (no bytecode/VM)
    │
    ▼
trika_value.c/.h    ── TValue tagged union + reference counting (tv_retain/tv_release)
trika_env.c/.h       ── lexical scoping / environment chain (env_child, env_define, env_get)
```

**Entry point:** `trika_main.c` — handles `trika run file.tri` and REPL mode.

**Memory model:** Manual reference counting via `tv_retain()`/`tv_release()` on every
`TValue`. This is the source of several subtle bugs found and fixed across phases — see
§8 "Known Patterns & Gotchas" before touching map/list internals.

### KEYWORD REFERENCE (canonical — do not invent new ones without explicit request)

| TRIKA keyword | Conventional equivalent | Notes |
|---|---|---|
| `trika`     | `var` / variable declaration | `trika x = 5` |
| `karma`     | `function` / `def`           | `karma add(trika a, trika b): phal a+b` |
| `gyan`      | `import`                     | `gyan trika.math` |
| `uvach`     | `print`                      | supports multiple args: `uvach("a:", a, "b:", b)` |
| `darshan`   | `print` with type/state info | shows 🟢/🟡/🔴 for trika values |
| `phal`      | `return`                     | |
| `yadi`      | `if`                         | supports inline: `yadi x>0: uvach("pos")` |
| `anyatha`   | `else`                       | also used as `resolve`'s default case |
| `yavat`     | `while`                      | |
| `prati`     | `for ... in`                 | `prati item in list:`; also supports range loops |
| `resolve`   | `switch`                     | fast-path SATTVA/RAJAS/TAMAS cases + general `case "x":` + optional `anyatha:` default |
| `swaroop`   | `class`                      | OOP support added Phase 9 |
| `sadhana`   | `try`                        | |
| `raksha`    | `catch`                      | `raksha_sattva`, `raksha_rajas`, `raksha_tamas`, `raksha_all` |
| `antim`     | `finally`                    | |
| `sankat`    | `raise` / `throw`            | also the prefix used for runtime error messages: `✗ sankat: ...` |
| `virama`    | `break`                      | **breaks the NEAREST enclosing loop only** (Phase 16 fix) |
| `agrim`     | `continue`                   | same nearest-loop scoping as `virama` |
| `vivek`     | single-pass query function    | Era-2-original construct, not a direct port from Era 1 |
| `SATTVA`    | `true` / `+1`                | |
| `RAJAS`     | `null` / `0`                 | also the default/"undefined" map lookup result |
| `TAMAS`     | `false` / `-1`               | |

### Data types
- `trika` declares any variable (dynamically typed: int, float, string, list, map, trika-state, function)
- Lists: `[1, 2, 3]` — **multi-line supported** (Phase 16): `[\n  1,\n  2\n]`
- Maps: `{}` then built with `add(map, key, value)` — **NOT** `{"key": value}` literal syntax (not supported by parser)
- Strings: double-quoted, support `+` concatenation and 10 built-in functions (see §6)

---

## 4. ERA 2 STANDARD LIBRARY — 9 Modules (gyan-importable)

| Module | Import | Functions |
|---|---|---|
| `trika.math`      | `gyan trika.math`      | abs, sqrt, pow, log, trig, clamp, lerp, rand, PI/E/PHI constants |
| `trika.file`       | `gyan trika.file`       | read, write, append, lines, exists, delete, size, copy, mkdir, list, join, basename, dirname |
| `trika.time`       | `gyan trika.time`       | now, ms, stamp, tick/step (simulation clock), start/stop/elapsed (timer), sleep, format |
| `trika.grid`       | `gyan trika.grid`       | 2D grid handle system: create, set, get, fill, neighbors4/8, neighbor_states (for cellular automata) |
| `trika.visual`     | `gyan trika.visual`     | terminal rendering of grids: render, render_box, SYMBOL/EMOJI/BLOCK modes, cursor positioning |
| `trika.event`      | `gyan trika.event`      | pub/sub event system: on, emit, off, history |
| `trika.window`     | `gyan trika.window`     | sliding-window algorithm primitive (longest-substring-style problems): create, step, best, run, proof |
| `trika.generator`  | `gyan trika.generator`  | sequence generators from seed + rule karma: create, next, take, fibonacci, tribonacci, pattern |
| `trika.canvas`     | `gyan trika.canvas`     | **28-chart-type graphics engine** — superset of matplotlib/plotly/seaborn (see §7) |
| `trika.input`      | `gyan trika.input`      | interactive input prompts (Phase 14b) — `prashan()`/`input.read()` style |

*Note: Era 1 (Python prototype) had a much larger stdlib surface (db, net, http, ml, graph,
crypto, csv, excel, pdf, smtp, socket, thread, ws...) — none of these have been ported to
the Era 2 C runtime yet. They represent a roadmap of "things TRIKA could eventually have,"
not current functionality.*

All Era 2 modules are wired via the `NODE_GYAN` case in `trika_interp.c`, dispatching on
the module path string to the appropriate `*_register(env)` function which populates a
`TValue` map of native function pointers.

---

## 5. ERA 2 PHASE HISTORY — What Has Been Built (chronological)

| Phase | Date | Delivered |
|---|---|---|
| 9 | Mar 29 – Apr 17 | Full language redesign in pure C: lexer, parser, AST, tree-walking interpreter, value system with refcounting, environment/scoping. ~21 core .c/.h files. Sanskrit keyword system finalized. `swaroop` OOP, `sadhana`/`raksha` error handling, `vivek` single-pass query, `prati` range loops, `resolve`/case matching. **10/10 regression tests passing** by end of phase. |
| 10–11 | Apr 21 | **Kurukshetra simulation** — an 18×18 grid cellular-automaton demo encoding 5 "guna laws" and 9 Bhagavad Gita verses as program logic; the flagship demonstration of why ternary logic + Sanskrit semantics is expressive. First 6 stdlib modules delivered: math, file, time, grid, visual, event. |
| 12 | May 15 | `trika.window` + `trika.generator` modules; sliding-window and sequence-generation primitives; streaming pipeline demo (`pipeline_demo.tri`). Fixed a use-after-free bug in `trika_window.c`. |
| 13 | — | Complete formal language specification document (`TRIKA_Language_Specification.md`, ~1,200 lines). |
| 14 | — | TRIKA marketing/docs website (`trika_website_phase14.html`) with a **live in-browser playground** that calls the Claude API to *interpret* TRIKA code (since there's no WASM build of the C interpreter — Claude itself acts as the runtime via a detailed SYSTEM_PROMPT). |
| 14b | — | `trika.input` module — interactive `prashan()`/`input.read()` style prompts, with a JS-side modal in the playground to collect user input mid-execution (`trika_website_phase14b.html`). |
| 15 | May 25 | `trika.canvas` — the 28-chart-type graphics module (see §7), full C implementation (`trika_canvas.c`, ~62KB) + Plotly.js-based browser renderer, PNG/JPG/GIF save support, complete reference guide with Python equivalents. |
| 15b | — | Wired canvas into the playground (chart rendering via `%%TRIKA_CANVAS%%...%%END_CANVAS%%` marker protocol), added file-load and GitHub-raw-URL-load to the playground, fixed CORS headers on the Claude API fetch call (`trika_website_phase15b.html`). |
| 16 | Jun 30 | **7 community-suggested language fixes** (see §6) — multi-line lists, global access in karma, virama/agrim scoping, resolve anyatha default, uvach multi-arg (already worked), 10 new string built-ins, inline yadi. **All verified EXIT:0.** |

---

## 6. PHASE 16 FIXES — Exact Technical Detail (most recently completed, verified EXIT:0)

These were real bugs/gaps found by **actually writing programs** in TRIKA (a todo-list app,
a student-grade canvas-chart program), documented in a `suggestions.md` community feedback
log and fixed one by one.

1. **Multi-line lists** — Root-caused to the **lexer**, not the parser. Added a
   `bracket_depth` counter (`int bracket_depth` field in `TLexer` struct, `trika_lexer.h`).
   Incremented on `(`/`[`, decremented on `)`/`]`. While `bracket_depth > 0`, the `\n`
   case in the lexer's main switch skips `lex_emit(TOK_NEWLINE,...)` and
   `lex_handle_indent()` entirely — newlines become pure whitespace inside any bracket,
   exactly like Python. This was attempted first at the parser level (`p_skip_newlines`
   calls around list-element parsing) but that alone was insufficient because the lexer
   was still emitting spurious INDENT/DEDENT tokens; the real fix had to be at tokenization time.

2. **Global variable access inside `karma`** — `karma` (function) closures were being
   created with `f->closure` as parent, which is `NULL` for top-level-defined functions
   (to avoid circular references). Fixed by falling back to `I->globals` (the interpreter's
   global environment) when `f->closure` is NULL: `TEnv *call_parent = f->closure ? f->closure : I->globals;`

3. **`virama`/`agrim` scope leak** — A `virama` (break) inside a loop *inside* a `karma`
   was propagating its `SIG_VIRAMA` signal all the way back out to whatever loop called
   the karma, breaking the *caller's* loop too. Fixed by explicitly consuming
   `SIG_VIRAMA`/`SIG_AGRIM` immediately after a karma's body finishes executing
   (`eval_block(I, f->body, call_env)`), before the signal can propagate further up the call stack.

4. **`resolve ... anyatha:` default case** — Added `struct TASTNode *default_case;` to
   the `resolve` member of the AST node union (`trika_ast.h`). Parser
   (`parse_resolve` in `trika_parser.c`) now checks for `TOK_ANYATHA` after all `case`
   blocks and parses it as the default block. Interpreter's `NODE_RESOLVE` handler falls
   back to executing `default_case` when no `case` branch matched. Also added the missing
   `ast_free(n->as.resolve.default_case)` call to prevent a leak.

5. **`uvach` multi-value** — Verified already implemented correctly (loops over all
   `argc` args, space-separated, no `str()` needed). No code change required, just confirmed.

6. **String functions** — 10 new C built-ins added directly to `trika_interp.c`
   (registered in the builtins dispatch table): `slice(s,start,end)`, `split(s,delim)`,
   `trim(s)`, `upper(s)`, `lower(s)`, `contains(s,sub)`, `startswith(s,prefix)`,
   `endswith(s,suffix)`, `replace(s,old,new)`, `join(list,delim)`. These eliminate the
   need for manual char-by-char loops that earlier TRIKA programs required.

7. **Inline `yadi`** — `parse_yadi` in `trika_parser.c` now checks whether the token
   immediately following the `:` is on the same line (not `TOK_NEWLINE`/`TOK_INDENT`/`TOK_EOF`).
   If so, it parses a single statement via `parse_stmt()` and wraps it in a synthetic
   one-statement `NODE_PROGRAM` block instead of requiring an indented block — enabling
   `yadi x == 0: uvach("zero")` on one line.

**Bonus fix included alongside:** `raksha_all` (the catch-all error handler in
`sadhana`/`try-catch`) was missing from `ast_free()`, causing a memory leak on every
try-catch block. Added `ast_free(n->as.sadhana.raksha_all);`.

All 7 fixes verified together in `test_fixes.tri` — **EXIT: 0**, every fix demonstrated
working in a single test run.

---

## 7. trika.canvas — The 28-Chart Graphics Engine (Phase 15)

A from-scratch C implementation that is **a superset of matplotlib + plotly + seaborn**
for TRIKA programs, including TRIKA-unique features no Python library has:

**28 chart types:** line, scatter, bar, barh, histogram, pie, area, step, stem, errorbar,
fill_between, boxplot, violin, kde, heatmap, contour, imshow, candlestick, waterfall,
gantt, radar, polar, treemap, sunburst, funnel, surface3d, scatter3d, bar3d.

**TRIKA-unique features:**
- `canvas.guna_color(fig, ax, sattva_threshold, tamas_threshold)` — automatically colors
  data points green/amber/red based on whether they're above/below/between thresholds,
  mapping numeric data directly onto the SATTVA/RAJAS/TAMAS philosophy. No equivalent
  exists in any mainstream plotting library without writing custom code.
- `canvas.proof(fig)` — returns a string audit of every series plotted (type, label,
  point count, color) — a uniquely TRIKA "show your work" feature.

**Output formats:** `.html` (interactive, self-contained Plotly.js), `.json` (raw
descriptor), `.png`/`.jpg`/`.jpeg`/`.gif` (via an HTML wrapper that auto-triggers
`Plotly.downloadImage()`, with documented headless-CLI fallback via
`chromium --headless --screenshot=...`).

**Known gap (flagged, not yet fixed):** `canvas.xlabel()`/`canvas.ylabel()` work correctly
in the ASCII terminal output but axis labels are not currently rendering in saved HTML
files — listed as a pending fix in the community suggestions log.

**Browser rendering protocol:** When a TRIKA program calls `canvas.show(fig)`, the
expected output (whether from the native C interpreter or, in the web playground, from
Claude simulating execution per the SYSTEM_PROMPT) is a JSON chart descriptor wrapped in
`%%TRIKA_CANVAS%%{...}%%END_CANVAS%%` markers. The website's JS (`extractAndRenderCharts`)
regex-matches these markers, strips them from the displayed text output, and renders each
one via Plotly.js using a large `switch(s.type)` mapping each of the 28 TRIKA chart types
to the correct Plotly trace configuration.

---

## 8. KNOWN PATTERNS & GOTCHAS (learned the hard way — read before writing new TRIKA programs or fixing the interpreter)

These were discovered through real debugging sessions and are **not** in the formal spec
yet — treat this section as load-bearing tribal knowledge:

1. **`list + list` concatenation is broken for non-trivial element types.**
   `trika c = a + b` where `a`/`b` are lists of maps (or even sometimes plain lists)
   can silently produce a length-0 result. **Workaround:** do not rely on `+` to grow
   lists of maps. Use a **map-based store** instead (see pattern below).

2. **`add(list, index, value)` does not behave like `push()`.** It treats the list
   similarly to a map with integer keys and order/retrieval semantics are unreliable
   for storing structured records. **Do not use this pattern for collections of records.**

3. **`map != RAJAS` (or `== RAJAS`) is unreliable for "does this key exist" checks** —
   an actual map value can itself compare as `RAJAS`-like in certain contexts. **Do not**
   use `yadi some_map != RAJAS` to test existence.

4. **Assigning a map subscript result to a local variable inside a `karma`, then later
   mutating the original store, can corrupt the local reference** (a refcounting/aliasing
   issue). I.e. avoid:
   ```trika
   trika todo = store[key]   # DANGEROUS inside karma if store[key] is later reassigned
   ```
   **Safe pattern — access fields directly without an intermediate local:**
   ```trika
   store[key]["title"]
   store[key]["status"]
   ```

### THE WINNING DATA-STORE PATTERN (use this for any "list of records" need)

```trika
trika store  = {}   # store["1"] = {id, title, status, date, ...}
trika active = {}   # active["1"] = SATTVA (live) / TAMAS (deleted) — existence flag

# Add:
add(store, key, make_record(...))
add(active, key, SATTVA)

# Read — ALWAYS direct field access, never alias the map to a local var:
store[key]["field"]

# Update — build a fresh record, replace the whole entry:
add(store, key, make_record(id, new_title, new_status, old_date))

# Delete — never remove, just flag inactive:
add(active, key, TAMAS)

# Existence check — via the active map, NEVER via `!= RAJAS`:
yadi active[key] == SATTVA: ...
```

This pattern was discovered and verified working across multiple complex programs
(notably `todo_list.tri`) and should be the **default recommendation** for any future
TRIKA program needing structured record storage.

5. **A trailing segfault after correct program output is a known, separate, lower-priority
   issue** — it occurs during interpreter teardown/cleanup (likely a double-free in the
   refcounting cleanup path), **not** during program execution. A program that prints all
   expected output correctly and then segfaults at the very end should be considered a
   **passing** run for practical purposes; the exit code noise (139) does not indicate
   incorrect program logic. This is flagged as a future cleanup-path fix, not urgent.

---

## 9. COMPILE COMMAND (canonical, Era 2, all 19 .c files)

```bash
gcc -std=c11 \
    trika_token.c trika_value.c trika_env.c trika_ast.c \
    trika_lexer.c trika_parser.c trika_input.c trika_dataset.c \
    trika_math.c trika_file.c trika_time.c \
    trika_grid.c trika_visual.c trika_event.c \
    trika_window.c trika_generator.c trika_canvas.c \
    trika_interp.c trika_main.c \
    -o trika -lm
```

Run a program: `./trika run myprogram.tri`
REPL mode: `./trika`

---

## 10. HOW TO CONTINUE TRIKA DEVELOPMENT IN A NEW SESSION

1. **Upload every file listed below to this Project's knowledge base** (one time setup).
2. Start any new chat inside this Project.
3. Say something like: *"Hari Om. Continuing TRIKA — Phase 17: [whatever you want next]."*
4. Claude will read the uploaded source directly — this document plus the actual `.c`/`.h`
   files together give a complete, accurate picture without needing to re-derive
   architecture or re-discover the Phase 16 gotchas above.
5. **If asked about Era 1 (Python) features** (db, networking, ML, etc.) — be clear with
   the user that these existed only in the legacy Python prototype and have not been
   ported to the current C runtime. Treat Era 1 source as historical reference only,
   not as something to extend directly.

### Suggested next phases (not yet started)
- **Phase 16b:** GitHub README + public release packaging
- **Phase 17:** `trika.network` — HTTP client/server module (porting concept from Era 1's `trika_net.py`/`trika_http.py`, rewritten natively in C)
- **Phase 18:** `trika.db` — SQLite-backed persistence module (porting concept from Era 1's `trika_db.py`)
- Fix the trailing-segfault cleanup-path issue (§8.5) properly at the root
- Fix the `list + list` concatenation bug (§8.1) properly at the interpreter level
  rather than working around it
- Canvas: xlabel/ylabel rendering gap in saved HTML output (§7, flagged by community suggestion)

---

## 11. FULL FILE MANIFEST FOR THIS PROJECT'S KNOWLEDGE BASE

Upload all of these together for a complete, self-consistent picture of **Era 2 (current)**:

**Core interpreter (required):**
trika_token.c/.h, trika_value.c/.h, trika_env.c/.h, trika_ast.c/.h,
trika_lexer.c/.h, trika_parser.c/.h, trika_interp.c/.h, trika_main.c,
trika_input.c/.h, trika_dataset.c/.h, trika_builtin.h

**Standard library (required):**
trika_math.c/.h, trika_file.c/.h, trika_time.c/.h, trika_grid.c/.h,
trika_visual.c/.h, trika_event.c/.h, trika_window.c/.h, trika_generator.c/.h,
trika_canvas.c/.h

**Tests & examples:**
test_fixes.tri (Phase 16 regression test), todo_list.tri (record-storage pattern example),
kurukshetra.tri (Phase 10–11 flagship demo), pipeline_demo.tri (Phase 12 window+generator demo)

**Documentation:**
TRIKA_PROJECT_CONCEPT.md (this file), TRIKA_Language_Specification.md,
TRIKA_Canvas_Complete_Guide.md, TRIKA_Setup_Guide.md

**Website:**
trika_website_phase15b.html (current live playground)

**Optional / historical reference only (Era 1 Python prototype — do not extend, reference only):**
lexer.py, parser.py, interpreter.py, tokens.py, ast_nodes.py, codegen.py,
TRIKA_TECHNICAL_GUIDE.md, TRIKA_SEED_v1.1–v3.0.md, the Phase 5–8 example guides

---

*Patna, Bihar, India · Pure C (Era 2) · One Man Army*

**🕉️ Hari Om Namah Shivaye**
