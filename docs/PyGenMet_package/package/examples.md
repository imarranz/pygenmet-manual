---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: '0.8'
    jupytext_version: 1.4.1+dev
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Examples

Import the `pygenmet` package


```python
from pygenmet import *
```


```python
import pandas as pd
import numpy as np
import random
import datetime
```

We define a new fitness function.

## Definition of a simple fitness function

We define a simple fitness function. This function always returns the 1.0 value.


```python
def my_own_get_fitness(genes, nwt, nko, dwt, dko, obj):

    p = 1.0
   
    return p
```

Now, we generate 10 initial solutions (by `_get_father_`function) and we can see the fitness function for each solution.


```python
nwt = 15
nko = 25
dwt = pd.DataFrame(np.array(random.choices('01', k = nwt * 10)).reshape(nwt, 10))
dko = pd.DataFrame(np.array(random.choices('01', k = nko * 10)).reshape(nko, 10))

for i in np.arange(10):
    A = _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                    geneSet = '01', get_fitness = my_own_get_fitness, 
                    obj = 1)

    A.print()
```

    110011000001000 ... 110011000001000 || 110011001111101 ... 111011110111010 	   5	  17	            1.0
    111110000101011 ... 111110000101011 || 100110000001111 ... 011110100001011 	   9	  11	            1.0
    010001110001001 ... 010001110001001 || 101010000001001 ... 010011011011110 	   6	  12	            1.0
    100110001011100 ... 100110001011100 || 011111100111111 ... 111111101001100 	   7	  17	            1.0
    111101110100010 ... 111101110100010 || 001000001001111 ... 011111011000001 	   9	  10	            1.0
    001110011101011 ... 001110011101011 || 001110001101100 ... 011001000001110 	   9	  11	            1.0
    100110010100001 ... 100110010100001 || 101011001110011 ... 100111110100001 	   6	  14	            1.0
    101000101010110 ... 101000101010110 || 011110001000010 ... 000101001101101 	   7	  12	            1.0
    101101000111111 ... 101101000111111 || 010001011010110 ... 101100011110110 	  10	  13	            1.0
    100010011101000 ... 100010011101000 || 100000001100100 ... 001000101000100 	   6	   7	            1.0
    

## Definition of a little more complex function

In this case, we considerer the following fitness function.


```python
def my_own_get_fitness(genes, nwt, nko, dwt, dko, obj):
    
    N_WT = sum(1 for x in genes[:nwt] if x == '1')
    N_KO = sum(1 for x in genes[nwt:] if x == '1')

    p = N_WT / N_KO
    
    return p
```


```python
nwt = 15
nko = 25
dwt = pd.DataFrame(np.array(random.choices('01', k = nwt * 10)).reshape(nwt, 10))
dko = pd.DataFrame(np.array(random.choices('01', k = nko * 10)).reshape(nko, 10))

for i in np.arange(10):
    A = _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                    geneSet = '01', get_fitness = my_own_get_fitness, 
                    obj = 1)

    A.print()
```

    101101010001100 ... 101101010001100 || 001111100111000 ... 110001000000010 	   7	  10	            0.7
    011111101110001 ... 011111101110001 || 101011110010001 ... 100010110010100 	  10	  12	0.8333333333333334
    100010101100111 ... 100010101100111 || 101011111110000 ... 100000101111010 	   8	  15	0.5333333333333333
    111111010110110 ... 111111010110110 || 100010110011100 ... 111001100100110 	  11	  12	0.9166666666666666
    110001100110000 ... 110001100110000 || 000001010000100 ... 001001111000011 	   6	   9	0.6666666666666666
    000110110000011 ... 000110110000011 || 001111111111110 ... 111100011000111 	   6	  17	0.35294117647058826
    011100100101000 ... 011100100101000 || 001000100101111 ... 011110110100010 	   6	  11	0.5454545454545454
    100111100010001 ... 100111100010001 || 101110000110001 ... 100011110010011 	   7	  13	0.5384615384615384
    101101100110001 ... 101101100110001 || 010100101010101 ... 101010110100011 	   8	  12	0.6666666666666666
    111110010111010 ... 111110010111010 || 100011110101101 ... 011011010000010 	  10	  12	0.8333333333333334
    

