# Operators

Import the `pygenmet` package


```python
from ..tools.tools import chromosome
```


```python
import pandas as pd
import numpy as np
```

(operators:_crossover)=
## Crossover

In Genetic Algorithms the crossover (also called recombination) is a genetic operator used to combine the genetic information of two parents to generate new offspring.

### operators.\_crossover

The `docstring` associated to the `_crossover` function is the following.

```python
?_crossover
```

    Parameters
    ----------
    chromosome_a: Chromosome
    chromosome_b: Chromosome
    k: k-point. If k = 1 the method will be single-point crossover, 
                If k = 2 the method will be two-point crossover. 
                If k = N (with N the length of chromosome) the method will be the uniform crossover. Its value is 1 by default.
    
    Returns
    -------
    Two new chromosomes
    
    Notes
    -----
    [1]
    
    References
    ----------
    [1] https://en.wikipedia.org/wiki/Crossover_(genetic_algorithm)
    
    Examples
    --------
    >>> A = _get_father(nwt = dwt.shape[0], nko = dko.shape[0], 
                        dwt = dwt, dko = dko,
                        geneSet = '01', 
                        get_fitness = _get_fitness, obj = np.array(FC.loc[:, murine_models_in[4]]))

    >>> B = _get_father(nwt = dwt.shape[0], nko = dko.shape[0], 
                        dwt = dwt, dko = dko,
                        geneSet = '01', 
                        get_fitness = _get_fitness, obj = np.array(FC.loc[:, murine_models_in[4]]))

    >>> A.print()
    011000111111010 ... 001000010001110 || 001010011000110 ... 011001001111111 	  43	 336	0.03363686825576087

    >>> B.print()
    100101111101111 ... 010001000100101 || 010101001001010 ... 111010000101010 	  42	 345	0.1410663212679354

    >>> A1, B1 = _crossover(A, B, get_fitness = _get_fitness,  
                        nwt = dwt.shape[0], nko = dko.shape[0], dwt = dwt, dko = dko, 
                        obj = np.array(FC.loc[:, murine_models_in[4]]), k = 1)

    >>> A1.print()
    011000111111010 ... 001000010001110 || 001010011000110 ... 111010000101010 	  43	 327	0.007288743389698732

    >>> B1.print()
    100101111101111 ... 010001000100101 || 010101001001010 ... 011001001111111 	  42	 354	0.15370276754212897

    >>> A1, B1 = _crossover(A, B, get_fitness = _get_fitness,  
                        nwt = dwt.shape[0], nko = dko.shape[0], dwt = dwt, dko = dko, 
                        obj = np.array(FC.loc[:, murine_models_in[4]]), k = 772)

    >>> A1.print()
    110000111101111 ... 000000010001111 || 011111001001110 ... 011000001111111 	  43	 355	0.017131591198246282

    >>> B1.print()
    001101111111010 ... 011001000100100 || 000000011000010 ... 111011000101010 	  42	 326	0.13633106854522628
    
(operators:_arithmetic_crossover)=
### operators.\_arithmetic\_crossover

```python
?_arithmetic_crossover
```

    Notes
    -----
    For this specific genotype (GeneSet = '01') the arithmetic crossover techniques are available.
    These techniques are:
      [1] AND
      [2] OR
      [3] XOR
    Arithmetic crossover - some arithmetic operation is performed to make a new offspring [1]
    
    References
    ----------
    [1] https://www.obitko.com/tutorials/genetic-algorithms/crossover-mutation.php
    

```{table} Truth table for AND, OR and XOR logical operators.
:align: center
:width: 80%
:name: truth_table
| A | B | AND | OR | XOR |
|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 |
```

(operators:_mutation)=
## Mutation

See {ref}`theory:mutation` for the theory and definitions.

### operators.\_mutation

```python
?_mutation
```

    Parameters
    ----------
    father : Genes of the father
    geneSet : Set of genes availables. Usually '0' and '1'
    get_fitness : Function to improve
    nwt : Number of No NAFLD Samples
    nko : Number of NAFLD Samples
    dwt : Data of No NAFLD Samples
    dko : Data of NAFLD Samples
    obj : The fold-changes of murine model to adjust
    type : Type of mutation process, 'bsm' by default. Five types are allowed.
           bf : bitflip
           bsm : bitstringmutation
           sw : swap
           in : inversion
           sc : scramble
    p : Parameter to modify the posibility of change in a genes
    
    Returns
    -------
    A new mutated chromosome by the type of mutation process
    
    Notes
    -----
    The flipbit (fb) mutation is an aggressive mutation because change all genes. 
    If in a specific gen the allelo value is '0' this process will change it to '1'.
    
    fb: '0101010101' -> '1010101010'
    
    The bitstringmutation (bsm) mutation process will change a gen with a 
    probability 'p'. If p = None then p = 1/len(genes) [1].
    
    bsm: '0101010101' -> '0101110101'
    
    References
    ----------
    
    [1] https://en.wikipedia.org/wiki/Mutation_(genetic_algorithm)
    [2] https://www.tutorialspoint.com/genetic_algorithms/genetic_algorithms_mutation.htm
    
    Examples
    --------
    

