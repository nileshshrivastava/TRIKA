# 🕉️ TRIKA Canvas — Complete Reference Guide
## Phase 15 — All 28 Chart Types

> *"The data contains its own pattern. The canvas reveals it. The position is always known."*

**Every chart. Every command. Every Python equivalent. Every data format.**

---

## How trika.canvas Works

```trika
gyan trika.canvas

# Step 1: Create a figure (canvas)
trika fig = canvas.figure("My Title", width, height)

# Step 2: Create an axis (plot area)
trika ax = canvas.subplot(fig, rows, cols, index)

# Step 3: Add data to the axis
canvas.line(fig, ax, x_list, y_list, "Label", "#color")

# Step 4: Decorate
canvas.title(fig, ax, "Plot Title")
canvas.xlabel(fig, ax, "X Label")
canvas.ylabel(fig, ax, "Y Label")
canvas.grid(fig, ax, SATTVA)

# Step 5: Output
canvas.to_ascii(fig)         # terminal preview
canvas.save(fig, "out.html") # save interactive HTML
canvas.to_json(fig)          # JSON descriptor for browser
canvas.free(fig)             # release memory
```

---

## Color Reference

| Name | Hex | Meaning |
|------|-----|---------|
| Gold | `#c8a84b` | Default TRIKA gold |
| SATTVA green | `#22c55e` | Good / high / dharma |
| RAJAS amber | `#f59e0b` | Neutral / middle |
| TAMAS red | `#ef4444` | Bad / low / adharma |
| Blue | `#3b82f6` | Cool / data |
| Purple | `#a855f7` | Mystery |
| Cyan | `#06b6d4` | Flow |

---

## canvas.figure() — The Canvas

```trika
trika fig = canvas.figure(title, width, height, dpi)
```

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `title` | string | `""` | Figure title |
| `width` | float | `10.0` | Width in inches |
| `height` | float | `6.0` | Height in inches |
| `dpi` | int | `100` | Dots per inch |

**Python equivalent:**
```python
fig = plt.figure(figsize=(10, 6), dpi=100)
fig.suptitle("My Title")
```

---

## canvas.subplot() — The Plot Area

```trika
trika ax = canvas.subplot(fig, rows, cols, index)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `fig` | handle | Figure handle |
| `rows` | int | Grid rows (1 for single) |
| `cols` | int | Grid columns (1 for single) |
| `index` | int | Position (1-based, left→right, top→bottom) |

**Examples:**
```trika
# Single plot
trika ax = canvas.subplot(fig, 1, 1, 1)

# 2×2 grid — top-left
trika ax1 = canvas.subplot(fig, 2, 2, 1)
# 2×2 grid — top-right
trika ax2 = canvas.subplot(fig, 2, 2, 2)
# 2×2 grid — bottom-left
trika ax3 = canvas.subplot(fig, 2, 2, 3)
# 2×2 grid — bottom-right
trika ax4 = canvas.subplot(fig, 2, 2, 4)
```

**Python equivalent:**
```python
ax = fig.add_subplot(1, 1, 1)
# or
fig, axes = plt.subplots(2, 2)
```

---

## Decoration Functions

### canvas.title(fig, ax, text)
```trika
canvas.title(fig, ax, "My Chart Title")
```
```python
ax.set_title("My Chart Title")
```

### canvas.xlabel(fig, ax, text)
```trika
canvas.xlabel(fig, ax, "X Axis Label")
```
```python
ax.set_xlabel("X Axis Label")
```

### canvas.ylabel(fig, ax, text)
```trika
canvas.ylabel(fig, ax, "Y Axis Label")
```
```python
ax.set_ylabel("Y Axis Label")
```

### canvas.grid(fig, ax, on)
```trika
canvas.grid(fig, ax, SATTVA)   # grid on
canvas.grid(fig, ax, TAMAS)    # grid off
```
```python
ax.grid(True)
ax.grid(False)
```

### canvas.xlim(fig, ax, min, max)
```trika
canvas.xlim(fig, ax, 0, 100)
```
```python
ax.set_xlim(0, 100)
```

### canvas.ylim(fig, ax, min, max)
```trika
canvas.ylim(fig, ax, 0, 1000)
```
```python
ax.set_ylim(0, 1000)
```

### canvas.xscale(fig, ax, scale)
```trika
canvas.xscale(fig, ax, "log")     # logarithmic
canvas.xscale(fig, ax, "linear")  # linear (default)
```
```python
ax.set_xscale("log")
```

### canvas.yscale(fig, ax, scale)
```trika
canvas.yscale(fig, ax, "log")
```
```python
ax.set_yscale("log")
```

### canvas.tight_layout(fig)
```trika
canvas.tight_layout(fig)
```
```python
plt.tight_layout()
```

### canvas.theme(fig, name)
```trika
canvas.theme(fig, "dharma")   # gold on black (default)
canvas.theme(fig, "dark")     # dark blue palette
canvas.theme(fig, "light")    # light background
canvas.theme(fig, "sattva")   # green palette
canvas.theme(fig, "classic")  # matplotlib classic
```

### canvas.palette(fig, name)
```trika
canvas.palette(fig, "trika")   # TRIKA gold palette
canvas.palette(fig, "dark")    # dark palette
canvas.palette(fig, "sattva")  # green shades
```

---

# THE 28 CHART TYPES

---

## 1. Line Chart — `canvas.line()`

**When to use:** Time series, trends, continuous data, mathematical functions.

**Equivalent Python libraries:** `matplotlib.pyplot.plot()`, `plotly.express.line()`, `seaborn.lineplot()`

### Data Format
```
x_data : list of numbers (x positions)
y_data : list of numbers (y values, same length as x)
```

### TRIKA Command
```trika
canvas.line(fig, ax, x_data, y_data, label, color)
```

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `fig` | handle | ✓ | Figure handle |
| `ax` | handle | ✓ | Axis handle |
| `x_data` | list | ✓ | X values |
| `y_data` | list | ✓ | Y values |
| `label` | string | optional | Legend label |
| `color` | string | optional | Hex color |

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Fibonacci Growth", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
trika y = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

canvas.line(fig, ax, x, y, "Fibonacci", "#c8a84b")
canvas.title(fig, ax, "Fibonacci Sequence")
canvas.xlabel(fig, ax, "n")
canvas.ylabel(fig, ax, "F(n)")
canvas.grid(fig, ax, SATTVA)
canvas.tight_layout(fig)

trika ascii = canvas.to_ascii(fig)
uvach(ascii)
canvas.save(fig, "fibonacci_line.html")
canvas.free(fig)
```

### Multiple Lines on Same Axis
```trika
canvas.line(fig, ax, x, y1, "Fibonacci", "#c8a84b")
canvas.line(fig, ax, x, y2, "Tribonacci", "#22c55e")
canvas.line(fig, ax, x, y3, "Linear",    "#ef4444")
canvas.legend(fig, ax)
```