It is easy to calculate the fitness function. For example, in the first solution the fitness value is 7/10 = 0.7.

## Using a fitness function with mutation operation to find an optimum


In this example, the optimum will be find when the genes string will be '111111...11111'. In this case, p = 0


```python
def my_own_get_fitness(genes, nwt, nko, dwt, dko, obj):
    
    N_WT = sum(1 for x in genes[:nwt] if x == '1') - nwt
    N_KO = sum(1 for x in genes[nwt:] if x == '1') - nko

    p = N_WT + N_KO
    
    return p
```


```python
nwt = 15
nko = 25
dwt = pd.DataFrame(np.array(random.choices('01', k = nwt * 10)).reshape(nwt, 10))
dko = pd.DataFrame(np.array(random.choices('01', k = nko * 10)).reshape(nko, 10))

for i in np.arange(10):
    A = _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                    geneSet = '01', get_fitness = my_own_get_fitness, 
                    obj = 0)

    A.print()
```

    101000001010000 ... 101000001010000 || 000001010101001 ... 010010010010010 	   4	   8	            -28
    010001000011010 ... 010001000011010 || 111100010001000 ... 010001111001000 	   5	  11	            -24
    110011100110111 ... 110011100110111 || 011111111100110 ... 001100110110011 	  10	  17	            -13
    100111010100011 ... 100111010100011 || 001011100010000 ... 100001011100010 	   8	  10	            -22
    110001110110110 ... 110001110110110 || 110011011101011 ... 010110111100110 	   9	  16	            -15
    111000100101110 ... 111000100101110 || 011101011110100 ... 101001011011001 	   8	  15	            -17
    100010000110110 ... 100010000110110 || 010010011000000 ... 000001011111001 	   6	  11	            -23
    001110011110111 ... 001110011110111 || 100011011100010 ... 000101010110111 	  10	  14	            -16
    101010101010011 ... 101010101010011 || 011110111100010 ... 000101100001100 	   8	  13	            -19
    000001110111111 ... 000001110111111 || 011010000011111 ... 111110000000001 	   9	   9	            -22
    

We initialize the algorithm with a maximum of 1000 generations. When the iterations reached the 1000 iterations, the algorithm stops and returns the optimum reached.

Moreover, in the following example, the `_mutation`function is applied.


