(fitness)=
# Fitness

Import the `pygenmet` package


```python
from pygenmet import *
```

Currently, three fully customizable fitness functions are developed in `pygenmet` package:

  * \_get\_fitness
  * \_get\_fitness\_robust
  * \_get\_fitness\_l
  

(fitness:_get_fitness)=
## fitness.\_get_fitness

The `docstring` associated to the `_get_fitness` function is the following.

```python
?_get_fitness
```

    Parameters
    ----------
    genes : Genes of a chromosome
    nwt : Number of observations of Wild Type
    nko : Number of observations of Knock-out
    dwt : Data of observations of Wild Type
    dko : Data of observations of Knock-out
    obj : Array of fold-changes of metabolites in murine model
    l : float Usually 0.5 / length(fc1). If length(fc1) = 50 then l = 0.01
    
    Returns
    -------
    p : float
        The aptitude of a genes of a chromosome (solution) is the correlation between fc1 and fc2. 
        Initially the aptitude (fitness) of a chromosome is the Pearson Correlation between the 
        fold-change of Knock-out select samples and Wild Type selected samples with the fold-change
        of the murine model analyzed (a vector of ¿50? fold-changes).
    
    Notes
    -----
    This function evaluates the Pearson Correlation 
    between fc1 and fc2 with a penalty for different sign 
    in the values. This function uses pearsonr from scipy and
    sign from numpy to evaluate the aptitude.
    
    The penalty has been named l.
    
    Examples
    --------

(fitness:_get_fitness_robust)=
## fitness.\_get\_fitness\_robust

The `docstring` associated to the `_get_fitness_robust` function is the following.

```python
?_get_fitness_robust
```

    Parameters
    ----------
    genes : Genes of a chromosome
    nwt : Number of observations of Wild Type
    nko : Number of observations of Knock-out
    dwt : Data of observations of Wild Type
    dko : Data of observations of Knock-out
    obj : Array of fold-changes of metabolites in murine model
    l : float Usually 0.5 / length(fc1). If length(fc1) = 50 then l = 0.01
    
    Returns
    -------
    p : float
        The aptitude of a genes of a chromosome (solution) is the correlation between fc1 and fc2. 
        Initially the aptitude (fitness) of a chromosome is the Pearson Correlation between the 
        fold-change of Knock-out select samples and Wild Type selected samples with the fold-change
        of the murine model analyzed (a vector of ¿50? fold-changes).
    
    Notes
    -----
    This function evaluates the Pearson Correlation 
    between fc1 and fc2 with a penalty for different sign 
    in the values. This function uses pearsonr from scipy and
    sign from numpy to evaluate the aptitude.
    
    The penalty has been named l.
    
    Examples
    --------


(fitness:_get_fitness_l)=
##  fitness.\_get\_fitness\_l

The `docstring` associated to the `_get_fitness_l` function is the following.

```python
?_get_fitness_l
```
    Parameters
    ----------
    genes : Genes of a chromosome
    nwt : Number of observations of Wild Type
    nko : Number of observations of Knock-out
    dwt : Data of observations of Wild Type
    dko : Data of observations of Knock-out
    obj : Array of fold-changes of metabolites in murine model
    
    Returns
    -------
    p : float
        The aptitude of a genes of a chromosome (solution) is the correlation between fc1 and fc2. 
        Initially the aptitude (fitness) of a chromosome is the Pearson Correlation between the 
        fold-change of Knock-out select samples and Wild Type selected samples with the fold-change
        of the murine model analyzed (a vector of ¿50? fold-changes).
    
    Notes
    -----
    This function evaluates the Pearson Correlation 
    between fc1 and fc2 with a penalty for different sign 
    in the values. This function uses pearsonr from scipy and
    sign from numpy to evaluate the aptitude.
    
    The penalty has been named l.
    
    Examples
    --------

    