### Python Equivalent
```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(10, 6))
ax.plot(x, y, label="Fibonacci", color="#c8a84b")
ax.set_title("Fibonacci Sequence")
ax.set_xlabel("n")
ax.set_ylabel("F(n)")
ax.grid(True)
plt.tight_layout()
plt.savefig("fibonacci_line.html")
```

### ASCII Output
```
  Fibonacci Growth
  |                                          *
  |                                       *
  |                                    *
  |                                *
  |                          *
  |                    *
  |               *
  |          *
  |     * *
  |-------------------------------------------
  n
```

---

## 2. Scatter Plot — `canvas.scatter()`

**When to use:** Relationships between two variables, clusters, outliers, correlation.

**Equivalent:** `matplotlib.pyplot.scatter()`, `plotly.express.scatter()`, `seaborn.scatterplot()`

### Data Format
```
x_data : list of numbers (x positions)
y_data : list of numbers (y positions)
```

### TRIKA Command
```trika
canvas.scatter(fig, ax, x_data, y_data, label, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Warrior Stats", 10, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika strength = [90, 85, 70, 75, 80, 65, 88, 92, 78, 83]
trika speed    = [75, 90, 85, 70, 80, 95, 72, 68, 88, 77]

canvas.scatter(fig, ax, strength, speed, "Warriors", "#22c55e")
canvas.title(fig, ax, "Strength vs Speed")
canvas.xlabel(fig, ax, "Strength")
canvas.ylabel(fig, ax, "Speed")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "scatter.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.scatter(strength, speed, label="Warriors", color="#22c55e", s=60)
```

---

## 3. Bar Chart — `canvas.bar()`

**When to use:** Comparing categories, discrete data, rankings.

**Equivalent:** `matplotlib.pyplot.bar()`, `plotly.express.bar()`, `seaborn.barplot()`

### Data Format
```
labels : list of strings (category names)
values : list of numbers (bar heights)
```

### TRIKA Command
```trika
canvas.bar(fig, ax, labels, values, label, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Guna Distribution", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika labels = ["SATTVA", "RAJAS", "TAMAS"]
trika values = [45, 35, 20]
trika colors = ["#22c55e", "#f59e0b", "#ef4444"]

# Note: for multi-color bars, call bar three times
canvas.bar(fig, ax, ["SATTVA"], [45], "SATTVA", "#22c55e")
canvas.bar(fig, ax, ["RAJAS"],  [35], "RAJAS",  "#f59e0b")
canvas.bar(fig, ax, ["TAMAS"],  [20], "TAMAS",  "#ef4444")

canvas.title(fig, ax, "Guna Distribution in Kurukshetra")
canvas.ylabel(fig, ax, "Count of Warriors")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "bar.html")
canvas.free(fig)
```

### ASCII Output
```
  Guna Distribution
  |    #####
  |    #####  #####
  |    #####  #####  #####
  |---SATTVA--RAJAS--TAMAS-
```

### Python Equivalent
```python
bars = ax.bar(labels, values, color=colors)
ax.set_ylabel("Count of Warriors")
```

---

## 4. Horizontal Bar — `canvas.barh()`

**When to use:** Long category names, rankings, comparisons where horizontal reading is natural.

**Equivalent:** `matplotlib.pyplot.barh()`, `plotly.express.bar(orientation='h')`

### TRIKA Command
```trika
canvas.barh(fig, ax, labels, values, label, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Warrior Rankings", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika warriors = ["Arjuna", "Bhima", "Nakula", "Sahadeva", "Yudhishthira"]
trika scores   = [95, 88, 72, 75, 80]

canvas.barh(fig, ax, warriors, scores, "Score", "#c8a84b")
canvas.title(fig, ax, "Pandava Warrior Scores")
canvas.xlabel(fig, ax, "Dharma Score")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "barh.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.barh(warriors, scores, color="#c8a84b", label="Score")
ax.set_xlabel("Dharma Score")
```

---

## 5. Histogram — `canvas.hist()`

**When to use:** Distribution of a single variable, frequency analysis.

**Equivalent:** `matplotlib.pyplot.hist()`, `plotly.express.histogram()`, `seaborn.histplot()`

### Data Format
```
data : list of numbers (raw values — bins computed automatically)
bins : int (number of bins, default 20)
```

### TRIKA Command
```trika
canvas.hist(fig, ax, data, bins, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Score Distribution", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika scores = [45, 62, 78, 55, 90, 88, 72, 95, 63, 41,
                85, 77, 69, 92, 58, 74, 81, 66, 87, 73,
                52, 96, 71, 84, 60, 79, 68, 91, 57, 76]

canvas.hist(fig, ax, scores, 10, "#3b82f6")
canvas.title(fig, ax, "Score Distribution")
canvas.xlabel(fig, ax, "Score")
canvas.ylabel(fig, ax, "Frequency")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "histogram.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.hist(scores, bins=10, color="#3b82f6", edgecolor='white')
ax.set_xlabel("Score")
ax.set_ylabel("Frequency")
```
```python
# seaborn equivalent
sns.histplot(scores, bins=10, ax=ax, color="#3b82f6")
```

---

## 6. Pie Chart — `canvas.pie()`

**When to use:** Part-to-whole relationships, proportions, percentages.

**Equivalent:** `matplotlib.pyplot.pie()`, `plotly.express.pie()`, `go.Pie()`

### Data Format
```
values : list of numbers (slice sizes — auto-normalized to 100%)
labels : list of strings (slice labels, same length)
```

### TRIKA Command
```trika
canvas.pie(fig, ax, values, labels)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Army Composition", 8, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika values = [40, 35, 25]
trika labels = ["Pandavas", "Kauravas", "Neutral"]

canvas.pie(fig, ax, values, labels)
canvas.title(fig, ax, "Kurukshetra Army Composition")
canvas.save(fig, "pie.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.pie(values, labels=labels, autopct='%1.1f%%',
       colors=["#22c55e", "#ef4444", "#f59e0b"])
ax.set_title("Army Composition")
```

---

## 7. Area Chart — `canvas.area()`

**When to use:** Cumulative totals, filled trends, emphasis on magnitude over time.

**Equivalent:** `matplotlib.pyplot.fill_between()` with line, `plotly.express.area()`

### TRIKA Command
```trika
canvas.area(fig, ax, x_data, y_data, label, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Cumulative Fibonacci", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
trika y = [1, 2, 4, 7, 12, 20, 33, 54, 88, 143]  # cumulative Fibonacci

canvas.area(fig, ax, x, y, "Cumulative", "#c8a84b")
canvas.title(fig, ax, "Cumulative Fibonacci Growth")
canvas.xlabel(fig, ax, "n")
canvas.ylabel(fig, ax, "Cumulative Sum")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "area.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.fill_between(x, y, alpha=0.4, color="#c8a84b", label="Cumulative")
ax.plot(x, y, color="#c8a84b")
```

