# Tools

Import the `pygenmet` package


```python
from pygenmet import *
```


```python
import pandas as pd
import numpy as np
```
(tools:_get_father)=
## tools.\_get\_father

With the function `\_get\_father()` we can to generate an initial solution. We can to initializate `nwt`, `dwt`, `nko` and `dko`. For replicate purpose, this function has the _random\_state_ argument.

The `docstring` associated to the `_get_father` function is the following.

```python
?_get_father
```

    Parameters
    ----------
    nwt : Number of observations of Wild Type
    nko : Number of observations of Knock-out
    dwt : Data of observations of Wild Type
    dko : Data of observations of Knock-out
    geneSet: Usually a list as '01'
    get_fitness: The fitness function to use
    obj : Array of fold-changes of metabolites in murine model
    random_state: If you don't mention the random_state in the code, then whenever you execute your code a new random value
    
    Returns
    -------
    This function returns a chromosome
    
    Examples
    --------    
    >>> _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, geneSet = '01', get_fitness = _get_fitness, obj = FC.FC).print()
    011101101010000 ... 000000001000001 || 101110011001010 ... 011110110000011    37     261    -0.04568152517704738
    
    >>> _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, geneSet = '01', get_fitness = _get_fitness, obj = FC.FC).print()
    000101011001011 ... 101100010101101 || 010000101000100 ... 110111010001010    46     252    -0.07192848665245967
    
    >>> _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, geneSet = '01', get_fitness = _get_fitness, obj = FC.FC).print()
    110101100111011 ... 000110110110111 || 110010000110100 ... 110010011101011    49     267    -0.11718322152992591


```python
nwt = 15
nko = 25
dwt = pd.DataFrame(np.random.rand(nwt,10))
dko = pd.DataFrame(np.random.rand(nko,10))

for i in np.arange(10):
    A = _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                    geneSet = '01', get_fitness = _get_fitness, 
                    obj = [1,0,1,-1,1,0,0,1,0.5, 0.5])

    A.print()
```

    000100010101011 ... 000100010101011 || 010011110000011 ... 000110111000101 	   6	  12	-0.01750455939922404
    010100000111001 ... 010100000111001 || 000111111010001 ... 100010010110110 	   6	  13	0.01583165234542458
    001010100111101 ... 001010100111101 || 101110011011111 ... 111110100001101 	   8	  15	0.1337101625593648
    011011101001110 ... 011011101001110 || 011111111111101 ... 111010000110111 	   9	  18	0.3326538149497444
    101100111001001 ... 101100111001001 || 010100110110000 ... 100001010110001 	   8	  11	0.09708129202192302
    010001010010001 ... 010001010010001 || 100111000100111 ... 001110100100100 	   5	  11	0.1442876222067664
    000000000011101 ... 000000000011101 || 100100011111100 ... 111000011110101 	   4	  14	0.28826914052937097
    110100111110100 ... 110100111110100 || 111011001010111 ... 101111010101001 	   9	  15	-0.377007167796123
    100111000110010 ... 100111000110010 || 111001110110000 ... 100001101111100 	   7	  15	0.3216335311818925
    000111101101000 ... 000111101101000 || 100010011101100 ... 011001100001110 	   7	  12	-0.09813075927314555
    


```python
for i in np.arange(10):
    A = _get_father(nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                    geneSet = '01', get_fitness = _get_fitness, 
                    obj = [1,0,1,-1,1,0,0,1,0.5, 0.5], 
                    random_state = 42)

    A.print()
```

    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    100011100001001 ... 100011100001001 || 101101100100011 ... 000111111011111 	   6	  17	0.04061614908467767
    
(tools:_get_population)=
## tools.\_get\_population

The `docstring` associated to the `_get_population` function is the following.