## Selection

(operators:_replacement)=
### operators.\_replacement

```python
?_replacement
```

    Parameters
    ----------
    type : Type of replacement
           rws : Replace Worst Strategy
           rts : Restricted Tournament Selection
           wams : Worst Among Most Similar Replacement
    
    
    Notes
    -----    
    The _replacement function is ised to change the old generation population with the new generation. 
    Four process have been evaluated [1]:
    
    1) Reemplazar  el  Peor  (Replace  Worst  Strategy,  RW).  Se  reemplaza  el  peor  elemento  de  la  población  si  el  hijo  lo  mejora.  
    Ofrece  alta  presión  selectiva,  incluso cuando sus padres son elegidos aleatoriamente.
    
    2) Selección de Torneo Restringido (Restricted Tournament Selection, RTS) [2].    
    
    3) Reemplazar el Peor Entre Semejantes (Worst Among Most Similar Replacement, WAMS)  [3]. se reemplaza el peor cromosoma del 
    conjunto de los N (N = 3, . . . ) padres mas parecidos al descendiente.
    
    4) Algoritmo de Crowding Determinístico (Deterministic Crowding, DC) [4].  Para facilitar la comparativa  utilizaremos  en  nuestros  experimentos. Una variante del DC en el que para cada cruce se generará un único descendente, que sustituirá al padre más parecido en el caso de que lo mejore. 
    
    References
    ----------
    [1] https://sci2s.ugr.es/keel/pdf/keel/congreso/4-diversidadfinal2_daniel_molina.pdf
    [2] G.   Harik.   Finding   multimodal   solutions   using restricted  tournament  selection. Proc.  6th  Int.  Conf. Genetic Algorithms, páginas 24-31, 1995.
    [3] W. Cedeño and V. Vemuri. Multi-niche crowding in genetic algorithms and its application to the assembly of dna restriction-fragments. Evolutionary Computation, 2(4):321-345, 1995.    
    [4] S.W. Mahfoud. Crowding and preselection revised. Parallel Problem Solving from Nature 2, páginas 27-36, 1992.
    
(operators:_selection)=    
### operators.\_selection

