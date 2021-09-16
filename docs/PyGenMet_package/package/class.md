(class:chromosome)=
# CLASS `chromosome`

Import the `pygenmet` package


```python
from pygenmet import *
```

With Pyhton a `class`can be created. A `class` provides a lot of functionalities. We can create a new `class` and then we can create a new type of object in Python. This new `class` allows new instances and these instances can also have `methods`.

The `class chromosome` has been created to optimization the algorithm. The `docstring` associated to the `chromosome` class is the following.

```python
?chromosome
```
  
    The class chromosome has a copy of its genes, its fitness and 
    the number of No NAFLD samples and NAFLD samples for print purposes.
    
    Attributes
    ----------
    
    Methods
    -------
    
    print()  
      Prints the chromosome
    
    to_json()   
        
    Notes
    -----
    The representation of a chromosome is the following way
        
    0110101101 ... 0110101101 || 0110110011 ... 0110110011     6     6           0.8945        
    -------------------------    -------------------------   ----- -----         ------
                A                            B                 C     D              E
                    
    Description of the representation:
      A] Wild Type Genes
      B] Knock-Out Genes
      C] Number of Wild Type cases selected 
      D] Number of Knock-out cases selected
      E] The fitness value. The value of the adaptation for this chromosome
        
    Examples
    --------
    >>> CH = chromosome('01101011010110110011', 0.8945, 10, 10)
    >>> print("Genes: {}".format(CH.Genes))
    Genes: 01101011010110110011        
    >>> print("WT Genes: {}".format(CH.WT_Genes))
    WT Genes: 0110101101        
    >>> print("KO Genes: {}".format(CH.KO_Genes))
    KO Genes: 0110110011        
    >>> print("Fitness: {}".format(CH.Fitness))
    Fitness: 0.8945        
    >>> CH.print() 


```python
CH = chromosome('0110101101011000111101101011010110001111', 0.4125, 10, 30)
```


```python
print("Genes: {}".format(CH.Genes))
```

    Genes: 0110101101011000111101101011010110001111
    


```python
print("WT Genes: {}".format(CH.WT_Genes))
```

    WT Genes: 0110101101
    


```python
print("KO Genes: {}".format(CH.KO_Genes))
```

    KO Genes: 011000111101101011010110001111
    


```python
print("Fitness: {}".format(CH.Fitness))
```

    Fitness: 0.4125

(class:methods)=
## Methods

A Python method is like a Python function, except it is associated with object/classes. Methods in python are very similar to functions except for two major differences:

  * The method is **implicitly** used for an object for which it is called.
  * The method is **accessible** to data that is contained within the class.
  
The _chromosome_ class has currently two methods:

  * print()
  * to\_json()

(method:print)=
### print()    

The *print()* method allows to show the `chromosome` information on the screen or in a file.

The *print()* method has an argument, _N_, and with this argument we can customized the number of alleles to print. This method print first de _Wild Types_ genes and second the _KO_ genes separated by ||. The number of alleles equal to 1 for each gen is also printed. At last, the fitness function value is shown.

```python
CH.print(N = 3) 
```

    011 ... 101 || 011 ... 111 	   6	  18	         0.4125

    
```python
CH.print(N = 5) 
```

    01101 ... 01101 || 01100 ... 01111 	   6	  18	         0.4125    

(method:to_json)=    
### to\_json()

**JavaScript Object Notation**, also known as **JSON**, is an open standard file format, that uses human-readable text to store and transmit data objects consisting of attribute–value pairs and array data types. It is also very easy for computers to parse and generate. The JSON is a very common data format.

```python
CH.to_json(path_or_buf = 'out.json')
```

file `out.json` has the following structure:

```json
{"chromosome": [{"Genes": "0110101101011000111101101011010110001111", 
                 "Fitness": 0.4125, 
                 "WT_Genes": "0110101101", 
                 "KO_Genes": "011000111101101011010110001111"}]}
```


    