---

## 8. Step Chart — `canvas.step()`

**When to use:** Discrete state changes, digital signals, step functions, guna transitions.

**Equivalent:** `matplotlib.pyplot.step()`, `plotly.express.line(line_shape='hv')`

### TRIKA Command
```trika
canvas.step(fig, ax, x_data, y_data, label, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Guna State Over Time", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika time  = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
trika state = [1, 1, 0, 0, -1, -1, 0, 1, 1, 0, -1]

canvas.step(fig, ax, time, state, "Guna State", "#f59e0b")
canvas.title(fig, ax, "Guna Transitions Over Time")
canvas.xlabel(fig, ax, "Time")
canvas.ylabel(fig, ax, "State: SATTVA=1 RAJAS=0 TAMAS=-1")
canvas.ylim(fig, ax, -2, 2)
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "step.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.step(time, state, label="Guna State", color="#f59e0b", where='post')
ax.set_ylim(-2, 2)
```

---

## 9. Stem Plot — `canvas.stem()`

**When to use:** Discrete sequences, impulse response, signal processing, standing values.

**Equivalent:** `matplotlib.pyplot.stem()`

### TRIKA Command
```trika
canvas.stem(fig, ax, x_data, y_data, label)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Fibonacci Impulse", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika n    = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
trika fibs = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

canvas.stem(fig, ax, n, fibs, "F(n)")
canvas.title(fig, ax, "Fibonacci — Impulse Response")
canvas.xlabel(fig, ax, "n")
canvas.ylabel(fig, ax, "F(n)")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "stem.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.stem(n, fibs, label="F(n)", linefmt='C0-', markerfmt='C0o')
```

---

## 10. Error Bar — `canvas.errorbar()`

**When to use:** Scientific measurements with uncertainty, confidence intervals, mean ± std.

**Equivalent:** `matplotlib.pyplot.errorbar()`, `plotly.express.scatter(error_y=...)`

### Data Format
```
x_data  : list of numbers (x positions)
y_data  : list of numbers (mean values)
y_errors: list of numbers (error magnitude ± same length)
```

### TRIKA Command
```trika
canvas.errorbar(fig, ax, x_data, y_data, y_errors, label)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Measurement with Uncertainty", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika x    = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
trika y    = [2.1, 3.8, 5.5, 4.2, 6.9, 8.1, 7.3, 9.0, 8.7, 10.2]
trika errs = [0.3, 0.5, 0.4, 0.6, 0.3, 0.5, 0.4, 0.3, 0.5, 0.4]

canvas.errorbar(fig, ax, x, y, errs, "Measurement")
canvas.title(fig, ax, "Sacred Measurements ± Uncertainty")
canvas.xlabel(fig, ax, "Experiment")
canvas.ylabel(fig, ax, "Value")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "errorbar.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.errorbar(x, y, yerr=errs, label="Measurement",
            fmt='o-', capsize=5, color="#c8a84b")
```

---

## 11. Fill Between — `canvas.fill_between()`

**When to use:** Confidence bands, range highlighting, upper/lower bounds, shaded regions.

**Equivalent:** `matplotlib.pyplot.fill_between()`, `plotly.graph_objects.Figure` with traces

### Data Format
```
x_data : list of numbers (x positions)
y1     : list of numbers (upper bound)
y2     : list of numbers (lower bound)
color  : string (fill color)
alpha  : float (transparency 0.0–1.0, default 0.3)
```

### TRIKA Command
```trika
canvas.fill_between(fig, ax, x_data, y1, y2, color, alpha)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Confidence Band", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika x     = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
trika mean  = [5, 6, 5.5, 7, 6.5, 8, 7.5, 9, 8.5, 10]
trika upper = [6, 7, 6.5, 8, 7.5, 9, 8.5, 10, 9.5, 11]
trika lower = [4, 5, 4.5, 6, 5.5, 7, 6.5, 8, 7.5, 9]

canvas.fill_between(fig, ax, x, upper, lower, "#22c55e", 0.3)
canvas.line(fig, ax, x, mean, "Mean", "#c8a84b")
canvas.title(fig, ax, "95% Confidence Band")
canvas.xlabel(fig, ax, "Time")
canvas.ylabel(fig, ax, "Value")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "fill_between.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax.fill_between(x, upper, lower, alpha=0.3, color="#22c55e")
ax.plot(x, mean, label="Mean", color="#c8a84b")
```

---

## 12. Box Plot — `canvas.boxplot()`

**When to use:** Statistical summary (min, Q1, median, Q3, max), outlier detection, group comparison.

**Equivalent:** `matplotlib.pyplot.boxplot()`, `plotly.express.box()`, `seaborn.boxplot()`

### Data Format
```
data   : list of numbers (raw values — quartiles computed automatically)
labels : list of strings (one label per dataset)
```

### TRIKA Command
```trika
canvas.boxplot(fig, ax, data, labels)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Score Box Plot", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika scores = [45, 62, 78, 55, 90, 88, 72, 95, 63, 41,
                85, 77, 69, 92, 58, 74, 81, 66, 87, 73]

canvas.boxplot(fig, ax, scores, ["Warrior Scores"])
canvas.title(fig, ax, "Warrior Score Distribution")
canvas.ylabel(fig, ax, "Score")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "boxplot.html")
canvas.free(fig)
```

### Multiple Groups
```trika
# Pass nested list for multiple boxes
trika pandava_scores = [85, 92, 88, 79, 95]
trika kaurava_scores = [72, 68, 75, 80, 71]
# Each sub-list becomes one box
canvas.boxplot(fig, ax, pandava_scores, ["Pandavas"])
canvas.boxplot(fig, ax, kaurava_scores, ["Kauravas"])
```

### Python Equivalent
```python
ax.boxplot(scores, labels=["Warrior Scores"], patch_artist=True)
# seaborn:
sns.boxplot(data=scores, ax=ax)
```

---

## 13. Violin Plot — `canvas.violin()`

**When to use:** Distribution shape (like boxplot + KDE combined), bimodal distributions.

**Equivalent:** `plotly.express.violin()`, `seaborn.violinplot()`

### TRIKA Command
```trika
canvas.violin(fig, ax, data, labels)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Score Violin", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika scores = [45, 62, 78, 55, 90, 88, 72, 95, 63, 41,
                85, 77, 69, 92, 58, 74, 81, 66, 87, 73]

canvas.violin(fig, ax, scores, ["Warriors"])
canvas.title(fig, ax, "Score Distribution Shape")
canvas.ylabel(fig, ax, "Score")
canvas.save(fig, "violin.html")
canvas.free(fig)
```