```python
?_get_population
```

    Parameters
    ----------
    individuals : Number of individual of first generation or initial population
    nwt : Number of observations of Wild Type
    nko : Number of observations of Knock-out
    dwt : Data of observations of Wild Type
    dko : Data of observations of Knock-out
    geneSet : Usually a list as '01'
    get_fitness : The fitness function to use
    obj : Array of fold-changes of metabolites in murine model
    random_state : If you don't mention the random_state in the code, then whenever you execute your code a new random value
    
    Returns
    -------
    population_ : A list of the initial population (chromosomes) to initialize the algorithm
    
    Notes
    -----
    
    Examples
    --------
    >>> nwt = 15
    >>> nko = 25
    >>> dwt = pd.DataFrame(np.random.rand(nwt,10))
    >>> dko = pd.DataFrame(np.random.rand(nko,10))
    >>> A = _get_population(individuals = 10, 
                            nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                            geneSet = '01', get_fitness = _get_fitness, obj = [1,0,1,-1,1,0,0,1,0.5, 0.5])
    
    >>> [A_.print() for A_ in A];
    110101101011111 ... 110101101011111 || 101110000011110 ... 111101111110101    11      16    0.27010320047631353
    110001101000111 ... 110001101000111 || 111011001000100 ... 001001100010011     8      12    0.4153593539526977
    110110110000111 ... 110110110000111 || 111001000001001 ... 010011110110101     9      13    0.24120026823063395
    001001101100010 ... 001001101100010 || 101000001100111 ... 001110111010010     6      12    0.5976992970173265
    110110101000111 ... 110110101000111 || 100011000000110 ... 001100011111011     9      12    0.4327563879291974
    010110111011011 ... 010110111011011 || 101101110101111 ... 011110010010000    10      13    0.19109063637942147
    011011111001110 ... 011011111001110 || 000001110011000 ... 110001111010111    10      13    0.19291545113399683
    100010011100001 ... 100010011100001 || 011101010010100 ... 101001111100011     6      14    0.3838922708272582
    110001111111010 ... 110001111111010 || 110111010001010 ... 010100000000100    10       9    0.04833875255418793
    001111011101100 ... 001111011101100 || 100011000100101 ... 001010101000110     9      10    0.6180057110908423    


```python
nwt = 15
nko = 25
dwt = pd.DataFrame(np.random.rand(nwt,10))
dko = pd.DataFrame(np.random.rand(nko,10))
A = _get_population(individuals = 10, 
                    nwt = nwt, nko = nko, dwt = dwt, dko = dko, 
                    geneSet = '01', get_fitness = _get_fitness, 
                    obj = [1,0,1,-1,1,0,0,1,0.5, 0.5])

[A_.print() for A_ in A];
```

    001100101100011 ... 001100101100011 || 010111011100111 ... 001111010101001 	   7	  15	0.22717953288324988
    011111001110011 ... 011111001110011 || 110011011010001 ... 100011100110100 	  10	  13	-0.14158703160537597
    000111000110010 ... 000111000110010 || 000111011011101 ... 111010101101111 	   6	  16	-0.14752436179984593
    111110011001001 ... 111110011001001 || 111101011001011 ... 010111111010101 	   9	  17	0.37230832910925965
    111100011100110 ... 111100011100110 || 001000100111010 ... 110100000100011 	   9	   9	0.09942842284405343
    011100001011101 ... 011100001011101 || 001010010010100 ... 101000010010000 	   8	   7	-0.29440398210415947
    111011011011101 ... 111011011011101 || 000101001001101 ... 011011010111110 	  11	  13	0.262667504755609
    000000010010100 ... 000000010010100 || 111110001111110 ... 111101010010111 	   3	  17	-0.3603100204852186
    111110110010001 ... 111110110010001 || 100101000011100 ... 111000110100010 	   9	  10	-0.254079327688995
    001010010000000 ... 001010010000000 || 100111101001111 ... 011111000011110 	   3	  15	0.3651577081778396

(tools:_read_chromosome)=    
## tools.\_read\_chromosome

This function read the chromosome information from a file and it is loaded in memory. The file can be generated by `to_json()` method.

The `docstring` associated to the `_read_chromosome` function is the following.

```python
?_read_chromosome
```

    Parameters
    ----------
    path_or_buf :  string or file handle. File path or object.
    
    Returns
    -------
    This function returns a chromosome
    
    Examples
    --------
    >>> A = chromosome(genes = '00100101001001011000111010110010', nko=16, nwt=16, fitness=0.98)
    >>> A.print(5)
    00100 ... 00101 || 10001 ... 10010     6       8               0.98
    >>> A.to_json('prueba.json')
    >>> B = _read_chromosome('prueba.json')
    >>> B.print(10)
    0010010100 ... 0100100101 || 1000111010 ... 1010110010         6       8               0.98    


```python
new_CH = _read_chromosome(path_or_buf = 'out.json')
new_CH.print()
```

    0110101101 ... 0110101101 || 011000111101101 ... 011010110001111 	   6	  18	         0.4125
