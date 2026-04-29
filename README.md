# PyCon US 2026 tutorial: Thinking in Arrays: An Introduction to Array-Oriented Programming

This repository contains everything you need to follow the "[Thinking in Arrays: An Introduction to Array-Oriented Programming](https://us.pycon.org/2026/schedule/presentation/92/)" tutorial, presented at the [PyCon US 2026](https://us.pycon.org/2026/) conference on [Thursday, May 14, 2026 1:30 p.m.–5 p.m.](https://us.pycon.org/2026/schedule/presentation/92/) in Room 101A.

## Internet connectivity

The tutorial can be run either locally or on MyBinder (a free Jupyter cloud platform).

**Before the tutorial:**
- If you plan to run it locally, create the virtual environment beforehand using one of the setups below (`pixi`, `uv`, `venv`, `conda`, etc.). You can also do it during the tutorial if the venue's internet is good enough.
- If you plan to use MyBinder, no prep is needed — you just need to be able to reach the MyBinder site.

**During the tutorial:**
- A local setup that was prepared beforehand needs no internet at all, *except* for Part 4, which streams a 611 MB Chicago taxi Parquet file from S3. To run Part 4 fully offline, download it once beforehand and place it at `part-4/chicago-taxi.parquet`:
  ```shell
  curl -L -o part-4/chicago-taxi.parquet https://pivarski-princeton.s3.amazonaws.com/chicago-taxi.parquet
  ```
  or with `wget`:
  ```shell
  wget -O part-4/chicago-taxi.parquet https://pivarski-princeton.s3.amazonaws.com/chicago-taxi.parquet
  ```
  then change the `"https://pivarski-princeton.s3.amazonaws.com/chicago-taxi.parquet"` strings in `part-4/project.ipynb` and `part-4/solutions.ipynb` to `"chicago-taxi.parquet"`.
- The MyBinder approach only needs enough connectivity to keep the page loaded.

**If the internet goes out at the venue:** the tutorial can only be completed by attendees with a working local setup. Projects are done in groups, so one local setup per group is enough. As a last resort, we'll live-code the solutions together.

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
