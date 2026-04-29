# PyCon US 2026 tutorial: Thinking in Arrays: An Introduction to Array-Oriented Programming

This repository contains everything you need to follow the "[Thinking in Arrays: An Introduction to Array-Oriented Programming](https://us.pycon.org/2026/schedule/presentation/92/)" tutorial, presented at the [PyCon US 2026](https://us.pycon.org/2026/) conference on [Thursday, May 14, 2026 1:30 p.m.–5 p.m.](https://us.pycon.org/2026/schedule/presentation/92/) in Room 101A.

## Internet connectivity

> [!IMPORTANT]
> **Strongly recommended: do a local setup *and* pre-download the Part 4 dataset before the tutorial.** Conference Wi-Fi is unreliable, and this is the only way to guarantee you can follow along regardless of what the network does on the day.

### Recommended path (local + pre-downloaded data)

1. Clone this repository and create the virtual environment using one of the setups below (`pixi`, `uv`, `venv`, `conda`, etc.) — see the sections that follow.
2. Pre-download the 611 MB Chicago taxi Parquet file used in Part 4 and place it at `part-4/chicago-taxi.parquet`.
   with `curl`:
   ```shell
   curl -L -o part-4/chicago-taxi.parquet https://pivarski-princeton.s3.amazonaws.com/chicago-taxi.parquet
   ```
   or with `wget`:
   ```shell
   wget -O part-4/chicago-taxi.parquet https://pivarski-princeton.s3.amazonaws.com/chicago-taxi.parquet
   ```
   Then change the `"https://pivarski-princeton.s3.amazonaws.com/chicago-taxi.parquet"` strings in `part-4/project.ipynb` and `part-4/solutions.ipynb` to `"chicago-taxi.parquet"`.

With those two steps done, you need **no internet at all** during the tutorial.

### Other options (less reliable)

- **Local setup without pre-downloading the Parquet file** — works for Parts 1–3 and 5 offline, but Part 4 will stream the 611 MB file from S3 on the day, which depends on the venue's Wi-Fi.
- **MyBinder** (no local setup) — runs everything in the browser, but needs steady connectivity throughout the tutorial just to keep the session alive.

**If the internet goes out at the venue:** only attendees with a local setup will be able to run the notebooks. The projects are done in groups, so one local setup per group is enough. As a last resort, we'll live-code the solutions together.

## Recommended: run the notebooks on your computer with `pixi`

First, clone this repository.

```shell
git clone https://github.com/ikrommyd/2026-05-14-pyconus2026-tutorial-thinking-in-arrays.git
cd 2026-05-14-pyconus2026-tutorial-thinking-in-arrays
```

Make sure you've [installed pixi](https://pixi.sh/latest/installation/) on your computer.

Then you can install the environment and start a local JupyterLab session with:

```shell
pixi run start
```
## Alternative: run the notebooks on your computer with `uv` or a standard Python `venv`

Make sure you've [installed uv](https://docs.astral.sh/uv/getting-started/installation/) on your computer.

Then you can install the environment and start a local JupyterLab session with uv:

```shell
uv venv --python=3.14
source .venv/bin/activate
uv pip install -r requirements.txt
jupyter lab
```

or with a standard Python `venv`:

```shell
python3.14 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

## Alternative: run the notebooks on your computer with `conda`/`mamba`

Make sure you've [installed Miniforge](https://conda-forge.org/download/) on your computer.

Then you can install the environment and start a local JupyterLab session with:

```shell
conda env create -f environment.yml
conda activate 2026-05-14-pyconus2026-tutorial-thinking-in-arrays
jupyter lab
```

## Alternative: run the notebooks on MyBinder
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/ikrommyd/2026-05-14-pyconus2026-tutorial-thinking-in-arrays/HEAD)

Click on the Binder badge above or go to the url below to launch a JupyterLab session in your browser with the notebooks and all dependencies pre-installed using MyBinder:
```
https://mybinder.org/v2/gh/ikrommyd/2026-05-14-pyconus2026-tutorial-thinking-in-arrays/HEAD
```

## Preliminary outline

* **0:00‒0:15 (15 min)** Lecture 1: Array-oriented programming and its benefits. Simple and complex (3 body problem) examples of imperative, functional, and array-oriented styles. Speed and memory advantages in Python. What the array-oriented paradigm emphasizes/is good for: interactive analyses of distributions. Path length as a worked example.
* **0:15‒0:40 (25 min)** Project 1: Conway’s Game of Life using arrays. Imperative solution is given, as is an initial condition that makes boundary conditions unimportant, simplifying the problem. Students’ array-oriented solutions should be much faster than imperative Python. For extra glory, there’s a slick solution involving convolutions.
* **0:40‒0:50 (10 min)** Break.
* **0:50‒1:05 (15 min)** Solutions to project 1. Show manual solution without boundary conditions first, then boundary conditions, then the slick solution involving convolutions.
* **1:05‒1:25 (20 min)** Lecture 2: Disadvantages of array-oriented programming. (1) The problem of intermediate arrays, shown using the quadratic formula, with timing, compared to pre-compiled C code. (2) The “iterate until converged” problem, shown using a one-dimensional minimizer (Newton’s method) for an array of initial states; talk about epochs in ML.
* **1:25‒1:30 (5 min)** Break.
* **1:30‒1:45 (15 min)** Lecture 3: JIT-compilation with Numba and JAX. Describe JIT-compilation as the solution to the intermediate array problem (1). First Numba then JAX on the quadratic formula. Show that Numba only accelerates if you write imperative code, unlike JAX, and show that JAX can’t follow if-branches or loops of unknown length.
* **1:45‒2:05 (20 min)** Project 3: JIT-compilation of the Mandelbrot set. Given imperative Python and array-oriented NumPy with timings, ask for a faster version using Numba and JAX.
* **2:05‒2:15 (10 min)** Break.
* **2:15‒2:30 (15 min)** Solutions to project 3. Show the full “Mandelbrot on all accelerators” and note that array-oriented programming is advantageous for GPU programming, even beyond Python.
* **2:30‒2:45 (15 min)** Lecture 4: Ragged and deeply nested arrays. Show examples of ragged, nested, missing, and heterogeneous data, and how it can still make sense to treat them as arrays. Conversion to and from “tidy” data (tabular with references) to compare and contrast.
* **2:45‒3:05 (20 min)** Project 4: Exploring data in ragged arrays. Compute path lengths of taxi trips from Parquet files.
* **3:05‒3:15 (10 min)** Break.
* **3:15‒3:30 (15 min)** Solutions to project 4.
