# 🕉️ TRIKA Language Specification
## Phase 13 — Complete Reference

> *"The universe operates in three modes — SATTVA, RAJAS, TAMAS.  
> Every particle, every thought, every computation has these qualities.  
> TRIKA makes them the foundation of the language itself."*

**Born in Patna, Bihar, India. Built in Pure C. One Man Army.**

---

## Table of Contents

1. [Philosophy](#1-philosophy)
2. [The Three States](#2-the-three-states)
3. [Syntax Overview](#3-syntax-overview)
4. [Keywords](#4-keywords-sanskrit-reference)
5. [Variables and Types](#5-variables-and-types)
6. [Operators](#6-operators)
7. [Control Flow](#7-control-flow)
8. [Functions — karma](#8-functions--karma)
9. [Classes — swaroop](#9-classes--swaroop)
10. [Error Handling — sadhana/raksha](#10-error-handling--sadhanaraksha)
11. [Standard Library](#11-standard-library)
12. [Window Primitive](#12-trika-window---position-aware-stream-window)
13. [Generator Primitive](#13-trika-generator---generative-pattern-primitive)
14. [Three-Level Certainty Architecture](#14-three-level-certainty-architecture)


---

## 1. Philosophy

TRIKA is the world's first ternary programming language rooted in the Bhagavad Gita.

Binary gives you 0 and 1. True and false. On and off. But the world is not binary. A decision can be correct, incorrect, or *undecided*. A test can pass, fail, or *unknown*. A warrior can fight, flee, or *stand still*. TRIKA gives you all three — and the Gita already named them.

The keywords are not decoration. `karma` is not just a function — it is the principle that every action has consequence. `vivek` is not just a query — it is discernment. `sadhana` is not just try/catch — it is spiritual practice. The keywords are philosophy made executable.

---

## 2. The Three States

Every TRIKA value, every decision, every condition operates in three states:

```
SATTVA  (+1)  — Goodness, clarity, dharma, truth, success
RAJAS   ( 0)  — Passion, action, undecided, in-progress
TAMAS   (-1)  — Darkness, inertia, adharma, failure, error
```

These are the **three gunas** from Bhagavad Gita 14.5:

> *"Sattva, Rajas, and Tamas — these three gunas born of Prakriti bind the imperishable soul to the body."*

### Usage

```trika
# Assign guna states directly
trika status = SATTVA
trika result = TAMAS
trika pending = RAJAS

# Compare with ==
yadi status == SATTVA:
    uvach("Dharma holds")

# darshan prints with emoji and numeric value
darshan(SATTVA)   # → 🟢 SATTVA (+1)
darshan(RAJAS)    # → 🟡 RAJAS  (0)
darshan(TAMAS)    # → 🔴 TAMAS  (-1)
```

### Return Values

In TRIKA, functions return **SATTVA** for success, **TAMAS** for failure, **RAJAS** for pending/uncertain. This replaces boolean true/false with three-valued logic.

---

## 3. Syntax Overview

TRIKA uses **indentation** for block structure (like Python). Comments begin with `#`.

```trika
# This is a comment

# Variable declaration
trika name = "Arjuna"
trika age  = 25
trika score = 90.5
trika active = SATTVA

# Function definition
karma greet(trika who):
    uvach("Hari Om " + who)
    phal SATTVA

# Call it
greet("Arjuna")
```

### File Extension

TRIKA programs use the `.tri` extension.

---

## 4. Keywords — Sanskrit Reference

All keywords are Sanskrit or Sanskrit-derived. This is intentional — the language reflects the philosophy it computes.

| Keyword | Equivalent | Sanskrit Meaning |
|---------|-----------|-----------------|
| `trika` | `var` / `let` | Three / ternary / declare |
| `karma` | `function` / `def` | Action with consequence |
| `gyan` | `import` | Knowledge / module |
| `uvach` | `print` | Spoke / said |
| `darshan` | `inspect` | Sacred seeing |
| `phal` | `return` | Fruit / result |
| `yadi` | `if` | If / when |
| `anyatha` | `else` | Otherwise |
| `yavat` | `while` | As long as |
| `prati` | `for` | Every / each |
| `resolve` | `switch` / `match` | Ternary resolution |
| `swaroop` | `class` | Form / nature |
| `sadhana` | `try` | Spiritual practice |
| `raksha` | `catch` | Protection / shield |
| `antim` | `finally` | The last / ultimate |
| `sankat` | `raise` / `throw` | Crisis / that which arises |
| `vivek` | `filter + map` | Discernment |
| `virama` | `break` | Stop / halt |
| `agrim` | `continue` | Forward / next |

### Built-in Values

| Value | Meaning | Numeric |
|-------|---------|---------|
| `SATTVA` | True / success / goodness | +1 |
| `RAJAS` | Undecided / pending / neutral | 0 |
| `TAMAS` | False / failure / darkness | -1 |

### Built-in Functions

| Function | Description |
|----------|-------------|
| `uvach(x)` | Print value to console |
| `darshan(x)` | Inspect/display with type and guna symbol |
| `str(x)` | Convert to string |
| `len(x)` | Length of string, list, or map |
| `type(x)` | Type name as string |
| `add(map, key, val)` | Add to map |
| `vivek(collection)` | Single-pass query — count, sum, avg, min, max, sorted, filtered |
| `TINV(x)` | Ternary NOT |
| `TMIN(x, y)` | Ternary AND (minimum) |
| `TMAX(x, y)` | Ternary OR (maximum) |

---

## 5. Variables and Types

### Declaration

```trika
trika x = 42           # integer
trika pi = 3.14        # float
trika name = "Shiva"   # string
trika flag = SATTVA    # trika/guna state
trika nums = [1, 2, 3] # list
trika m = {             # map (inline)
    "name": "Arjuna",
    "age": 25
}
```

### Types

| Type | Example | Notes |
|------|---------|-------|
| Integer | `42`, `-7`, `0` | 64-bit signed |
| Float | `3.14`, `-2.5` | 64-bit double |
| String | `"Hari Om"` | UTF-8, double-quoted |
| Trika | `SATTVA`, `RAJAS`, `TAMAS` | Ternary state |
| List | `[1, 2, 3]` | Dynamic, mixed types |
| Map | `{"key": val}` | String keys |
| Null | — | Internal only |

### Type Checking

```trika
trika x = 42
uvach(type(x))          # "int"
uvach(type("hello"))    # "string"
uvach(type(SATTVA))     # "trika"
uvach(type([1,2,3]))    # "list"
```

### Lists

```trika
trika nums = [10, 20, 30, 40, 50]
uvach(len(nums))          # 5
uvach(nums[0])            # 10
uvach(nums[2])            # 30

# Lists are dynamic — any type
trika mixed = [1, "two", SATTVA, 3.14]
```

### Maps

```trika
trika person = {
    "name": "Arjuna",
    "city": "Patna"
}

uvach(person["name"])     # Arjuna
add(person, "age", 25)    # add new key
uvach(person["age"])      # 25
```

---

## 6. Operators

### Arithmetic

```trika
trika a = 10 + 3    # 13
trika b = 10 - 3    # 7
trika c = 10 * 3    # 30
trika d = 10 / 3    # 3.333...
trika e = 10 % 3    # 1  (modulo)
```

### Comparison

```trika
trika x = 10 == 10   # SATTVA
trika y = 10 != 5    # SATTVA
trika z = 10 > 5     # SATTVA
trika w = 10 < 5     # TAMAS
trika v = 10 >= 10   # SATTVA
trika u = 10 <= 9    # TAMAS
```

### Logical

```trika
trika a = SATTVA && RAJAS   # RAJAS  (AND)
trika b = SATTVA || TAMAS   # SATTVA (OR)
trika c = !SATTVA            # TAMAS  (NOT)
```

### Ternary Gates (pure ternary logic)

```trika
darshan(TINV(SATTVA))           # TAMAS
darshan(TINV(TAMAS))            # SATTVA
darshan(TINV(RAJAS))            # RAJAS

darshan(TMIN(SATTVA, RAJAS))    # RAJAS  (AND minimum)
darshan(TMIN(SATTVA, TAMAS))    # TAMAS

darshan(TMAX(SATTVA, TAMAS))    # SATTVA (OR maximum)
darshan(TMAX(RAJAS,  TAMAS))    # RAJAS
```

### String Concatenation

```trika
trika greeting = "Hari Om " + "Namah Shivaye"
uvach(greeting)
```

---

## 7. Control Flow

### yadi / anyatha (if / else)

```trika
trika score = 85

yadi score >= 90:
    uvach("SATTVA — Excellent")
anyatha:
    yadi score >= 70:
        uvach("RAJAS — Good")
    anyatha:
        uvach("TAMAS — Needs work")
```

### resolve (switch on ternary state)

```trika
trika state = SATTVA

resolve state:
    case SATTVA:
        uvach("Dharma holds — " + str(pct) + "%")
    case RAJAS:
        uvach("Battle undecided")
    case TAMAS:
        uvach("Adharma rises — retreat and reflect")
```

### yavat (while loop)

```trika
trika count = 0
yavat count < 5:
    uvach(count)
    count = count + 1
```

### prati (for loop)

```trika
# Range loop
prati i = 0 to 5:
    uvach(i)          # 0, 1, 2, 3, 4

# Loop over list
trika names = ["Arjuna", "Krishna", "Bhishma"]
prati name in names:
    uvach(name)

# Loop over string (each character)
prati c in "Shiva":
    uvach(c)          # S, h, i, v, a

# Loop over map (keys)
trika warrior = {"name": "Arjuna", "weapon": "Gandiva"}
prati key in warrior:
    uvach(key + ": " + warrior[key])

# virama — break
prati i = 0 to 10:
    yadi i == 5:
        virama
    uvach(i)

# agrim — continue
prati i = 0 to 10:
    yadi i % 2 == 0:
        agrim
    uvach(i)    # prints only odd numbers
```

---

## 8. Functions — karma

### Basic Definition

```trika
karma add(trika a, trika b):
    phal a + b

trika result = add(10, 20)
uvach(result)    # 30
```

### No Parameters

```trika
karma chant():
    uvach("Hari Om Namah Shivaye")
    phal SATTVA

chant()
```

### Multiple Return Paths

```trika
karma classify_score(trika score):
    yadi score >= 90:
        phal SATTVA
    anyatha:
        yadi score >= 50:
            phal RAJAS
        anyatha:
            phal TAMAS

darshan(classify_score(95))    # 🟢 SATTVA
darshan(classify_score(70))    # 🟡 RAJAS
darshan(classify_score(30))    # 🔴 TAMAS
```

### Recursive Functions

```trika
karma factorial(trika n):
    yadi n <= 1:
        phal 1
    phal n * factorial(n - 1)

uvach(factorial(5))    # 120
```

### Functions as First-Class Values

```trika
karma apply(trika fn_name, trika value):
    # Functions are values — callable by name
    phal value * 2

trika result = apply("double", 21)
uvach(result)    # 42
```

---

## 9. Classes — swaroop

`swaroop` defines a class. `init` is the constructor. `gyan` refers to the instance (`self`).

### Basic swaroop

```trika
swaroop Warrior:
    karma init(trika name, trika weapon):
        gyan.name   = name
        gyan.weapon = weapon
        gyan.status = RAJAS    # starts undecided

    karma fight():
        uvach(gyan.name + " fights with " + gyan.weapon)
        gyan.status = SATTVA
        phal SATTVA

    karma retreat():
        gyan.status = TAMAS
        phal TAMAS

    karma status_report():
        resolve gyan.status:
            case SATTVA:
                uvach(gyan.name + " prevails — SATTVA")
            case RAJAS:
                uvach(gyan.name + " in battle — RAJAS")
            case TAMAS:
                uvach(gyan.name + " retreated — TAMAS")

# Create instance
trika arjuna = Warrior("Arjuna", "Gandiva")
arjuna.fight()
arjuna.status_report()

# Access fields
uvach(arjuna.name)     # Arjuna
uvach(arjuna.weapon)   # Gandiva
darshan(arjuna.status) # 🟢 SATTVA
```

### swaroop with State Management

```trika
swaroop Payment:
    karma init(trika amount):
        gyan.amount = amount
        gyan.status = RAJAS    # pending

    karma approve():
        gyan.status = SATTVA
        uvach("Payment approved: " + str(gyan.amount))

    karma reject():
        gyan.status = TAMAS
        uvach("Payment rejected")

    karma is_complete():
        phal gyan.status != RAJAS

trika p = Payment(1000)
p.approve()
darshan(p.is_complete())    # 🟢 SATTVA
```

---

## 10. Error Handling — sadhana/raksha

`sadhana` = try, `raksha` = catch, `antim` = finally, `sankat` = raise.

```trika
# Basic try/catch
sadhana:
    uvach("Attempting dharma...")
    trika result = 10 / 0
raksha:
    uvach("Error caught — raksha shields us")
antim:
    uvach("Antim — this always runs")
```

### Catch by Guna State

```trika
sadhana:
    trika x = risky_operation()
raksha SATTVA:
    uvach("Recovered gracefully")
raksha RAJAS:
    uvach("Partial recovery")
raksha TAMAS:
    uvach("Fatal — cannot recover")
raksha:
    uvach("Any error caught here")
```

### Raising Errors — sankat

```trika
karma safe_divide(trika a, trika b):
    sadhana:
        yadi b == 0:
            sankat("Cannot divide by zero in dharma")
        phal a / b
    raksha:
        uvach("Division failed")
        phal TAMAS

trika r1 = safe_divide(10, 2)
uvach(r1)      # 5
trika r2 = safe_divide(10, 0)
darshan(r2)    # 🔴 TAMAS
```

### Nested sadhana

```trika
sadhana:
    sadhana:
        sankat("Inner crisis")
    raksha:
        uvach("Inner raksha caught it")
    uvach("Outer sadhana continues")
raksha:
    uvach("Outer raksha — uncaught inner")
```

---

## 11. Standard Library

Import any module with `gyan`:

```trika
gyan trika.math
gyan trika.file
gyan trika.time
gyan trika.grid
gyan trika.visual
gyan trika.event
gyan trika.window
gyan trika.generator
```

---

### trika.math — Sacred Mathematics

```trika
gyan trika.math

# Constants
uvach(math.PI)      # 3.14159265358979...
uvach(math.E)       # 2.71828182845904...
uvach(math.PHI)     # 1.61803398874989...  (Golden Ratio)
uvach(math.SQRT2)   # 1.41421356237309...

# Core functions
uvach(math.abs(-5))           # 5
uvach(math.sqrt(16))          # 4.0
uvach(math.pow(2, 10))        # 1024.0
uvach(math.floor(3.7))        # 3
uvach(math.ceil(3.2))         # 4
uvach(math.round(3.5))        # 4

# Trigonometry
uvach(math.sin(math.PI / 2))  # 1.0
uvach(math.cos(0))            # 1.0
uvach(math.deg(math.PI))      # 180.0
uvach(math.rad(180))          # 3.14159...

# Range functions
uvach(math.max(10, 20))       # 20
uvach(math.min(10, 20))       # 10
uvach(math.clamp(15, 0, 10))  # 10 (clamped to max)

# Geometry
uvach(math.dist(0, 0, 3, 4))  # 5.0 (Pythagorean distance)
uvach(math.lerp(0, 100, 0.5)) # 50.0 (linear interpolation)

# Ternary sign
darshan(math.sign(5))         # 🟢 SATTVA (+1)
darshan(math.sign(-3))        # 🔴 TAMAS  (-1)
darshan(math.sign(0))         # 🟡 RAJAS  (0)

# Random (seed 108 = sacred)
math.seed(108)
uvach(math.rand(0, 100))      # random float in [0, 100]
```

---

### trika.file — Sacred Texts

```trika
gyan trika.file

# Write a sacred text
file.write("dharma.txt", "Gita 2.47: Do your duty")

# Read it back
trika content = file.read("dharma.txt")
uvach(content)

# Append to log
file.append("battle.log", "Day 1: Arjuna hesitates")
file.append("battle.log", "Day 18: Dharma prevails")

# Read line by line
trika lines = file.lines("battle.log")
prati line in lines:
    uvach(line)

# File operations
darshan(file.exists("dharma.txt"))    # 🟢 SATTVA
uvach(file.size("dharma.txt"))        # byte count
file.copy("dharma.txt", "backup.txt")
file.delete("backup.txt")

# Directory operations
file.mkdir("reports")
trika entries = file.list(".")        # list current directory

# Path operations
uvach(file.join("reports", "day1.txt"))   # reports/day1.txt
uvach(file.basename("reports/day1.txt"))  # day1.txt
uvach(file.dirname("reports/day1.txt"))   # reports
```

---

### trika.time — Simulation Clock

```trika
gyan trika.time

# Wall clock
uvach(time.stamp())         # "2025-01-15 14:32:01"
uvach(time.now())           # Unix timestamp (float)

# Simulation clock (for step-based simulations)
time.reset()
uvach(time.tick())          # 1
uvach(time.tick())          # 2
uvach(time.step())          # 2 (current step)
time.set(100)               # jump to step 100
uvach(time.step())          # 100

# Timer
time.start()
# ... do work ...
trika elapsed = time.stop()
uvach(elapsed)              # milliseconds elapsed

# Sleep
time.sleep(100)             # sleep 100ms

# Human-readable duration
uvach(time.format(3661))    # "1h 1m 1s"
uvach(time.format(90))      # "1m 30s"
```

---

### trika.grid — Cellular Automaton

```trika
gyan trika.grid

# Create 18x18 grid (Kurukshetra has 18 dimensions)
trika g = grid.create(18, 18)

# Fill with RAJAS (undecided)
grid.fill(g, RAJAS)

# Set individual cells
grid.set(g, 0, 0, SATTVA)    # (row, col, value)
grid.set(g, 17, 17, TAMAS)

# Read cell
trika cell = grid.get(g, 0, 0)
darshan(cell)                 # 🟢 SATTVA

# Dimensions
uvach(grid.rows(g))           # 18
uvach(grid.cols(g))           # 18

# Count states
uvach(grid.count(g, SATTVA))  # number of SATTVA cells
uvach(grid.count(g, TAMAS))   # number of TAMAS cells

# Find cells with state
trika sattva_positions = grid.find(g, SATTVA)

# Copy grid (for double-buffering)
trika g2 = grid.copy(g)

# Neighbor counts for guna simulation
trika ns = grid.neighbor_states(g, 9, 9)
uvach(ns["SATTVA"])           # SATTVA neighbors
uvach(ns["TAMAS"])            # TAMAS neighbors
uvach(ns["total"])            # total neighbors (max 8)

# Neighbor lists
trika n4 = grid.neighbors4(g, 9, 9)   # 4 cardinal neighbors
trika n8 = grid.neighbors8(g, 9, 9)   # 8 neighbors

# Bounds check
darshan(grid.valid(g, 0, 0))  # 🟢 SATTVA (valid)
darshan(grid.valid(g, 18, 0)) # 🔴 TAMAS  (out of bounds)

grid.free(g)
grid.free(g2)
```

---

### trika.visual — Render the Battle

```trika
gyan trika.grid
gyan trika.visual

trika g = grid.create(5, 5)
grid.fill(g, RAJAS)
grid.set(g, 2, 2, SATTVA)
grid.set(g, 0, 0, TAMAS)

# Three render modes
visual.mode(visual.SYMBOL)    # S R T (text)
visual.render(g)

visual.mode(visual.EMOJI)     # 🟢 🟡 🔴
visual.render(g)

visual.mode(visual.BLOCK)     # ANSI colored blocks
visual.render(g)

# Bordered render with step counter
visual.render_box(g, 42)

# Stats bar
visual.stats(g)

# Legend
visual.legend()

# Terminal control
visual.clear()
visual.cursor(0, 0)
visual.print_at(5, 10, "Kurukshetra Day 9")

grid.free(g)
```

---

### trika.event — Pub/Sub System

```trika
gyan trika.event

# Define a handler karma
karma on_victory(trika data):
    uvach("JAI! " + data["victor"] + " prevails!")
    uvach("Gita 4.7 — Whenever dharma declines...")

# Register handler
event.on("victory", "on_victory")

# Emit an event
trika data = {"victor": "Pandavas", "day": 18}
event.emit("victory", data)

# Multiple handlers for one event
karma log_event(trika data):
    uvach("[LOG] victory event fired")

event.on("victory", "log_event")

# Remove a handler
event.off("victory", "log_event")

# Check handler count
uvach(event.count("victory"))    # 1

# Event history
trika hist = event.history("victory")

# List all registered events
trika evts = event.list()

# Enable event logging
event.log(SATTVA)

# Clear event
event.clear("victory")

# Clear all events
event.clear_all()
```

---

## 12. trika.window — Position-Aware Stream Window

### The Problem Classic Algorithms Have

Classic sliding window algorithms silently destroy state:

```
String: "abcdyxb"
At repeat 'b' (index 6):
  seen = x       ← WRONG: entire window replaced by 1 character
  All history silently destroyed. Position unknown.
```

### The Trika Window Solution

```
seen = seen[idx+1:] + x  ← slides precisely past the duplicate
Every element carries its ORIGIN INDEX — the position proof.
```

### Three Invariants (Always Maintained)

```
1. seen == stream[left : right+1]       (true contiguous substring)
2. len(seen) == right - left + 1        (no gaps)
3. all elements in seen are unique      (no duplicates)
```

### API

```trika
gyan trika.window

# ── window.run() — one-shot convenience ──────────────────────
trika result = window.run("abcabcbb")
uvach(result["proof"])      # "length=3 at [0:2]"
uvach(result["left"])       # 0
uvach(result["right"])      # 2
uvach(result["length"])     # 3
prati v in result["value"]:
    uvach(v)                # a, b, c
prati p in result["position"]:
    uvach(str(p["char"]) + " @ index " + str(p["idx"]))

# ── window.create() + step-by-step ───────────────────────────
trika w = window.create("abcdyxb")

yavat window.state(w) == RAJAS:
    trika s = window.step(w)
    uvach("right=" + str(window.right(w)) +
          " left=" + str(window.left(w)) +
          " len=" + str(window.length(w)) +
          " → " + s["proof"])

trika best = window.best(w)
uvach(best["proof"])        # "length=6 at [0:5]"

window.free(w)

# ── Accessor functions ────────────────────────────────────────
trika w2 = window.create([1, 2, 3, 1, 2, 4])
window.step(w2)
uvach(window.left(w2))      # current left boundary
uvach(window.right(w2))     # current right position
uvach(window.length(w2))    # current window length
trika seen = window.seen(w2) # list of current window elements
uvach(window.proof(w2))      # full audit string
window.reset(w2)             # reset to start
window.free(w2)

# ── window.scan_all() — all unique windows ────────────────────
trika all = window.scan_all("abcb")
prati win in all:
    uvach(win["proof"])

# ── window.longest() — just the chars ────────────────────────
trika chars = window.longest("abcabcbb")
prati c in chars:
    uvach(c)                # a, b, c
```

### Known Test Cases (All Verified)

| Input | Expected | Proof |
|-------|----------|-------|
| `"abcabcbb"` | length=3 | `length=3 at [0:2]` |
| `"bbbbb"` | length=1 | `length=1 at [0:0]` |
| `"pwwkew"` | length=3 | `length=3 at [2:4]` |
| `"abcdef"` | length=6 | `length=6 at [0:5]` |
| `"abcdyxb"` | length=6 | `length=6 at [0:5]` |
| `"dvdf"` | length=3 | `length=3 at [1:3]` |
| `[1,2,3,1,2,4]` | length=4 | `length=4 at [2:5]` |

### Algorithm Comparison

| Algorithm | Silent Mutation | What Is Lost |
|-----------|----------------|--------------|
| Sliding Window | `seen = x` | Entire window → 1 char |
| Two Pointer | `left += 1` | Valid chars skipped |
| HashMap | `map[c] = right` | Old position overwritten |
| **Trika Window** | `seen[idx+1:]+x` | **NOTHING — position always known** |

> *"Length alone is a claim. Position is the proof."*

---

## 13. trika.generator — Generative Pattern Primitive

### The Principle

Classic algorithms stop when they find a pattern. The Trika Generator continues — the found pattern becomes a seed that generates structure from itself.

```
seed = [1, 1]   →   rule: last + prev   →   1, 1, 2, 3, 5, 8, 13, 21...
                                         →   infinite Fibonacci
                                         →   position always known
```

### API

```trika
gyan trika.generator

# ── Define a rule karma ───────────────────────────────────────
# The rule receives the FULL history list as argument
karma fib_rule(trika history):
    trika n = len(history)
    phal history[n-1] + history[n-2]

# ── generator.create() ───────────────────────────────────────
trika g = generator.create([1, 1], "fib_rule")

# ── generator.next() — advance one step ──────────────────────
trika r = generator.next(g)
uvach(str(r["value"]))       # 2
uvach(str(r["position"]))    # 3
uvach(r["proof"])            # "position=3 generated by 'fib_rule' from seed[len=2]"

# ── generator.take() — n steps at once ───────────────────────
trika batch = generator.take(g, 8)
prati item in batch:
    uvach(str(item["value"]) + " @ pos " + str(item["position"]))

# ── generator.peek() — look without advancing ────────────────
trika next_val = generator.peek(g)
uvach(str(next_val))         # shows next, does NOT advance

# ── generator.rewind() — reset to seed ───────────────────────
generator.rewind(g)
uvach(str(generator.position(g)))   # back to seed_len

# ── generator.history() — all values so far ──────────────────
trika hist = generator.history(g)

# ── generator.seed() — original seed ─────────────────────────
trika seed = generator.seed(g)

# ── generator.free() ─────────────────────────────────────────
generator.free(g)

# ── Convenience: generator.fibonacci(n) ──────────────────────
trika fibs = generator.fibonacci(10)
prati f in fibs:
    uvach(f)    # 1, 1, 2, 3, 5, 8, 13, 21, 34, 55

# ── Convenience: generator.tribonacci(n) ─────────────────────
trika tribs = generator.tribonacci(8)
prati t in tribs:
    uvach(t)    # 1, 1, 2, 4, 7, 13, 24, 44

# ── generator.from_rule() — create + generate + free ─────────
trika values = generator.from_rule([1, 1], "fib_rule", 10)
prati v in values:
    uvach(v)

# ── generator.pattern() — detect repeating period, extend ────
trika stream = [1, 2, 3, 1, 2, 3, 1, 2, 3]
trika next6 = generator.pattern(stream, 6)
prati v in next6:
    uvach(v)    # 1, 2, 3, 1, 2, 3
```

### Rule Karma Design

The rule karma receives the **full history** list. It can look at any past value:

```trika
# Fibonacci — last + previous
karma fib_rule(trika history):
    trika n = len(history)
    phal history[n-1] + history[n-2]

# Tribonacci — last three
karma trib_rule(trika history):
    trika n = len(history)
    phal history[n-1] + history[n-2] + history[n-3]

# Squares — position squared
karma square_rule(trika history):
    trika n = len(history)
    phal n * n

# Guna cycle — sacred ternary progression
karma guna_cycle(trika history):
    trika n = len(history)
    trika last = history[n-1]
    yadi last == SATTVA:
        phal RAJAS
    anyatha:
        yadi last == RAJAS:
            phal TAMAS
        anyatha:
            phal SATTVA
```

### Critical Note

The rule must NOT return `TAMAS` as an error signal. `TAMAS` is a **valid generative value** in TRIKA (used in guna sequences). The generator uses `TV_NULL` (never produced by rule karmas) as the internal error sentinel.

---

## 14. Three-Level Certainty Architecture

TRIKA's deepest design truth — the same principle at every level:

```
The thing contains its own rule.
The rule generates the next thing.
The position is always known.
```

### Level 1 — OCC (One Character Compilation)

One character → one token. No ambiguous token possible. The compiler knows exactly what it is reading before it reads it. Syntactic certainty is enforced by construction, not checked.

### Level 2 — Window Primitive (Semantic Certainty)

Classic algorithms silently mutate state. `seen = x` replaces an entire window with one character — no error, no warning. The Trika Window carries position at every step. Nothing is ever silently lost.

**Semantic certainty at runtime.**

### Level 3 — Generator Primitive (Generative Certainty)

Classic algorithms stop when they find a pattern. TRIKA continues — the found pattern becomes a seed that generates structure. Like Fibonacci: one seed `[1, 1]` + one rule → infinite spiral in shells, galaxies, sunflowers.

**Generative certainty into infinity.**

### The Pipeline

```trika
gyan trika.window
gyan trika.generator

karma fib_rule(trika history):
    trika n = len(history)
    phal history[n-1] + history[n-2]

# Level 2: Window finds the pattern
trika stream = [1, 1, 2, 3, 5, 8, 13, 1, 1, 2, 3]
trika w = window.run(stream)
uvach(w["proof"])    # "length=6 at [1:6]"

# Level 3: Generator extends it forever
trika seed = w["value"]
trika g = generator.create(seed, "fib_rule")
prati i = 0 to 7:
    trika r = generator.next(g)
    uvach("F(" + str(r["position"]) + ") = " + str(r["value"]))
generator.free(g)
```

---

## 15. Run



### Run a Program

```bash
./trika run myprogram.tri
```

### Interactive REPL

```bash
./trika
> trika x = 42
> uvach(x)
42
> darshan(SATTVA)
🟢 SATTVA (+1)
> virama    (or exit)
```



---

## Appendix — The Kurukshetra Simulation

The reference implementation that proves the language works — `kurukshetra.tri` runs an 18×18 cellular automaton for 18 days using five laws of guna dynamics, with nine Gita verses each triggered by data conditions (not timers).

```trika
gyan trika.grid
gyan trika.visual
gyan trika.event
gyan trika.time

# Five Laws of Guna Dynamics:
# Law 1: RAJAS + 2 SATTVA     → SATTVA
# Law 2: RAJAS + 3 TAMAS (no dharma) → TAMAS
# Law 3: SATTVA + 5 TAMAS     → RAJAS
# Law 4: TAMAS + 4 SATTVA     → RAJAS
# Law 5: RAJAS + 3 SATTVA     → SATTVA

# Each Gita verse fires at a DATA THRESHOLD, not a timer.
# The Gita is embedded in the physics — not the UI.
```

This is not an example. It is the proof that every module works together — that the Gita's physics are computationally valid.

---

  🕉️ Hari Om Namah Shivaye
```

---

*TRIKA Language Specification — Phase 13*  
*Patna, Bihar, India*  
*Hari Om Namah Shivaye 🕉️*