```python
?_selection
```

    HAY DOS TIPOS DE SELECCIÓN. LA QUE SELECCIONA FUTUROS PADRES Y LOS SELECCIONA PADRES PARA CRUZARLOS
    
    Tecnicas de emparejamiento:
    Los padres se pueden seleccionar de forma que se mantenga la diversidad de la poblacion 
    
    1) Prohibicion de cruce basada en ascendencia. Un individuo no puede emparejarse con el mismo, ni con sus padres, ni con sus hijos, ni con sus hermanos
    
    2) Prohibicion de incesto. Dos padres se cruzan si su distancia Hamming esta por encima de cierto umbral
    
    3) Emparejamiento variado. Un individuo se cruza con otro que es bastante diferente. Distancia de Hamming
    
    LA QUE SELECCIONA UNA NUEVA GENERACIÓN
    
    1) Random Selection (RS)
    
    2) Tournament Selection (TS): escoge al individuo de mejor
    fitness de entre N individuos seleccionados aleatoriamente (N = 2, 3, . . . )
    La seleccion por torneo, constituye un procedimiento de seleccion de padres muy extendido y en el cual 
    la idea consiste en escoger al azar un numero de individuos de la poblacion, taman~o del torneo, 
    (con o sin reemplazamiento), seleccionar el mejor individuo de este grupo, y repetir el proceso hasta que 
    el numero de individuos seleccionados coincida con el taman~o de la poblacion. Habitualmente el 
    taman~o del torneo es 2, y en tal caso se ha utilizado una version probabilistica en la cual se permite 
    la seleccion de individuos sin que necesariamente sean los mejores.

    3) Linear Rank Selection (LRS): la poblacion se ordena en funcion de su fitness 
    y se asocia una probabilidad de seleccion a cada individuo que depende de su orden
    
    4) Seleccion por Ruleta (Roulette Selection, RS): asigna una probabilidad de seleccion proporcional al valor del fitness del individuo
    Baker (1987) introduce un metodo denominado muestreo universal estocastico, el cual utiliza un unico giro 
    de la ruleta siendo los sectores circulares proporcionales a la funcion objetivo. Los individuos son 
    seleccionados a partir de marcadores, igualmente espaciados y con comienzo aleatorio. (algoritmos geneticos.pdf)
    
    5) Elitista: En el modelo de seleccion elitista se fuerza a que el mejor individuo de la poblacion 
    en el tiempo t, sea seleccionado como padre.
    
    Parameters
    ----------
    chromosomes : List of chromosomes of the population
    size : Number of individuals to select from the population. This parameter is not considered with method = 'elitist'.
    N : Number of Genes to print (if trace is True)
    trace : Should be the chromosomes and the selection printed on the screen
    method: The method used for selection: ['random', 'tournament', 'linear', 'roulette', 'elitist']
    
    Returns
    -------
    fitness : The fitness of each chromosome (individual)
    psel : Probabilities of selecction of each chromosome. pesl(x) = f(x) / sum(f(y)), for each x in y
    selecction : List of selected chromosomes
    
    Notes
    -----
    The aim of this function is to evaluate the fitness of each population (by the chromosome structure) and 
    to asign a probability to select for a new population (next generation).
    
    Examples
    --------
    >>> A_ = []
    >>> A_.append(chromosome(genes = '01010001010110100100', nwt = 10, nko = 10, fitness = 2.3454))
    >>> A_.append(chromosome(genes = '01011011110110100100', nwt = 10, nko = 10, fitness = 1.4401))
    >>> A_.append(chromosome(genes = '01010001010100000100', nwt = 10, nko = 10, fitness = 0.9254))
    >>> A_.append(chromosome(genes = '01110101010110100100', nwt = 10, nko = 10, fitness = 7.1104))
    >>> A_.append(chromosome(genes = '01010101110111100100', nwt = 10, nko = 10, fitness = 2.1494))
    >>> A_.append(chromosome(genes = '01010001110000100100', nwt = 10, nko = 10, fitness = 1.9954))
    >>> A_.append(chromosome(genes = '00000000010110100100', nwt = 10, nko = 10, fitness = 1.7323))
    >>> A_.append(chromosome(genes = '01010000111110100111', nwt = 10, nko = 10, fitness = 1.5002))
    >>> A_.append(chromosome(genes = '01110011010110100111', nwt = 10, nko = 10, fitness = 2.4119))
    >>> A_.append(chromosome(genes = '01010011011110101100', nwt = 10, nko = 10, fitness = 2.1414))

    >>> selection, fit, ps, sel_mean, sel_maximun = _selection(A_, size = 4, N = 8, trace = True, method = 'roulette')

    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01010001...01000101 || 01101001...10100100         4        4           2.3454       0.09912204
    01011011...01101111 || 01101001...10100100         7        4           1.4401       0.07244166
    01010001...01000101 || 01000001...00000100         4        2           0.9254       0.05727278
    01110101...11010101 || 01101001...10100100         6        4           7.1104       0.23955286
    01010101...01010111 || 01111001...11100100         6        5           2.1494       0.09334567
    01010001...01000111 || 00001001...00100100         5        2           1.9954       0.08880708
    00000000...00000001 || 01101001...10100100         1        4           1.7323       0.08105318
    01010000...01000011 || 11101001...10100111         4        7           1.5002       0.07421289
    01110011...11001101 || 01101001...10100111         6        6           2.4119       0.10108189
    01010011...01001101 || 11101011...10101100         5        6           2.1414       0.09310990
    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01110101...11010101 || 01101001...10100100         6        4           7.1104       0.23955286
    01010001...01000101 || 01101001...10100100         4        4           2.3454       0.09912204
    01010001...01000111 || 00001001...00100100         5        2           1.9954       0.08880708
    01010011...01001101 || 11101011...10101100         5        6           2.1414       0.09310990

    >>> selection, fit, ps, sel_mean, sel_maximun = _selection(A_, size = 4, N = 8, trace = True, method = 'linear')

    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01010001...01000101 || 01101001...10100100         4        4           2.3454       0.15555555
    01011011...01101111 || 01101001...10100100         7        4           1.4401       0.02222222
    01010001...01000101 || 01000001...00000100         4        2           0.9254              0.0
    01110101...11010101 || 01101001...10100100         6        4           7.1104              0.2
    01010101...01010111 || 01111001...11100100         6        5           2.1494       0.13333333
    01010001...01000111 || 00001001...00100100         5        2           1.9954       0.08888888
    00000000...00000001 || 01101001...10100100         1        4           1.7323       0.06666666
    01010000...01000011 || 11101001...10100111         4        7           1.5002       0.04444444
    01110011...11001101 || 01101001...10100111         6        6           2.4119       0.17777777
    01010011...01001101 || 11101011...10101100         5        6           2.1414       0.11111111
    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01011011...01101111 || 01101001...10100100         7        4           1.4401       0.02222222
    01010000...01000011 || 11101001...10100111         4        7           1.5002       0.04444444
    01110101...11010101 || 01101001...10100100         6        4           7.1104              0.2
    01010001...01000101 || 01101001...10100100         4        4           2.3454       0.15555555

    >>> selection, fit, ps, sel_mean, sel_maximun = _selection(A_, size = 4, N = 8, trace = True, method = 'random')

    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01010001...01000101 || 01101001...10100100         4        4           2.3454              0.1
    01011011...01101111 || 01101001...10100100         7        4           1.4401              0.1
    01010001...01000101 || 01000001...00000100         4        2           0.9254              0.1
    01110101...11010101 || 01101001...10100100         6        4           7.1104              0.1
    01010101...01010111 || 01111001...11100100         6        5           2.1494              0.1
    01010001...01000111 || 00001001...00100100         5        2           1.9954              0.1
    00000000...00000001 || 01101001...10100100         1        4           1.7323              0.1
    01010000...01000011 || 11101001...10100111         4        7           1.5002              0.1
    01110011...11001101 || 01101001...10100111         6        6           2.4119              0.1
    01010011...01001101 || 11101011...10101100         5        6           2.1414              0.1
    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01010101...01010111 || 01111001...11100100         6        5           2.1494              0.1
    01010001...01000101 || 01000001...00000100         4        2           0.9254              0.1
    01010011...01001101 || 11101011...10101100         5        6           2.1414              0.1
    01010001...01000101 || 01101001...10100100         4        4           2.3454              0.1
    
    >>> selection, fit, ps, sel_mean, sel_maximun = _selection(A_, size = 4, N = 8, trace = True, method = 'elitist')

    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01010001...01000101 || 01101001...10100100         4        4           2.3454       ----------
    01011011...01101111 || 01101001...10100100         7        4           1.4401       ----------
    01010001...01000101 || 01000001...00000100         4        2           0.9254       ----------
    01110101...11010101 || 01101001...10100100         6        4           7.1104       ----------
    01010101...01010111 || 01111001...11100100         6        5           2.1494       ----------
    01010001...01000111 || 00001001...00100100         5        2           1.9954       ----------
    00000000...00000001 || 01101001...10100100         1        4           1.7323       ----------
    01010000...01000011 || 11101001...10100111         4        7           1.5002       ----------
    01110011...11001101 || 01101001...10100111         6        6           2.4119       ----------
    01010011...01001101 || 11101011...10101100         5        6           2.1414       ----------
    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01010101...01010111 || 01111001...11100100         6        5           2.1494       ----------
    01010001...01000101 || 01101001...10100100         4        4           2.3454       ----------
    01110011...11001101 || 01101001...10100111         6        6           2.4119       ----------
    01110101...11010101 || 01101001...10100100         6        4           7.1104       ----------
    
    >>> selection, fit, ps, sel_mean, sel_maximun = _selection(A_, size = 4, N = 8, trace = True, method = 'tournament')

    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    01010001...01000101 || 01101001...10100100         4        4           2.3454       ----------
    01011011...01101111 || 01101001...10100100         7        4           1.4401       ----------
    01010001...01000101 || 01000001...00000100         4        2           0.9254       ----------
    01110101...11010101 || 01101001...10100100         6        4           7.1104       ----------
    01010101...01010111 || 01111001...11100100         6        5           2.1494       ----------
    01010001...01000111 || 00001001...00100100         5        2           1.9954       ----------
    00000000...00000001 || 01101001...10100100         1        4           1.7323       ----------
    01010000...01000011 || 11101001...10100111         4        7           1.5002       ----------
    01110011...11001101 || 01101001...10100111         6        6           2.4119       ----------
    01010011...01001101 || 11101011...10101100         5        6           2.1414       ----------
    |---------------------------------------------------------------------------------------------|
    |-------------- fenotypes ---------------||--- genotypes ---||--- fitness ---||- Probability -|
    00000000...00000001 || 01101001...10100100         1        4           1.7323       ----------
    01010000...01000011 || 11101001...10100111         4        7           1.5002       ----------
    01110011...11001101 || 01101001...10100111         6        6           2.4119       ----------
    01010101...01010111 || 01111001...11100100         6        5           2.1494       ----------
    01110101...11010101 || 01101001...10100100         6        4           7.1104       ----------