```python
generations = 1000
starttime = datetime.datetime.now()

nwt = 25
nko = 50
dwt = pd.DataFrame(np.array(random.choices('01', k = nwt * 20)).reshape(nwt, 20))
dko = pd.DataFrame(np.array(random.choices('01', k = nko * 20)).reshape(nko, 20))

A = _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                geneSet = '01', get_fitness = my_own_get_fitness, 
                obj = 0)

for i in np.arange(generations):
    A_son = _mutation(A.Genes, geneSet = '01', 
                      get_fitness = my_own_get_fitness, 
                      nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                      obj = 0, type = 'bsm', p = None)
    
    if A_son.Fitness > A.Fitness:
        A = A_son
        _show_partial_solution(A, starttime = starttime, N = 4)
    
```

    0101...1111 || 1010...0001 	  14	  22	                  -39	 time:    0.001
    0101...1111 || 1110...0001 	  16	  24	                  -35	 time:    0.002
    0101...1111 || 1110...0001 	  16	  25	                  -34	 time:    0.002
    0101...1111 || 1110...0001 	  16	  26	                  -33	 time:    0.003
    0101...1111 || 1110...0001 	  17	  27	                  -31	 time:    0.003
    0101...1111 || 1110...0001 	  17	  28	                  -30	 time:    0.003
    0101...1111 || 1110...0001 	  17	  29	                  -29	 time:    0.003
    0101...1111 || 1110...0001 	  18	  29	                  -28	 time:    0.003
    0101...1111 || 1110...0001 	  18	  30	                  -27	 time:    0.003
    0101...1111 || 1110...0001 	  18	  31	                  -26	 time:    0.004
    0101...1111 || 1110...0001 	  18	  32	                  -25	 time:    0.004
    0101...1111 || 1110...0001 	  19	  32	                  -24	 time:    0.007
    0101...1111 || 1110...0001 	  19	  33	                  -23	 time:    0.008
    0101...1111 || 1110...0001 	  19	  34	                  -22	 time:    0.008
    1101...1111 || 1110...0001 	  20	  34	                  -21	 time:    0.009
    1101...1111 || 1110...0001 	  20	  35	                  -20	 time:    0.009
    1101...1111 || 1110...0001 	  20	  36	                  -19	 time:    0.010
    1101...1111 || 1110...0001 	  20	  37	                  -18	 time:    0.011
    1101...1111 || 1110...0001 	  20	  38	                  -17	 time:    0.011
    1101...1111 || 1110...0001 	  20	  39	                  -16	 time:    0.011
    1101...1111 || 1110...0001 	  21	  39	                  -15	 time:    0.011
    1101...1111 || 1110...0001 	  22	  39	                  -14	 time:    0.011
    1101...1111 || 1110...0001 	  23	  39	                  -13	 time:    0.012
    1101...1111 || 1110...0001 	  24	  39	                  -12	 time:    0.013
    1101...1111 || 1110...0001 	  24	  40	                  -11	 time:    0.017
    1101...1111 || 1110...0011 	  24	  41	                  -10	 time:    0.018
    1101...1111 || 1111...0011 	  24	  42	                   -9	 time:    0.024
    1111...1111 || 1111...0011 	  25	  42	                   -8	 time:    0.025
    1111...1111 || 1111...0011 	  25	  43	                   -7	 time:    0.026
    1111...1111 || 1111...0011 	  25	  44	                   -6	 time:    0.032
    1111...1111 || 1111...0011 	  25	  45	                   -5	 time:    0.032
    1111...1111 || 1111...1011 	  25	  46	                   -4	 time:    0.036
    1111...1111 || 1111...1111 	  25	  47	                   -3	 time:    0.040
    1111...1111 || 1111...1111 	  25	  48	                   -2	 time:    0.050
    1111...1111 || 1111...1111 	  25	  49	                   -1	 time:    0.056
    1111...1111 || 1111...1111 	  25	  50	                    0	 time:    0.056
    

We can see how the algorithm reaches the optimum at 0.056 seconds.


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```


```python
fig, ax = plt.subplots(nrows = 1, ncols = 1, figsize = (10, 6))

generations = 10000
starttime = datetime.datetime.now()

nwt = 250
nko = 500
dwt = pd.DataFrame(np.array(random.choices('01', k = nwt * 50)).reshape(nwt, 50))
dko = pd.DataFrame(np.array(random.choices('01', k = nko * 50)).reshape(nko, 50))
 
for k in [1,2,3,4,5]:
    
    p = 10**(-k)

    results = []
    
    starttime = datetime.datetime.now()
    
    A = _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                    geneSet = '01', get_fitness = my_own_get_fitness, 
                    obj = 0, random_state = 42)

    for i in np.arange(generations):
        A_son = _mutation(A.Genes, geneSet = '01', 
                          get_fitness = my_own_get_fitness, 
                          nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                          obj = 0, type = 'bsm', p = p)

        if A_son.Fitness > A.Fitness:
            A = A_son
            results.append([p, A.Fitness, (datetime.datetime.now() - starttime).total_seconds()])            
      
    results = pd.DataFrame(results, columns = ['p', 'fitness', 'time'])
    ax.plot(results.time, results.fitness, label = r'p = $10^{-{' + str(k) + '}}$', linewidth = 2)

