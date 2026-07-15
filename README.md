<div align="center">

# 🕉️ TRIKA

### The World's First Ternary Programming Language

*Born in Patna, Bihar, India · Pure C · One Man Army*

**"You have a right to perform your duty, but not to the fruits of action."**
*— Bhagavad Gita 2.47*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Language: C](https://img.shields.io/badge/Language-C11-blue.svg)]()
[![Platform: Windows](https://img.shields.io/badge/Platform-Windows-lightblue.svg)]()
[![Platform: Linux](https://img.shields.io/badge/Platform-Linux-orange.svg)]()
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero-green.svg)]()

</div>

---

## What is TRIKA?

TRIKA is the **world's first ternary programming language** — built from scratch in pure C with zero external dependencies. Unlike every other programming language built on binary `true`/`false` logic, TRIKA's foundational logic is **three-valued**, rooted in the philosophy of the **Bhagavad Gita**.

Every value in TRIKA resolves to one of three **gunas** (qualities):

| Guna | Value | Meaning |
|------|-------|---------|
| 🟢 **SATTVA** | `+1` | Goodness, clarity, success, truth |
| 🟡 **RAJAS** | `0` | Activity, neutrality, in-progress |
| 🔴 **TAMAS** | `-1` | Inertia, failure, error |

---

## Why TRIKA?

```trika
# Every comparison returns SATTVA, RAJAS, or TAMAS — not just true/false
trika result = network.get("https://api.example.com/data")

resolve result["guna"]:
    case SATTVA: uvach("Request succeeded!")
    case RAJAS:  uvach("Redirected — following...")
    case TAMAS:  uvach("Request failed")
    anyatha:     uvach("Unknown state")
```

This is **philosophically meaningful code**. The HTTP response is not just success/failure — it has a **quality**. 2xx is SATTVA (goodness), 3xx is RAJAS (action needed), 4xx/5xx is TAMAS (darkness).

---

## Sanskrit Keywords

TRIKA uses Sanskrit keywords so that **the code itself carries philosophical meaning**:

| TRIKA | Meaning | Equivalent |
|-------|---------|------------|
| `trika` | declare | `var` |
| `karma` | action/function | `function` / `def` |
| `gyan` | knowledge/import | `import` |
| `uvach` | spoke/print | `print` |
| `phal` | fruit/return | `return` |
| `yadi` | if | `if` |
| `anyatha` | otherwise | `else` |
| `yavat` | while | `while` |
| `prati` | for each | `for` |
| `resolve` | discern | `switch` |
| `virama` | pause/break | `break` |
| `agrim` | forward/continue | `continue` |
| `sadhana` | practice/try | `try` |
| `raksha` | protect/catch | `catch` |
| `sankat` | crisis/throw | `throw` |
| `vivek` | wisdom/query | single-pass query |

---



### Run a program
```bash
trika run examples/hello.tri
trika run examples/server.tri
trika run tests/test_fixes.tri
```

---

## Hello World

```trika
uvach("Hari Om Namah Shivaye!")
uvach("TRIKA — The Ternary Language")
darshan(SATTVA)
```

Output:
```
Hari Om Namah Shivaye!
TRIKA — The Ternary Language
🟢 SATTVA (+1)
```

---

## Language Features

### Variables and Types
```trika
trika x     = 42           # integer
trika pi    = 3.14159      # float
trika name  = "Arjuna"     # string
trika flag  = SATTVA       # ternary state
trika list  = [1, 2, 3]    # list (multi-line supported)
trika map   = {}           # map
add(map, "key", "value")   # map operations
```

### Multi-line Lists
```trika
trika scores = [
    72, 85, 91,
    63, 78, 88,
    54, 76, 82
]
```

### Functions (karma)
```trika
karma add(trika a, trika b):
    phal a + b

trika result = add(10, 20)
uvach("Sum: " + str(result))
```

### Conditionals
```trika
yadi x > 0: uvach("positive")    # inline yadi
yadi x == 0:
    uvach("zero")
anyatha:
    uvach("negative")
```

### Loops
```trika
trika i = 0
yavat i < 5:
    uvach(str(i))
    i = i + 1

prati item in [1, 2, 3, 4, 5]:
    uvach(str(item))
```

### Ternary Switch
```trika
resolve status:
    case SATTVA: uvach("Success")
    case RAJAS:  uvach("Pending")
    case TAMAS:  uvach("Failed")
    anyatha:     uvach("Unknown")
```

### Error Handling
```trika
sadhana:
    trika result = risky_operation()
raksha_sattva:
    uvach("Succeeded!")
raksha_tamas:
    uvach("Error caught")
antim:
    uvach("Always runs")
```

### String Functions
```trika
uvach(upper("dharma"))           # DHARMA
uvach(slice("Kurukshetra", 0, 5)) # Kuruk
uvach(replace("Hello World", "World", "Dharma"))
trika parts = split("a,b,c", ",")
uvach(join(["Hari", "Om"], " "))  # Hari Om
```

---

## Standard Library — 11 Modules

| Module | Import | Key Functions |
|--------|--------|---------------|
| **math** | `gyan trika.math` | sin, cos, sqrt, pow, rand, PI, E, PHI |
| **file** | `gyan trika.file` | read, write, lines, exists, copy, move, ext |
| **time** | `gyan trika.time` | stamp, ms, sleep, format, start/stop/elapsed |
| **grid** | `gyan trika.grid` | create, set, get, neighbors4/8 (cellular automata) |
| **visual** | `gyan trika.visual` | render, SYMBOL/EMOJI/BLOCK modes |
| **event** | `gyan trika.event` | on, emit, off, history (pub/sub) |
| **window** | `gyan trika.window` | sliding window algorithms |
| **generator** | `gyan trika.generator` | fibonacci, tribonacci, custom sequences |
| **canvas** | `gyan trika.canvas` | **28 chart types** (line, bar, pie, heatmap, 3D...) |
| **network** | `gyan trika.network` | HTTP GET/POST, serve (raw sockets, zero dependencies) |
| **database** | `gyan trika.database` | CRUD for memory/CSV/JSON/SQLite/MySQL/PostgreSQL/Redis |

---

## HTTP Server in 10 lines

```trika
gyan trika.network

karma handler(trika req):
    trika path = req["path"]
    yadi path == "/":
        phal network.respond(200, "Hari Om!", "text/plain")
    anyatha:
        phal network.respond(404, "Not found", "text/plain")

network.serve(8080, "handler")
```

---

## Database in 5 lines

```trika
gyan trika.database
trika conn = database.connect("myapp.db", database.SQLITE)
trika row  = {}
add(row, "name", "Arjuna")
add(row, "score", 95)
database.insert(conn, "warriors", row)
uvach("rows: " + str(database.count(conn, "warriors")))
```

---

## trika.canvas — 28 Chart Types

```trika
gyan trika.canvas
trika fig = canvas.figure("Dharma Chart", 800, 500)
trika ax  = canvas.subplot(fig, 1, 1, 1)
canvas.plot(fig, ax, [1,2,3,4,5], [10,25,15,40,20], "Karma", "blue")
canvas.title(fig, ax, "The Path of Dharma")
canvas.show(fig)
canvas.save(fig, "dharma.html")
```

**Chart types:** line, scatter, bar, barh, histogram, pie, area, step,
stem, errorbar, fill_between, boxplot, violin, kde, heatmap, contour,
imshow, candlestick, waterfall, gantt, radar, polar, treemap, sunburst,
funnel, surface3d, scatter3d, bar3d

**TRIKA-unique:** `canvas.guna_color()` — colors data points
SATTVA/RAJAS/TAMAS based on value thresholds. No equivalent in matplotlib.

---
---

## Database Backends

| Backend | Flag | Library | URL |
|---------|------|---------|-----|
| Memory | (always) | none | `memory://` |
| CSV | (always) | none | `csv://path/` |
| JSON | (always) | none | `json://path/` |
| SQLite | `-DTRIKA_SQLITE` | `sqlite3.c` | `sqlite://file.db` |
| MySQL | `-DTRIKA_MYSQL` | libmysqlclient | `mysql://user:pass@host/db` |
| PostgreSQL | `-DTRIKA_POSTGRES` | libpq | `postgres://user:pass@host/db` |
| Redis | `-DTRIKA_REDIS` | hiredis | `redis://host:6379` |
| MariaDB | `-DTRIKA_MARIADB` | libmariadb | `mariadb://user:pass@host/db` |

---

## Zero External Dependencies

TRIKA is designed to be **completely self-contained**:

- No Python runtime
- No Node.js
- No package manager
- No install scripts
- Just `gcc` and your source files

The only optional dependency is `sqlite3.c` — a single file download from sqlite.org, included directly in your build. Everything else — HTTP networking, file I/O, math, graphics — is pure C.

---

## Platform Support

| Platform | Compile | Tested |
|----------|---------|--------|
| Windows (MinGW-w64) | `gcc -lm -lws2_32` | ✅ Confirmed |
| Linux (gcc) | `gcc -lm` | ✅ Confirmed |
| macOS (clang) | `clang -lm` | Should work |

---

## Philosophy

TRIKA is not just a programming language. It is a **meditation on computation**.

When you write `karma` instead of `function`, you are reminded that every action has consequences. When you write `gyan trika.math`, you are importing not just functions but **knowledge**. When your HTTP request returns `TAMAS`, you know it is not just an error — it is **inertia**, **darkness**, something to overcome.

The Bhagavad Gita teaches that the universe operates through three gunas — Sattva, Rajas, Tamas. Every output of every computation in TRIKA reflects this truth.

---

## License

MIT License — see [LICENSE](LICENSE)

---

## Author

**One Man Army** · Patna, Bihar, India

*Building the future of computation, one guna at a time.*

---

<div align="center">

**🕉️ Hari Om Namah Shivaye**

*TRIKA — Where code meets dharma*

</div>