### Python Equivalent
```python
# seaborn:
sns.violinplot(data=scores, ax=ax, color="#c8a84b")
# plotly:
fig = px.violin(y=scores, box=True, points="all")
```

---

## 14. KDE Plot — `canvas.kde()`

**When to use:** Smooth probability density, continuous distributions, shape of data.

**Equivalent:** `seaborn.kdeplot()`, `scipy.stats.gaussian_kde` + matplotlib

### Data Format
```
data  : list of numbers (raw values — KDE computed automatically)
label : string (legend label)
color : string (line color)
```

### TRIKA Command
```trika
canvas.kde(fig, ax, data, label, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Score Density", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika scores = [45, 62, 78, 55, 90, 88, 72, 95, 63, 41,
                85, 77, 69, 92, 58, 74, 81, 66, 87, 73]

canvas.kde(fig, ax, scores, "Score KDE", "#c8a84b")
canvas.hist(fig, ax, scores, 10, "#3b82f6")
canvas.title(fig, ax, "Score KDE + Histogram")
canvas.xlabel(fig, ax, "Score")
canvas.ylabel(fig, ax, "Density")
canvas.save(fig, "kde.html")
canvas.free(fig)
```

### Python Equivalent
```python
# seaborn:
sns.kdeplot(scores, ax=ax, color="#c8a84b", label="Score KDE")
# matplotlib + scipy:
from scipy.stats import gaussian_kde
kde = gaussian_kde(scores)
x_range = np.linspace(min(scores), max(scores), 200)
ax.plot(x_range, kde(x_range), color="#c8a84b")
```

---

## 15. Heatmap — `canvas.heatmap()`

**When to use:** Matrix data, correlation matrices, 2D grid intensity, cross-tabulation.

**Equivalent:** `seaborn.heatmap()`, `plotly.express.imshow()`, `matplotlib.pyplot.imshow()`

### Data Format
```
matrix  : list of lists (2D matrix — rows × cols)
xlabels : list of strings (column labels)
ylabels : list of strings (row labels)
cmap    : string (colormap name: "viridis"|"dharma"|"plasma"|"hot")
```

### TRIKA Command
```trika
canvas.heatmap(fig, ax, matrix, xlabels, ylabels, cmap)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Battle Intensity Heatmap", 10, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

# 3×5 matrix — rows=armies, cols=days
trika matrix = [
    [9, 7, 5, 3, 1],
    [2, 4, 6, 8, 10],
    [5, 5, 5, 5, 5]
]
trika days    = ["Day1","Day2","Day3","Day4","Day5"]
trika armies  = ["Pandava","Kaurava","Neutral"]

canvas.heatmap(fig, ax, matrix, days, armies, "viridis")
canvas.title(fig, ax, "Battle Intensity Heatmap")
canvas.xlabel(fig, ax, "Day")
canvas.ylabel(fig, ax, "Army")
canvas.save(fig, "heatmap.html")
canvas.free(fig)
```

### Python Equivalent
```python
import seaborn as sns
sns.heatmap(matrix, xticklabels=days, yticklabels=armies,
            annot=True, fmt='g', cmap='viridis', ax=ax)
```

---

## 16. Contour Plot — `canvas.contour()`

**When to use:** 3D data in 2D, terrain maps, field visualizations, level curves.

**Equivalent:** `matplotlib.pyplot.contour()`, `plotly.graph_objects.Contour`

### Data Format
```
x : list of numbers (x grid values)
y : list of numbers (y grid values)
z : list of lists (2D height matrix, rows=y, cols=x)
```

### TRIKA Command
```trika
canvas.contour(fig, ax, x, y, z)
```

### Full Example
```trika
gyan trika.canvas
gyan trika.math

trika fig = canvas.figure("Dharma Field", 10, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika x = [-2, -1, 0, 1, 2]
trika y = [-2, -1, 0, 1, 2]
# z = x² + y² for each (x,y) combination
trika z = [
    [8, 5, 4, 5, 8],
    [5, 2, 1, 2, 5],
    [4, 1, 0, 1, 4],
    [5, 2, 1, 2, 5],
    [8, 5, 4, 5, 8]
]

canvas.contour(fig, ax, x, y, z)
canvas.title(fig, ax, "Dharma Field — x² + y²")
canvas.xlabel(fig, ax, "X")
canvas.ylabel(fig, ax, "Y")
canvas.save(fig, "contour.html")
canvas.free(fig)
```

### Python Equivalent
```python
import numpy as np
X, Y = np.meshgrid(x, y)
Z = X**2 + Y**2
ax.contour(X, Y, Z, levels=10, cmap='viridis')
ax.contourf(X, Y, Z, levels=10, cmap='viridis', alpha=0.6)
```

---

## 17. Imshow — `canvas.imshow()`

**When to use:** Images, pixel data, raw matrix visualization, confusion matrices.

**Equivalent:** `matplotlib.pyplot.imshow()`, `plotly.express.imshow()`

### Data Format
```
matrix : list of lists (2D data — each inner list = one row of pixels/values)
cmap   : string (colormap: "viridis"|"dharma"|"gray"|"hot"|"plasma")
```

### TRIKA Command
```trika
canvas.imshow(fig, ax, matrix, cmap)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Sacred Matrix", 6, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika matrix = [
    [255, 128, 0,   0],
    [128, 255, 128, 0],
    [0,   128, 255, 128],
    [0,   0,   128, 255]
]

canvas.imshow(fig, ax, matrix, "viridis")
canvas.title(fig, ax, "Sacred Matrix — imshow")
canvas.save(fig, "imshow.html")
canvas.free(fig)
```

### Python Equivalent
```python
im = ax.imshow(matrix, cmap='viridis', aspect='auto')
plt.colorbar(im, ax=ax)
```

---

## 18. Candlestick — `canvas.candlestick()`

**When to use:** OHLC financial data, stock prices, trading charts, market analysis.

**Equivalent:** `plotly.graph_objects.Candlestick`, `mplfinance.plot()`

### Data Format
```
dates  : list of strings (date labels)
opens  : list of numbers (opening prices)
highs  : list of numbers (high prices)
lows   : list of numbers (low prices)
closes : list of numbers (closing prices)
```

### TRIKA Command
```trika
canvas.candlestick(fig, ax, dates, opens, highs, lows, closes)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Dharma Market", 12, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika dates  = ["Day1","Day2","Day3","Day4","Day5","Day6","Day7"]
trika opens  = [100, 105, 103, 108, 106, 112, 110]
trika highs  = [108, 110, 107, 115, 112, 118, 116]
trika lows   = [98,  103, 100, 106, 104, 110, 108]
trika closes = [105, 103, 108, 106, 112, 110, 115]

canvas.candlestick(fig, ax, dates, opens, highs, lows, closes)
canvas.title(fig, ax, "Dharma Market — OHLC Candlestick")
canvas.xlabel(fig, ax, "Date")
canvas.ylabel(fig, ax, "Price")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "candlestick.html")
canvas.free(fig)
```

