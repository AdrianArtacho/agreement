# Modality Agreement [Explorer](https://adrianartacho.github.io/agreement/)

This repository hosts an **interactive 3D visualization** for exploring *time-varying agreement between multiple modalities* (e.g. audio, motion capture, IMU, etc.).

It is designed as a **second-order analytical tool** within the **SALTA pipeline**, allowing researchers to inspect how agreement relationships between modalities evolve over time — not only as static metrics, but as a dynamic, navigable structure.

---

## What this visualization shows

* Each **node** represents one modality
  (e.g. `audio`, `mpipe`, `imu`, …)
* Each **edge (cylinder)** represents **pairwise agreement** between two modalities
* Edge **thickness + opacity** encode agreement strength
* Edge **color gradient** interpolates between the colors of the connected modalities
* Agreement is **time-dependent** and can be explored via:

  * automatic playback
  * manual scrubbing with a time slider

Conceptually, this shows **how modalities converge and diverge over time**, rather than collapsing agreement into a single global scalar.

---

## Repository structure

```text
.
├── index.html        # Main interactive 3D visualization
├── helper.html       # URL parameter helper (optional but recommended)
├── README.md         # This file
```

---

## `index.html` — the main visualization

### How to open

You can open `index.html` in three ways:

1. **Locally**

   ```bash
   open index.html
   ```

2. **Via GitHub Pages**

   ```url
   https://<username>.github.io/<repo>/
   ```

3. **With URL parameters** (see below)

---

### Navigation & interaction

#### Time navigation

* The **time slider** at the bottom spans the full time range
* Time is displayed in **seconds** (internally stored as tenths of a second)
* Playback advances automatically in real time

#### Rotation

* **Click empty space** → start steady rotation
* Rotation speed depends on distance from screen center
* Rotation continues until interrupted

#### Focus

* **Click a node**:

  * rotation stops
  * the clicked modality moves to the foreground
  * the topology rotates to center that modality
* **Click empty space again**:

  * focus is released
  * topology recenters
  * rotation resumes

This separation supports both **exploratory** and **comparative** modes of analysis.

---

### Node colors (heuristic)

Nodes are intentionally kept close to white, with subtle modality-specific tints:

| Modality keyword | Color hint |
| ---------------- | ---------- |
| `audio`          | Blue-ish   |
| `mpipe`          | Red-ish    |
| `imu`            | Green-ish  |
| other            | White      |

Edges smoothly interpolate between the colors of their connected nodes.

---

## Loading custom data via URL parameters

The visualization supports loading **external CSV files** and optional metadata via URL parameters.

### Supported parameters

| Parameter | Description                                                               |
| --------- | ------------------------------------------------------------------------- |
| `csv`     | URL-encoded link to a CSV file containing time-varying pairwise agreement |
| `title`   | Optional title displayed at the top                                       |
| `link`    | Optional hyperlink attached to the title                                  |

### Example

```url
https://<username>.github.io/<repo>/?csv=https%3A%2F%2Fraw.githubusercontent.com%2F...%2Fmodality_agreement_timeseries.csv&title=Experiment%2017&link=https%3A%2F%2Ftrello.com%2F...
```

If no parameters are provided, the visualization falls back to a default CSV file expected in the repository.

---

## CSV format (expected)

The CSV must follow this structure:

```csv
time,modA__modB,modA__modC,modB__modC,...
0,0.34,0.12,0.56
1,0.36,0.15,0.58
...
```

* `time` is expressed in **tenths of a second**
* Each column encodes agreement between a pair of modalities
* Values are expected in `[0,1]`

---

## [`helper.html`](https://adrianartacho.github.io/agreement/helper.html) — URL builder utility

The [`helper.html`](https://adrianartacho.github.io/agreement/helper.html) file is a **small companion tool** that helps you construct valid URLs without manually encoding parameters.

### What it does

* Takes:

  * a *plain* CSV URL
  * an optional title
  * an optional link
* Automatically **URL-encodes** everything
* Outputs a **ready-to-copy link** that opens the visualization with your data

### How to use

1. Open `helper.html` in your browser
2. Paste:

   * the **raw CSV URL**
   * the title (optional)
   * the link (optional)
3. Copy the generated URL
4. Share or bookmark it

This is especially useful when embedding links in:

* documentation
* Trello / Notion
* emails
* calendars
* Research Catalogue expositions

---

## Conceptual context (SALTA)

This visualization is part of the **SALTA ecosystem** (Segmentation Algorithm for Live Temporal Analysis).

Within SALTA, it operates as a:

* **second-order diagnostic tool**
* complementing scalar confidence metrics
* enabling inspection of *when* and *how* modalities align or diverge

Rather than asking *“How consistent is this dataset overall?”*, it supports questions like:

> *At which moments do audio and motion align strongly?
> When does IMU diverge from the rest?
> Are there transient coordination regimes?*

---

## License / reuse

This repository is intended for:

* research
* teaching
* artistic exploration

Feel free to adapt, fork, or embed it in other SALTA-related projects.
If you reuse it in academic or artistic contexts, attribution is appreciated.
