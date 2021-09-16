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
  languaje: python
  name: python3
---

```{raw} html
<script async="async" src="https://hypothes.is/embed.js"></script>
```

(header_target)=
# Genetics Algorithms with Python

![](./figures/cover.png)


**GENETICS ALGORITHMS WITH PYTHON**        
<br>
_Ibon Martínez-Arranz_
2021-09-15

<!--

.. code-block:: python
   :caption: this.py
   :name: this-py
   print('prueba')

prueba

$$
e = mc^2
$$ (eqn:best)

This is the best equation {eq}`eqn:best`.

```{math} 
---
label: euler
---
e^{i\pi} + 1 = 0
```

Euler's identity, equation {math:numref}`euler`, was elected one of the most beautiful mathematical formulas.

```{margin} Anotación
Contenido al margen
```

:::{admonition,warning} This *is* also **Markdown**
This text is **standard** _Markdown_
:::

```{admonition} My Markdown list
Here is [Markdown link syntax](https://jupyter.org)
```

```python
---
lineno-start: 1
emphasize-lines: 1, 3
caption: |
    This is my
    multi-line caption. It is *pretty ninfty*.
---
a = 1
print('my 1st line')
print(f'my {a}nd line'}
```



```{code-block} python
---
lineno-start: 1
emphasize-lines: 1, 28, 29, 31
caption: |
    This is my
    multi-line caption. It is *pretty ninfty*.
---
def _get_multifitness(genes, nwt, nko, dwt, dko, obj):
    
    """\
    Parameters
    ----------
    genes : Genes of a chromosome
    nwt : Number of observations of Wild Type
    nko : Number of observations of Knock-out
    dwt : Data of observations of Wild Type
    dko : Data of observations of Knock-out
    obj : Array of arrays of fold-changes of the metabolites in all murine models

    Notes
    -----
    
    El geneSet será ahora de 13 caracteres (los mismos que modelos de ratón) más
    el 0. Cada caracter representa un modelo de ratón y cogerenmos los casos en el 
    dataset de los Knock-Out. Ahora bien, para los genes de los wild type, voy a 
    considerar a todos los que no sean '0'. En el caso de los Knock-Out, el '0' 
    indica que es una muestra que no se clasifica 8no optimiza) ningún otro grupo. 
    Podría ser outliers o simplemente no ser de los grupos considerados.
    
    Me falta ordenar que ocurre si en alguna solución no están representados
    todos los modelos ¿qué valores devuelve? ¿cómo operar con ellos?

    """

    den = dwt.loc[[True if x != '0' else False for x in genes[:nwt]], :].mean()
    list_of_correlations = []
    
    for i, j in zip(list('ABCDEFGHIJKLM'), np.arange(13)):
        num = dko.loc[[True if x == i else False for x in genes[nwt:]], :].mean()
        myfc = np.log2(num / den)
        p, _ = pearsonr(myfc, obj[j])
        list_of_correlations.append(p)
        
    """\
    La función devuelve un único valor que tiene que ser un resumen del 
    comportamiento de todas las muestras.
    
    La salida más directa sería la correlación promedio, esperando en alcanzar un 
    máximo que a su vez maximizaría todas los submodelos.
    
    Otra opción es devolver el mínimo de todas las correlaciones, pero esta
    opción puede obligar al algoritmo a buscar como sólución un único modelo
    y el resto clasificarlo como '0'.
    
    Podríamos pensar también en algún tipo de penalización
    """
    
    
    return None
```

```{code-block} python
:lineno-start: 10
:emphasize-lines: 1, 3
:caption: This is my multi-line caption. It is *pretty ninfty*.

a = 3
print('my 1st line')
print(f'my {a}nd line'}
```

```{image} figures/cover.png
:alt: cover
:class: bg-primary
:width: 200px
:align: center
```

prueba

```{figure} figures/cover.png
---
alt: cover
class: bg-primary
width: 500px
align: center
name: fig_pez
---
Mi titulo de figura.
```

prueba

Mi figura {ref}`fig_pez`. {figure:numref}`fig_pez`.

{numref}`{number} <fig_pez>`.



Ejemplo: {ref}`header_target`. 

Ejemplo: {ref}`mi texto <header_target>`

[mi texto](header_target)

`````{tabs}
````{tab} Figura

```{figure} figures/cover.png
---
alt: cover
class: bg-primary
width: 250px
align: center
name: fig_pez_2
---
Mi titulo de figura.
```
````

````{tab} Tabla

| hola | Adios |
|:-:|-:|
| 2.34 | 1.54 |

````


`````

```{code-cell} ipython3
:tags: ['remove-output']
print('This is a test.')
```