### Python Equivalent
```python
import plotly.graph_objects as go
fig = go.Figure(data=[go.Candlestick(
    x=dates, open=opens, high=highs,
    low=lows, close=closes
)])
# OR mplfinance:
import mplfinance as mpf
mpf.plot(df, type='candle', style='charles')
```

---

## 19. Waterfall Chart — `canvas.waterfall()`

**When to use:** Cumulative effect of sequential positive/negative values, financial P&L, bridge charts.

**Equivalent:** `plotly.graph_objects.Waterfall`, custom matplotlib

### Data Format
```
labels : list of strings (category names including start and end)
values : list of numbers (positive = gain, negative = loss)
```

### TRIKA Command
```trika
canvas.waterfall(fig, ax, labels, values)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Battle P&L", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika labels = ["Start", "Day1 Win", "Day2 Loss", "Day3 Win",
                "Day4 Loss", "Day5 Win", "Final"]
trika values = [100, 25, -15, 35, -20, 40, 0]

canvas.waterfall(fig, ax, labels, values)
canvas.title(fig, ax, "Battle Gains & Losses — Waterfall")
canvas.ylabel(fig, ax, "Warriors Remaining")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "waterfall.html")
canvas.free(fig)
```

### Python Equivalent
```python
import plotly.graph_objects as go
fig = go.Figure(go.Waterfall(
    name="Battle", orientation="v",
    x=labels, y=values,
    connector={"line": {"color": "rgb(63, 63, 63)"}}
))
```

---

## 20. Gantt Chart — `canvas.gantt()`

**When to use:** Project timelines, task scheduling, battle plans, phase planning.

**Equivalent:** `plotly.express.timeline()`, custom matplotlib bars

### Data Format
```
tasks     : list of strings (task/activity names)
starts    : list of numbers (start time of each task)
durations : list of numbers (duration of each task)
```

### TRIKA Command
```trika
canvas.gantt(fig, ax, tasks, starts, durations)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Kurukshetra Battle Plan", 12, 7)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika tasks     = ["Formation","Advance","First Contact",
                   "Main Battle","Defense","Retreat","Victory Claim"]
trika starts    = [0, 1, 2, 3, 8, 12, 15]
trika durations = [1, 1, 1, 5, 4, 3, 3]

canvas.gantt(fig, ax, tasks, starts, durations)
canvas.title(fig, ax, "Kurukshetra 18-Day Battle Plan")
canvas.xlabel(fig, ax, "Day")
canvas.save(fig, "gantt.html")
canvas.free(fig)
```

### Python Equivalent
```python
import plotly.express as px
import pandas as pd

df = pd.DataFrame({
    "Task": tasks, "Start": starts, "Duration": durations
})
df["Finish"] = df["Start"] + df["Duration"]
fig = px.timeline(df, x_start="Start", x_end="Finish", y="Task")
# OR matplotlib:
ax.barh(tasks, durations, left=starts, color="#c8a84b")
```

---

## 21. Radar Chart — `canvas.radar()`

**When to use:** Multi-dimensional comparison, skill profiles, performance across categories.

**Equivalent:** `plotly.graph_objects.Scatterpolar`, matplotlib polar axes

### Data Format
```
categories : list of strings (axis labels — 3 or more)
values     : list of numbers (one value per category, same length)
label      : string (series name)
color      : string (line color)
```

### TRIKA Command
```trika
canvas.radar(fig, ax, categories, values, label, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Warrior Profile", 8, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika categories = ["Strength","Speed","Wisdom","Dharma","Courage","Skill"]
trika arjuna = [90, 85, 88, 95, 92, 97]
trika karna  = [95, 90, 70, 60, 88, 95]

canvas.radar(fig, ax, categories, arjuna, "Arjuna", "#22c55e")
canvas.radar(fig, ax, categories, karna,  "Karna",  "#ef4444")
canvas.title(fig, ax, "Warrior Profile — Radar")
canvas.save(fig, "radar.html")
canvas.free(fig)
```

### Python Equivalent
```python
import plotly.graph_objects as go
fig = go.Figure()
fig.add_trace(go.Scatterpolar(
    r=arjuna, theta=categories, fill='toself',
    name='Arjuna', line_color='#22c55e'
))
fig.add_trace(go.Scatterpolar(
    r=karna, theta=categories, fill='toself',
    name='Karna', line_color='#ef4444'
))
```

---

## 22. Polar Plot — `canvas.polar()`

**When to use:** Cyclic data, angles and magnitudes, direction + intensity, mandala patterns.

**Equivalent:** matplotlib polar axes, `plotly.graph_objects.Scatterpolar`

### Data Format
```
theta : list of numbers (angles in degrees: 0–360)
r     : list of numbers (radius values)
label : string (legend label)
color : string (line color)
```

### TRIKA Command
```trika
canvas.polar(fig, ax, theta, r, label, color)
```

### Full Example
```trika
gyan trika.canvas
gyan trika.math

trika fig = canvas.figure("Sacred Mandala", 8, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

# 12-point sacred circle
trika theta = [0, 30, 60, 90, 120, 150, 180, 210, 240, 270, 300, 330, 360]
trika r1    = [5, 3, 4, 5, 3, 4, 5, 3, 4, 5, 3, 4, 5]
trika r2    = [3, 5, 3, 4, 5, 3, 4, 5, 3, 4, 5, 3, 3]

canvas.polar(fig, ax, theta, r1, "Outer Ring", "#c8a84b")
canvas.polar(fig, ax, theta, r2, "Inner Ring", "#22c55e")
canvas.title(fig, ax, "Sacred Mandala — Polar")
canvas.save(fig, "polar.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax = fig.add_subplot(111, projection='polar')
theta_rad = [t * np.pi / 180 for t in theta]
ax.plot(theta_rad, r1, label="Outer Ring", color="#c8a84b")
ax.fill(theta_rad, r1, alpha=0.2, color="#c8a84b")
```

---

## 23. Treemap — `canvas.treemap()`

**When to use:** Hierarchical data, proportional area, nested categories, file sizes.

**Equivalent:** `plotly.express.treemap()`, `squarify` library

### Data Format
```
labels  : list of strings (node names — first is root)
values  : list of numbers (node sizes)
parents : list of strings (parent node name for each, root has "" parent)
```

