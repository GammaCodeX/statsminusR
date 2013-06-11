

# Tango with the pandas



### The indev work of a few mad students.


<p>Welcome to the first revision of the statsminusR project, the (hopefully)
first project in a range of notebooks, each with the intention of easying the
transistion to using python for all the math and engineering stuff. We honestly
don't know how far the capabilities of python reach, but the wonderful thing is,
of course, that we DO know they'll reach further every month.</p>

<p><i> A fair warning, we sometimes jut stuff down in danish, as the course
we're taking at the Technical University of Denmark (DTU) is being taught in
just that. We'll get around to translating it as soon as we can.</i></p>

Okay, so let's get down to business. For this all to work, you should have
installed on your system the following:
<ul>
    <li> Python </li>
    <li> IPython </li>
    <li> NumPy </li>
    <li> SciPy </li>
    <li> Matplotlib </li>
    <li> Pandas </li>
</ul>

In[1]:
```
%pylab inline
```

    
    Welcome to pylab, a matplotlib-based Python environment [backend: module://IPython.zmq.pylab.backend_inline].
    For more information, type 'help(pylab)'.


In[2]:
```
import pandas as pd
import numpy as np
import scipy as sp
import scipy.special as spec
import scipy.stats as st
```
Stokastiske variabler:
 * Store bogstaver: X,Y,Z osv
 * Udfald af stokastiske variabler angives ved små: x,y,z osv
 * Vi skelner mellem diskrete og kontinuerte stokastiske variable
   * Diskrete - heltal - ex. antal børn.
   * Kontinuerte - det andet gøgl.


# Diskrete stokastiske Variable:

Hvis der findes n lige sandsynlige udfald, hvorfra et må ske,
og hændelse s betegnes som 'succes' så er sandsynligheden for succes
givet ved: s/n
Tæthedsfunktionen kan skrives som f(x) = P(X = x) 
- sandsynligheden for, at en stokastisk variable har udkastet s.

da skal f(x) > 0 for x in S
f(x) = 0 for x not in S


Fordelingsfunktionen for en stokastisk variabel betegnes F(x).
Fordelingsfunktionen er den kumulerede tæthedsfunktion:
  F(x) = P(X <= x)


# Konkrete Statistiske fordelinger



#### Binomial fordeling


<ul>
    <li>There has to be <i>n</i> independant trials, where <i>n</i> is a
constant integer.</li>
    <li>Each trial can produce either succes or failure</li>
    <li>The probability of succes is <i>p</i>, and the probability of failure
<i>1-p</i>. <i>p</i> is constant for all trials.</li>
</ul>

X:           Amount of succes' in <i>n</i> trials.

binom(n,x):  Ways to chose <i>x</i> from <i>n</i>.

Ex:

We wanna know the probability, that out of 50 people, 4 are colorblind.
The probability of being colorblind is 4%.

X: Amount of colorblind people.

P(X = 4)

In[7]:
```
x = 4 
n = 50
p = .04

spec.binom(n,x)*pow(p,x)*pow((1-p),(n-x)) #The sneaky thing about programming is having both an example, and the actual formula.
```



    0.090159319083132725



So a little over 9% chance. Huh.


#### Den hypergeometriske fordeling

* En population af størrelse N
* Vi tager en stikprøve af størrelse n
* Der er a defekte i populationen
* Der er N - a ikke-defekte i populationen

Den stokastiske variabel, X, er hypergeometrisk fordelt.

Tætheden for den hypergeometriske fordeling:

f(x) = P(X = x) = (binom(a,x)*binom(N-a,n-x))/binom(N,n)

Ved stor population kan man snyde med binomialfordeling.
Eks:

tag 3 hardisks fra 15 med 5 defekte

f(1) = P(X = x)
N = 15
a = 5
n = 3

f(1) = (binom(5,1)*binom(10,2))/binom(15,3)

havde det være 'højest 1' havde man lagt f(0) til.

In[30]:
```
chance = (spec.binom(5,1)*spec.binom(10,2))/spec.binom(15,3)
chance
```



    0.49450549450549453




#### Poisson fordelingen

* Poisson fordelingen anvendes ofte som en fordeling (model) for tælletal, hvor der ikk er nogen naturlig øvre grænse.
* Poisson fordelingen kan ofte karakteriseres som intensitet, dvs på formen antal/enhed
* Parameteren lambda angiver intensiteten i poisson fordelingen

In[ ]:
```

```
