# PYGENMET MANUAL

[![Twitter Follow](https://img.shields.io/twitter/follow/imarranz.svg?style=social)](https://twitter.com/imarranz)
![10.5281/zenodo.5233539](https://zenodo.org/badge/DOI/10.5281/zenodo.5233539.svg)

## Introduction

This repository contains the documentation of [pygenmet](https://github.com/imarranz/pygenmet), a genetic algorithms package developed in Python.

This book includes a collection of functions and examples, written in Python, that shows how to use the PyGenMet package.


## Rendering the manual

To compile or generate the documentation with [Jupyter Book](https://jupyterbook.org/) try this from console:

Clone the repository:

```
git clone https://github.com/imarranz/pygenmet-manual.git
```


Render the manual with [JupyterBook](https://github.com/imarranz/pygenmet-manual.git):

```
jupyter-book build pygenmet-manual/
```

## Citation

I publish each release of PyGenMet on Zenodo and here is a list of version:

|Version|Date|DOI|
|-------|----|---|
| [v1.0.0](https://github.com/imarranz/pygenmet/releases/tag/v1.0.0) | August 22, 2021 | ![10.5281/zenodo.5233539](https://zenodo.org/badge/DOI/10.5281/zenodo.5233539.svg) |
 
If you'd like to cite this package, instead of a specific version, use the following DOI: [https://doi.org/10.5281/zenodo.5233539](https://doi.org/10.5281/zenodo.5233539). Here is the bibtex entry for the book:


```
@software{ibon_martinez_arranz_2021_5233539,
  author       = {Ibon Martínez-Arranz},
  title        = {imarranz/pygenmet: v1.0.0},
  month        = aug,
  year         = 2021,
  publisher    = {Zenodo},
  version      = {v1.0.0},
  doi          = {10.5281/zenodo.5233539},
  url          = {https://doi.org/10.5281/zenodo.5233539}
}
```

Last update on the website: [www.imarranz.com/pygenmet-manual/](http://www.imarranz.com/pygenmet-manual/docs/index.html)

```mermaid
flowchart TB
ids((Start)) ==> A[Initial Population]
A[Initial Population] ==Evaluate all<br>chromosomes in the<br>population==> B[Fitness Evaluation]
B[Fitness Evaluation] ==> F{Stopping Criteria}
F{Stopping Criteria} ==NO==> id1[Genetic Operators]
F{Stopping Criteria} ==YES==> G[Best<br>Chromosome<br>Result]
C[Selection] ==> D[Crossover]
D[Crossover] ==> E[Mutation]
subgraph id1[Genetic Operators]
  direction TB
  C[Selection]
  D[Crossover]
  E[Mutation]
end
subgraph id2[Algorithm]
 id1[Genetic Operators]
 B[Fitness Evaluation]
 F{Stopping Criteria}
end
id1[GeneticOperators] ==> B[Fitness Evaluation]
G[Best<br>Chromosome<br>Result] ==> ide((End))
```