### TRIKA Command
```trika
canvas.treemap(fig, ax, labels, values, parents)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Army Structure", 12, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika labels  = ["Pandava Army","Infantry","Cavalry",
                 "Archers","Elephants","Kaurava Army",
                 "Heavy Infantry","Chariots"]
trika values  = [100, 40, 25, 20, 15, 100, 50, 50]
trika parents = ["", "Pandava Army", "Pandava Army",
                 "Pandava Army", "Pandava Army", "",
                 "Kaurava Army", "Kaurava Army"]

canvas.treemap(fig, ax, labels, values, parents)
canvas.title(fig, ax, "Army Structure — Treemap")
canvas.save(fig, "treemap.html")
canvas.free(fig)
```

### Python Equivalent
```python
import plotly.express as px
fig = px.treemap(names=labels, parents=parents, values=values)
```

---

## 24. Sunburst — `canvas.sunburst()`

**When to use:** Hierarchical data in concentric rings, multi-level proportions, drill-down.

**Equivalent:** `plotly.express.sunburst()`

### Data Format
Same as treemap: `labels`, `values`, `parents`.

### TRIKA Command
```trika
canvas.sunburst(fig, ax, labels, values, parents)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Army Sunburst", 8, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika labels  = ["Total","Pandavas","Kauravas",
                 "Infantry","Cavalry","Heavy Inf","Chariots"]
trika values  = [0, 100, 100, 40, 60, 50, 50]
trika parents = ["","Total","Total",
                 "Pandavas","Pandavas","Kauravas","Kauravas"]

canvas.sunburst(fig, ax, labels, values, parents)
canvas.title(fig, ax, "Army Structure — Sunburst")
canvas.save(fig, "sunburst.html")
canvas.free(fig)
```

### Python Equivalent
```python
import plotly.express as px
fig = px.sunburst(names=labels, parents=parents, values=values)
```

---

## 25. Funnel Chart — `canvas.funnel()`

**When to use:** Sales pipeline, conversion rates, process stages, sequential reduction.

**Equivalent:** `plotly.graph_objects.Funnel`, `plotly.express.funnel()`

### Data Format
```
labels : list of strings (stage names, top to bottom)
values : list of numbers (count at each stage, decreasing)
```

### TRIKA Command
```trika
canvas.funnel(fig, ax, labels, values)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("Path to Liberation", 10, 7)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika stages = ["Awareness of Dharma",
                "Study of Gita",
                "Practice (Sadhana)",
                "Devotion (Bhakti)",
                "Surrender (Prapatti)",
                "Liberation (Moksha)"]
trika counts = [10000, 5000, 2000, 800, 300, 108]

canvas.funnel(fig, ax, stages, counts)
canvas.title(fig, ax, "Path to Liberation — Funnel")
canvas.save(fig, "funnel.html")
canvas.free(fig)
```

### Python Equivalent
```python
import plotly.graph_objects as go
fig = go.Figure(go.Funnel(
    y=stages, x=counts,
    textinfo="value+percent initial",
    marker={"color": ["#22c55e","#3b82f6","#f59e0b",
                      "#c8a84b","#a855f7","#ef4444"]}
))
```

---

## 26. 3D Surface — `canvas.surface3d()`

**When to use:** Mathematical surfaces, terrain, 3D field visualization, z=f(x,y).

**Equivalent:** `matplotlib Axes3D.plot_surface()`, `plotly.graph_objects.Surface`

### Data Format
```
x   : list of numbers (x grid values)
y   : list of numbers (y grid values)
z   : list of lists (2D surface matrix — z[i][j] = height at (x[j], y[i]))
cmap: string (colormap)
```

### TRIKA Command
```trika
canvas.surface3d(fig, ax, x, y, z, cmap)
```

### Full Example
```trika
gyan trika.canvas
gyan trika.math

trika fig = canvas.figure("Sacred Surface", 10, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

# z = sin(x) * cos(y) surface
trika x = [-3, -2, -1, 0, 1, 2, 3]
trika y = [-3, -2, -1, 0, 1, 2, 3]

# Build z matrix manually
trika z = [
    [-0.14, -0.38, -0.45, -0.14, 0.41, 0.91, 0.66],
    [-0.38, -0.93, -0.91, -0.38, 0.72, 0.93, 0.41],
    [-0.45, -0.91, -0.76, -0.45, 0.45, 0.76, 0.14],
    [-0.14, -0.38, -0.45, -0.14, 0.41, 0.91, 0.66],
    [0.41,  0.72,  0.45,  0.41, -0.17, -0.38, 0.14],
    [0.91,  0.93,  0.76,  0.91, -0.38, -0.93,-0.41],
    [0.66,  0.41,  0.14,  0.66, 0.14,  -0.41,-0.14]
]

canvas.surface3d(fig, ax, x, y, z, "viridis")
canvas.title(fig, ax, "Sacred 3D Surface — sin(x)*cos(y)")
canvas.xlabel(fig, ax, "X")
canvas.ylabel(fig, ax, "Y")
canvas.save(fig, "surface3d.html")
canvas.free(fig)
```

### Python Equivalent
```python
from mpl_toolkits.mplot3d import Axes3D
import numpy as np
X, Y = np.meshgrid(x, y)
Z = np.sin(X) * np.cos(Y)
ax = fig.add_subplot(111, projection='3d')
ax.plot_surface(X, Y, Z, cmap='viridis', alpha=0.8)
# plotly:
fig = go.Figure(data=[go.Surface(x=x, y=y, z=Z, colorscale='Viridis')])
```

---

## 27. 3D Scatter — `canvas.scatter3d()`

**When to use:** Three-variable relationships, 3D clustering, spatial data, volumetric data.

**Equivalent:** `matplotlib Axes3D.scatter()`, `plotly.express.scatter_3d()`

### Data Format
```
x      : list of numbers (x positions)
y      : list of numbers (y positions)
z      : list of numbers (z positions)
color  : string (point color)
```

### TRIKA Command
```trika
canvas.scatter3d(fig, ax, x, y, z, color)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("3D Battle Positions", 10, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

# 10 warrior positions in 3D space
trika px = [1, 3, 5, 7, 9, 2, 4, 6, 8, 5]
trika py = [2, 4, 1, 3, 5, 6, 2, 4, 1, 3]
trika pz = [1, 2, 3, 4, 5, 2, 4, 1, 3, 5]

canvas.scatter3d(fig, ax, px, py, pz, "#22c55e")
canvas.title(fig, ax, "Warrior Positions — 3D Space")
canvas.xlabel(fig, ax, "East-West")
canvas.ylabel(fig, ax, "North-South")
canvas.save(fig, "scatter3d.html")
canvas.free(fig)
```

### Python Equivalent
```python
import plotly.express as px
fig = px.scatter_3d(x=px, y=py, z=pz, color_discrete_sequence=["#22c55e"])
# matplotlib:
ax = fig.add_subplot(111, projection='3d')
ax.scatter(px, py, pz, c="#22c55e", s=50)
```

