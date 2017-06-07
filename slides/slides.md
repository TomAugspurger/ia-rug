---
title: Python for Data Analysis
author: Tom Augspurger
date: 2017-06-08
---

### Topics

- Jupyter: Cross-language project supporting interactive data science
- Pandas: High-performance data structures for data analysis in Python
- Dask: Flexible parallel computing

<aside class="notes">

This is a note

</aside>

### Goals

- *Not* to teach you Python
- Explore cross-language tools
- Compare and contrast, learn from each other

### A bit of History

- First release in 1991
- Popular as a "glue" language
- Benefiting from the rise of data science

### Trends

<section data-background-color="#fefefe">
  ![](figures/trends.svg)
</section>


### Jupyter

IPython: an interactive python shell
![](figures/ipython-6-screenshot.png)

### Jupyter Notebook

![](figures/jupyter-notebook-default.png)

- A web application
- More importantly, a file format
- Enables things like nbviewer

### nbviewer

<iframe data-src="http://nbviewer.jupyter.org/" width="800" height="800"></iframe>

### Jupyter Messaging Protocol

![](figures/frontend-kernel.png){width=50%}

Kernels for > 50 languages (including R)

### IRKernel

*Demo*

### ![](figures/pandas_logo.png)

- Implements high-performance data structures for tabular data
- Many familiar operations (groupby, join)
- Handles missing data

### Pandas

*Demo*

### Dask

> - Python has a great, diverse ecosystem for scientific computing
> - but it's mostly restricted to a single core

### Collections, DAGs, and schedulers

![](figures/collections-schedulers.png)

- Take a familiar API
- Translate operations to a task graph
- Have smart schedulers execute the tasks

### Dask.array

<img src="figures/dask-array.svg" width="60%">

    # NumPy code
    import numpy as np
    x = np.random.random((1000, 1000))
    u, s, v = np.linalg.svd(x.dot(x.T))
    
    # Dask.array code
    import dask.array as da
    x = da.random.random((100000, 100000), chunks=(1000, 1000))
    u, s, v = da.linalg.svd(x.dot(x.T))

### Dask.DataFrame

<img src="figures/dask-dataframe-inverted.svg" width="30%">

    import pandas as pd
    df = pd.read_csv('myfile.csv', parse_dates=['timestamp'])
    df.groupby(df.timestamp.dt.hour).value.mean()

    import dask.dataframe as dd
    df = dd.read_csv('hdfs://myfiles.*.csv', parse_dates=['timestamp'])
    df.groupby(df.timestamp.dt.hour).value.mean().compute()

### Fine Grained Python Code

    .

<hr>

    results = {}

    for a in A:
        for b in B:
            if a < b:
                results[a, b] = f(a, b)
            else:
                results[a, b] = g(a, b)

    .

### Fine Grained Python Code

    from dask import delayed, compute

<hr>

    results = {}

    for a in A:
        for b in B:
            if a < b:
                results[a, b] = delayed(f)(a, b)  # lazily construct graph
            else:
                results[a, b] = delayed(g)(a, b)  # without structure

    results = compute(results)  # trigger all computation
