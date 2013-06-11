

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


In[19]:
```
import pandas as pa
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

* Der skal være n uafhængige forsøg (n er et heltal), hvor n er konstant.
* I hvert enkelt forsøg kan udfaldet være success eller fiasko.
* Sansynlighed for succes er p (og er den samme for alle n forsøg) (sandsynligheden for fiasko er 1-p)

X: antal succes blandt n forsøg. (x er stokastisk variable)

(n (over) x) på hvormange måde kan man vælge x ud af n.

Tæthedsfunktion for binomial : hov, sov.
Eksempel:

X: antal farveblinde

P(X=1)
Ud af 3, hvor én er farveblind.


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