ax.grid(linestyle = '--', color = 'gray', alpha = 0.5)
ax.set_title(r'Convergence of the genetic algorithm by mutation probability (10000 generations)')
ax.set_ylabel(r'Fitness value')
ax.set_xlabel(r'Time (seconds)')
ax.legend(frameon = False, title = r'Probability', bbox_to_anchor = [1.0, 1.0]);
```


```{figure} example_files/example_20_0.png
---
alt: Example
class: bg-primary
width: 80%
align: center
name: example_time
---
Evolution of fitness value of the genetic algorithms by different probability values of mutation. We can observe that the genetic algorithm with a probability of mutation of $10^{-3}$, reaches the optimum in 2.5 seconds.
```

## Chinese postman problem

The Chinese postman problem, postman tour or route inspection problem is to find a shortest closed path or circuit that visits every edge of a (connected) undirected graph. When the graph has an Eulerian circuit (a closed walk that covers every edge once), that circuit is an optimal solution.[^wiki_chinese_problem]

[^wiki_chinese_problem]: [Chinese Postman Problem](https://en.wikipedia.org/wiki/Route_inspection_problem)

A simple example has been built with only four cities. The problem starts and finishes in the city **A**. In the following matrix the distances between each two cities is shown.

```{math}
---
label: distances_chinese_problem
---
\begin{array}{cc}
 & \begin{array}{cccc} \quad A\quad & B\quad & C\quad & D\quad \end{array} \\
\begin{array}{c} A \\ B \\ C \\ D \end{array} & 
\left| \begin{array}{cccc}
0.00 & 5.00 & 5.09 & 9.21\\
5.00 & 0.00 & 2.23 & 2.42\\
5.09 & 2.23 & 0.00 & 5.38\\
9.21 & 2.42 & 5.38 & 0.00\end{array} \right|
\end{array}
```

With these distances we can calculate the distance of each route. These distances are the fitness value for this genetic algorithm.

```{math}
---
label: fitness_chinese_problem
---
f\left\{ \left[\begin{matrix} ABCDA \\ ABDCA \\ ACBDA \\ ACDBA \\ ADBCA \\ ADCBA \end{matrix} \right] \right\} = \left[ \begin{matrix} 21.82 \\ 19.71 \\ 20.77 \\ 19.71 \\ 20.77 \\ 21.82 \end{matrix} \right] 
```

```{code-cell} ipython3
---
tags: [remove-cell]
---
import pandas as pd
import matplotlib.pyplot as plt
from myst_nb import glue
```

```{code-cell} ipython3
---
tags: [remove-cell]
---

for row_, fv, ruta in zip(range(6), (21.82, 19.71, 20.77, 19.71, 20.77, 21.82), ('ABCDA', 'ABDCA', 'ACBDA', 'ACDBA', 'ADBCA', 'ADCBA')): 

    fig, ax = plt.subplots(nrows = 1, ncols = 1, figsize = (3,2))

    data = pd.DataFrame([[0,0], [3,4], [1,5], [6,7]], columns = list('XY'), index = list('ABCD'))
    data = pd.DataFrame([[0,3,1,6], [0,4,5,7]], columns = list('ABCD'), index = list('XY'))

    data.T.plot(kind = 'scatter', x = 'X', y = 'Y', ax = ax, s = 75)
        
    paso = 0.3
        
    ax.annotate('A', (0, 0 + paso), fontsize = 14)
    ax.annotate('B', (3, 4 + paso), fontsize = 14)
    ax.annotate('C', (1, 5 + paso), fontsize = 14)
    ax.annotate('D', (6, 7 + paso), fontsize = 14)

    data_pt = pd.DataFrame([
        [(0,1),(1,2),(2,3),(3,0)],
        [(0,1),(1,3),(3,2),(2,0)],
        [(0,2),(2,1),(1,3),(3,0)],
        [(0,2),(2,3),(3,1),(1,0)],
        [(0,3),(3,1),(1,2),(2,0)],
        [(0,3),(3,2),(2,1),(1,0)]])

    for column_ in range(4):

        point_x = data.iloc[:, data_pt.iloc[row_][column_][0]].values
        point_y = data.iloc[:, data_pt.iloc[row_][column_][1]].values
            
        ax.annotate("",
            xy = (point_y[0], point_y[1]), xycoords = 'data', 
            xytext = (point_x[0], point_x[1]), 
                    textcoords='data', 
                    arrowprops = dict(arrowstyle = "->", 
                                        shrinkA = 10, 
                                        shrinkB = 10,
                                        connectionstyle = "arc3"))

    ax.set_xlabel('')
    ax.set_ylabel('')
    ax.grid(linestyle = ':', color = 'gray')

    glue(ruta, fig, display = False)