---

## 28. 3D Bar Chart — `canvas.bar3d()`

**When to use:** 3D categorical comparisons, volumetric bar charts, spatial bar plots.

**Equivalent:** `matplotlib Axes3D.bar3d()`, Plotly 3D bars

### Data Format
```
x     : list of numbers (x base positions)
y     : list of numbers (y base positions)
z     : list of numbers (bar heights)
```

### TRIKA Command
```trika
canvas.bar3d(fig, ax, x, y, z)
```

### Full Example
```trika
gyan trika.canvas

trika fig = canvas.figure("3D Battle Scores", 10, 8)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika bx = [1, 2, 3, 4, 5]
trika by = [1, 2, 3, 4, 5]
trika bz = [10, 25, 40, 30, 55]

canvas.bar3d(fig, ax, bx, by, bz)
canvas.title(fig, ax, "Battle Day Scores — 3D")
canvas.xlabel(fig, ax, "X Position")
canvas.ylabel(fig, ax, "Y Position")
canvas.save(fig, "bar3d.html")
canvas.free(fig)
```

### Python Equivalent
```python
ax = fig.add_subplot(111, projection='3d')
ax.bar3d(bx, by, [0]*len(bz), 0.8, 0.8, bz, color="#c8a84b")
```

---

# TRIKA-UNIQUE FEATURES

## canvas.guna_color() — SATTVA/RAJAS/TAMAS Coloring

Color data points automatically based on their value relative to SATTVA and TAMAS thresholds. This is impossible in standard Python libraries without custom code.

```trika
canvas.guna_color(fig, ax, sattva_threshold, tamas_threshold)
```

| Value | Color | Meaning |
|-------|-------|---------|
| >= sattva_threshold | 🟢 `#22c55e` | SATTVA — Good / High |
| <= tamas_threshold | 🔴 `#ef4444` | TAMAS — Bad / Low |
| Between | 🟡 `#f59e0b` | RAJAS — Neutral |

```trika
gyan trika.canvas

trika fig = canvas.figure("Guna-Colored Scores", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika days   = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
trika scores = [30, 45, 85, 65, 10, 92, 55, 78, 25, 95]

canvas.line(fig, ax, days, scores, "Score", "#c8a84b")
canvas.scatter(fig, ax, days, scores, "Points", "#c8a84b")

# Above 70 → SATTVA green
# Below 40 → TAMAS red
# Between  → RAJAS amber
canvas.guna_color(fig, ax, 70, 40)

canvas.title(fig, ax, "Dharma Score — Guna Colored")
canvas.xlabel(fig, ax, "Day")
canvas.ylabel(fig, ax, "Score")
canvas.grid(fig, ax, SATTVA)
canvas.save(fig, "guna_colored.html")
canvas.free(fig)
```

**Python equivalent (custom code required):**
```python
colors = ["#22c55e" if v >= 70 else "#ef4444" if v <= 40
          else "#f59e0b" for v in scores]
ax.scatter(days, scores, c=colors, s=60, zorder=5)
```

---

## canvas.proof() — Position Audit

Every chart in TRIKA carries a mathematical proof of what was drawn and where.

```trika
trika audit = canvas.proof(fig)
uvach(audit)
```

**Output example:**
```
TRIKA Canvas Proof — Figure 1 'My Chart'
  3 axes, 1000x600 pts, theme=dharma
  Axis 1 'Fibonacci Growth': 2 series
    Series 1: type=line  label='Fibonacci'  n=10  color=#c8a84b
    Series 2: type=scatter  label='Points'  n=10  color=#22c55e
  Axis 2 'Scatter': 1 series
    Series 1: type=scatter  label='Warriors'  n=20  color=#22c55e
  Axis 3 'Histogram': 1 series
    Series 1: type=histogram  label=''  n=30  color=#3b82f6
```

---

## canvas.to_ascii() — Terminal Preview

Any chart can be previewed in the terminal without a browser:

```trika
trika preview = canvas.to_ascii(fig)
uvach(preview)
```

**Output (line/bar charts):**
```
  Fibonacci Growth
  |                                          *
  |                                    *
  |                              *
  |                        *
  |                  *
  |            *
  |       *
  |    **
  |-------------------------------------------
  n
```

---

## canvas.save() — Output Formats

```trika
# Interactive HTML (recommended — uses Plotly.js)
canvas.save(fig, "chart.html")

# Raw JSON descriptor
canvas.save(fig, "chart.json")
```

The saved HTML file is completely self-contained — no server needed. Open in any browser.

---

## Multi-Panel Figures — Subplots

```trika
gyan trika.canvas

trika fig = canvas.figure("Dashboard", 14, 10)

# 2×2 grid
trika ax1 = canvas.subplot(fig, 2, 2, 1)   # top-left
trika ax2 = canvas.subplot(fig, 2, 2, 2)   # top-right
trika ax3 = canvas.subplot(fig, 2, 2, 3)   # bottom-left
trika ax4 = canvas.subplot(fig, 2, 2, 4)   # bottom-right

trika x = [1,2,3,4,5,6,7,8,9,10]
trika y = [1,1,2,3,5,8,13,21,34,55]

canvas.line(fig, ax1, x, y, "Fibonacci", "#c8a84b")
canvas.title(fig, ax1, "Line")

canvas.scatter(fig, ax2, x, y, "Points", "#22c55e")
canvas.title(fig, ax2, "Scatter")

canvas.bar(fig, ax3, ["S","R","T"], [45,35,20], "Guna")
canvas.title(fig, ax3, "Bar")

canvas.hist(fig, ax4, y, 5, "#3b82f6")
canvas.title(fig, ax4, "Histogram")

canvas.tight_layout(fig)
canvas.save(fig, "dashboard.html")
canvas.free(fig)
```

---


---

## canvas.save() — All Output Formats

TRIKA canvas supports saving to **6 formats**: HTML, JSON, JPG, JPEG, PNG, GIF.

```trika
# Interactive HTML (recommended — Plotly.js, fully self-contained)
canvas.save(fig, "chart.html")

# Raw JSON descriptor (for custom renderers)
canvas.save(fig, "chart.json")

# PNG — lossless, transparent background, best for reports
canvas.save(fig, "chart.png")

# JPG / JPEG — compressed, small file size, best for web sharing
canvas.save(fig, "chart.jpg")
canvas.save(fig, "chart.jpeg")

# GIF — animated chart, best for presentations and social media
canvas.save(fig, "chart.gif")
```

### Format Comparison