```{code-cell} ipython3
note = 'python'
print(note)
```

```{code-cell} ipython3
:tags: ['remove-input']
note = 'python & pyhton'
print(note)
```

```{code-cell} ipython3
from myst_nb import glue
mi_texto = 'Esto es una prueba'
glue('glue_sample', mi_texto, display = False)
```

Aquí hay un ejemplo: {glue:}`glue_sample`.



```{note}
:class: dropdown
Una prueba de contenido.
```

%Aquí citamos {cite}`Armitage2014` y {cite}`Baker2011`


<b>Begin</b><div style="margin-left:20px;width:600px;">
<b>Create Initial Population</b> - Each individual solution is made up of two fixed length strings, with each bit set to 1 with probability <i>P</i><sub>i</sub>. <br>
<b>Repeat</b>
</div>  
<div style="margin-left:40px;width:580px;">
<b>Test all solutions</b> - Assess the predictive accuracy of the nearest neighbour classifier, using only those samples and variables selected by the solution (corresponding to 1 in each string) using study-wise leave-one-out cross validation. This is their <i>fitness</i>. <br>
<b>Repeat</b>
</div>
<div style="margin-left:60px;width:560px;">
<b>Tournament Solutions</b> - Pick four solutions from the population at random, compare their <i>fitness</i>, save the winning solution and repeat to select a second <i>parent</i>.<br>
<b>Crossover</b> - Taking the two winning solutions, pick at random a crossover point inside them. <br>
<b>Create a <i>Child</i> solution</b> - From these two parents by taking the <i>chromosome</i> from one parent up until the crossover point, and from the second parent after the crossover point until the end of the <i>chromosomes</i>. <br>
<b>Mutation</b> - For each point in the <i>chromosome</i> with probability <i>P</i><sub>m</sub>, pick that point to mutate.
</div>
<div style="margin-left:40px; width:580px;">
<b>Until</b> - The new population is full. 
</div>
<div style="margin-left:20px; width:600px;">
<b>Until</b> - K generation habe been simulated.<br>
</div>
<b>End</b>


{fa}`check,text-success mr-1`   

{fa}`terminal mr+1`  

{fa}`book`  

{fa}`arrow-alt-circle-up`

{term}`AA <AA>` y {term}`ChoE <ChoE>`.

```{admonition}
:class: dropdwon, tip
[Mouse Models of Human Cancer Database (MMHCdb)](http://tumor.informatics.jax.org/mtbwi/index.do)
```

% how to combine bold and code sample in markdown

` `**`INPUT:`**`input`   
` `**`OUTPUT:`**`results;`  
` `**`IF`**` this_is_true`  
`    do this;`  
` `**`ELSE`**` `    
`    select B from input;`   
`    `**`FOR EACH`**` `$a_i$` `**`in`**` B`   
`      do something with ` $a_i$` `    
`      do something with a<sub>i</sub>`  
`      do something with ` a<sub>i</sub>` `


```{code}
 **INPUT:** input  
 **OUTPUT:** results;  
 **IF** this_is_true  
   do_this;  
 **ELSE**  
   select B from input;  
   do something with input;  
   **FOR EACH** $a_i$ **in** B  
     do something with $a_i$  
```


<div class="row">
  <div class="column" style="background-color:#aaa;">
    <h2>Column 1</h2>
    <p>Some text..</p>
  </div>
  <div class="column" style="background-color:#bbb;">
    <h2>Column 2</h2>
    <p>Some text..</p>
  </div>
  <div class="column" style="background-color:#ccc;">
    <h2>Column 3</h2>
    <p>Some text..</p>
  </div>
</div>



<div class="card-deck">
  <div class="card">
    <img src="01_Introduction/figures/favicon.png" class="card-img-top" alt="...">
    <div class="card-body">
      <h5 class="card-title">Card title</h5>
      <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
      <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
    </div>
  </div>
  <div class="card">
    <img src="..." class="card-img-top" alt="...">
    <div class="card-body">
      <h5 class="card-title">Card title</h5>
      <p class="card-text">This card has supporting text below as a natural lead-in to additional content.</p>
      <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
    </div>
  </div>
  <div class="card">
    <img src="..." class="card-img-top" alt="...">
    <div class="card-body">
      <h5 class="card-title">Card title</h5>
      <p class="card-text">This is a wider card with supporting text below as a natural lead-in to additional content. This card has even longer content than the first to show that equal height action.</p>
      <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
    </div>
  </div>
</div>


````{admonition} BIBLIOGRAPHY
:class: dropdown, note  
```


```{bibliography} bibliography/bibliography.bib
:notcited:
:style: alpha # plain, unsrt, unsrtalpha
```    
````

-->