```


The genotype space (see {ref}`genotype_interpretation` for more information) for this problem is composed for only six chromosomes (table {ref}`table_genotype_space`).

```{table} Genotype space and fitness value for each solution. The routes are shown in lexicographic order.
:align: center
:width: 80%
:name: table_genotype_space
| Genotypes | Distance | Route | Fitness |
|:-:|:-:|:-:|:-:|
| ABCDA | 5.00 + 2.23 + 5.38 + 9.21 | {glue:}`ABCDA` | 21.82 |
| ABDCA | 5.00 + 4.24 + 5.38 + 5.09 | {glue:}`ABDCA` | 19.71 |
| ACBDA | 5.09 + 2.23 + 4.24 + 9.21 | {glue:}`ACBDA` | 20.77 |
| ACDBA | 5.09 + 5.38 + 4.24 + 5.00 | {glue:}`ACDBA` | 19.71 |
| ADBCA | 9.21 + 4.24 + 2.23 + 5.09 | {glue:}`ADBCA` | 20.77 |
| ADCBA | 9.21 + 5.38 + 2.23 + 5.00 | {glue:}`ADCBA` | 21.82 | 
```


We can conclude that the optimum solution is ABDCA and ACDBA. In the figure {figure:numref}`figure_routes_chinese_postman` we can see the phenotype space.  

```{code-cell} ipython3
---
tags: [remove-cell]
---
fig, axes = plt.subplots(nrows = 3, ncols = 2, figsize = (14,12))

data = pd.DataFrame([[0,0], [3,4], [1,5], [6,7]], columns = list('XY'), index = list('ABCD'))
data = pd.DataFrame([[0,3,1,6], [0,4,5,7]], columns = list('ABCD'), index = list('XY'))

for ax, row_, fv in zip(axes.flat, range(6), (21.82, 19.71, 20.77, 19.71, 20.77, 21.82)):

    data.T.plot(kind = 'scatter', x = 'X', y = 'Y', ax = ax, s = 75)
    
    paso = 0.3
    
    ax.annotate('A', (0, 0 + paso), fontsize = 14)
    ax.annotate('B', (3, 4 + paso), fontsize = 14)
    ax.annotate('C', (1, 5 + paso), fontsize = 14)
    ax.annotate('D', (6, 7 + paso), fontsize = 14)

    data_pt = pd.DataFrame([
     [(0,1),(1,2),(2,3),(3,0)],
     [(0,1),(1,3),(3,2),(2,0)],
     [(0,2),(2,1),(1,3),(3,0)],
     [(0,2),(2,3),(3,1),(1,0)],
     [(0,3),(3,1),(1,2),(2,0)],
     [(0,3),(3,2),(2,1),(1,0)]])

    for column_ in range(4):

        point_x = data.iloc[:, data_pt.iloc[row_][column_][0]].values
        point_y = data.iloc[:, data_pt.iloc[row_][column_][1]].values
        #ax.plot((point_x[0], point_y[0]), (point_x[1],point_y[1]), color = 'black')
        
        ax.annotate("",
            xy = (point_y[0], point_y[1]), xycoords = 'data', 
            xytext = (point_x[0], point_x[1]), 
                    textcoords='data', 
                    arrowprops = dict(arrowstyle = "->", 
                                      shrinkA = 10, 
                                      shrinkB = 10,
                                      connectionstyle = "arc3"))
        
    #data.T.plot(kind = 'scatter', x = 'X', y = 'Y', ax = ax, s = 100)
    
    titulo = ''
    
    for column_ in range(4):
        titulo = titulo + ' | ' + data.columns[data_pt.iloc[row_][column_][0]] + ' -> ' + data.columns[data_pt.iloc[row_][column_][1]] 
    
    titulo = titulo + ' |\n' + 'fitness: ' + str(fv)
    ax.set_title(titulo)
    ax.set_xlabel('')
    ax.set_ylabel('')
    ax.grid(linestyle = ':', color = 'gray')

fig.subplots_adjust(wspace = 0.10, hspace = 0.35)

glue("glue_routes_chinese_postman_problem", fig, display = False)

```

```{glue:figure} glue_routes_chinese_postman_problem
---
align: center
name: figure_routes_chinese_postman
---
All possibles routes among the four cities with the city **A** as node. These routes are the phenotype space for this problem.
```