| Format | Extension | Quality | File Size | Transparency | Animated | Best For |
|--------|-----------|---------|-----------|--------------|----------|---------|
| HTML | `.html` | Interactive | Medium | ✓ | ✓ | Browser, sharing |
| JSON | `.json` | Raw data | Small | — | — | Programmatic |
| PNG | `.png` | Lossless | Medium | ✓ | — | Reports, embed |
| JPG | `.jpg` `.jpeg` | Compressed | Small | — | — | Web, photos |
| GIF | `.gif` | 256 colors | Small | ✓ | ✓ | Animation, social |

### Full Save Example — All Formats

```trika
gyan trika.canvas

trika fig = canvas.figure("Sacred Chart", 10, 6)
trika ax  = canvas.subplot(fig, 1, 1, 1)

trika x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
trika y = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

canvas.line(fig, ax, x, y, "Fibonacci", "#c8a84b")
canvas.title(fig, ax, "Fibonacci — All Formats")
canvas.xlabel(fig, ax, "n")
canvas.ylabel(fig, ax, "F(n)")
canvas.grid(fig, ax, SATTVA)

# Save in every format
darshan(canvas.save(fig, "fibonacci.html"))    # interactive
darshan(canvas.save(fig, "fibonacci.json"))    # raw JSON
darshan(canvas.save(fig, "fibonacci.png"))     # lossless PNG
darshan(canvas.save(fig, "fibonacci.jpg"))     # compressed JPG
darshan(canvas.save(fig, "fibonacci.jpeg"))    # same as jpg
darshan(canvas.save(fig, "fibonacci.gif"))     # animated GIF

canvas.free(fig)

uvach("All formats saved!")
```

### Animated GIF — Multi-Frame

For animated GIFs, create multiple figures and save as a sequence:

```trika
gyan trika.canvas

# GIF animation — Fibonacci growing frame by frame
prati i = 1 to 11:
    trika fig = canvas.figure("Fibonacci Growing", 10, 6)
    trika ax  = canvas.subplot(fig, 1, 1, 1)

    trika x_frame = []
    trika y_frame = []
    prati j = 1 to i+1:
        # build up to frame i
    # canvas saves each frame as fibonacci_frame_N.gif
    darshan(canvas.save(fig, "fibonacci_frame_" + str(i) + ".gif"))
    canvas.free(fig)
```

### Python Equivalent

```python
# matplotlib save formats:
plt.savefig("chart.png",  dpi=150, bbox_inches='tight')
plt.savefig("chart.jpg",  dpi=150, bbox_inches='tight', quality=95)
plt.savefig("chart.jpeg", dpi=150, bbox_inches='tight', quality=95)
plt.savefig("chart.gif",  dpi=100)  # requires pillow

# plotly save formats:
fig.write_image("chart.png")    # requires kaleido
fig.write_image("chart.jpg")    # requires kaleido
fig.write_image("chart.gif")    # animated
fig.write_html("chart.html")    # interactive, no dependencies

# seaborn (uses matplotlib backend):
plt.savefig("chart.png", dpi=150, transparent=True)
plt.savefig("chart.jpg", dpi=150, format='jpeg', quality=90)
```

### DPI and Quality Settings

```trika
# Higher DPI = larger file, sharper image
# Default DPI = 100 (set in canvas.figure)
trika fig = canvas.figure("High Res Chart", 10, 6, 300)  # 300 DPI for print
trika fig = canvas.figure("Web Chart",      10, 6, 72)   # 72 DPI for web
trika fig = canvas.figure("Standard Chart", 10, 6, 150)  # 150 DPI balanced
```

---

## Complete Compile Command — Phase 15

```bash
gcc -std=c11 \
    trika_token.c trika_value.c trika_env.c trika_ast.c \
    trika_lexer.c trika_parser.c trika_input.c \
    trika_math.c trika_file.c trika_time.c \
    trika_grid.c trika_visual.c trika_event.c \
    trika_window.c trika_generator.c trika_canvas.c \
    trika_interp.c trika_main.c \
    -o trika -lm
```

---

## Python Library Equivalence Table

| trika.canvas | matplotlib | plotly | seaborn | bokeh |
|-------------|-----------|--------|---------|-------|
| `canvas.line` | `plt.plot` | `px.line` | `sns.lineplot` | `p.line` |
| `canvas.scatter` | `plt.scatter` | `px.scatter` | `sns.scatterplot` | `p.scatter` |
| `canvas.bar` | `plt.bar` | `px.bar` | `sns.barplot` | `p.vbar` |
| `canvas.barh` | `plt.barh` | `px.bar(orientation='h')` | — | `p.hbar` |
| `canvas.hist` | `plt.hist` | `px.histogram` | `sns.histplot` | — |
| `canvas.pie` | `plt.pie` | `px.pie` | — | — |
| `canvas.area` | `fill_between` | `px.area` | — | — |
| `canvas.step` | `plt.step` | `px.line(line_shape='hv')` | — | — |
| `canvas.stem` | `plt.stem` | — | — | — |
| `canvas.errorbar` | `plt.errorbar` | `px.scatter(error_y=...)` | — | — |
| `canvas.fill_between` | `fill_between` | custom | — | — |
| `canvas.boxplot` | `plt.boxplot` | `px.box` | `sns.boxplot` | — |
| `canvas.violin` | — | `px.violin` | `sns.violinplot` | — |
| `canvas.kde` | — | — | `sns.kdeplot` | — |
| `canvas.heatmap` | `plt.imshow` | `px.imshow` | `sns.heatmap` | — |
| `canvas.contour` | `plt.contour` | `go.Contour` | — | — |
| `canvas.imshow` | `plt.imshow` | `px.imshow` | — | — |
| `canvas.candlestick` | mplfinance | `go.Candlestick` | — | — |
| `canvas.waterfall` | custom | `go.Waterfall` | — | — |
| `canvas.gantt` | custom | `px.timeline` | — | — |
| `canvas.radar` | polar axes | `go.Scatterpolar` | — | — |
| `canvas.polar` | polar axes | `go.Scatterpolar` | — | — |
| `canvas.treemap` | squarify | `px.treemap` | — | — |
| `canvas.sunburst` | — | `px.sunburst` | — | — |
| `canvas.funnel` | — | `go.Funnel` | — | — |
| `canvas.surface3d` | `Axes3D.plot_surface` | `go.Surface` | — | — |
| `canvas.scatter3d` | `Axes3D.scatter` | `px.scatter_3d` | — | — |
| `canvas.bar3d` | `Axes3D.bar3d` | — | — | — |
| **`canvas.guna_color`** | **custom code** | **custom code** | **custom code** | **custom code** |
| **`canvas.proof`** | **none** | **none** | **none** | **none** |

---

*TRIKA Canvas Complete Reference — Phase 15*
*Born in Patna, Bihar, India · Built in Pure C · One Man Army*
*🕉️ Hari Om Namah Shivaye*
