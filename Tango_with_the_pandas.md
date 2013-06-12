

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


In[6]:
```
import pandas as pd
import numpy as np
import scipy as sp
import scipy.special as spec
import scipy.stats as st
import matplotlib.pyplot as plt
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

In[3]:
```
x = 4 
n = 50
p = .04

print spec.binom(n,x)*pow(p,x)*pow((1-p),(n-x)) #The sneaky thing about programming is having both an example, and the actual formula.

print st.binom.pmf(x,n,p) #do it the easy way 

print st.binom.cdf(x,n,p) #this is, unlike before where we looked for EXACTLY four, UP TO four.

print st.binom.cdf(n-x,n,1-p) # and here we flip it, to represent the chance of 4 or more people being colorblind.
```

    0.0901593190831
    0.0901593190831
    0.951028528115
    0.139130790968


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

In[4]:
```
chance = (spec.binom(5,1)*spec.binom(10,2))/spec.binom(15,3)
chance
```



    0.49450549450549453




#### Poisson fordelingen

* Poisson fordelingen anvendes ofte som en fordeling (model) for tælletal, hvor der ikk er nogen naturlig øvre grænse.
* Poisson fordelingen kan ofte karakteriseres som intensitet, dvs på formen antal/enhed
* Parameteren lambda angiver intensiteten i poisson fordelingen


## Kontinuerte fordelinger



#### Normalfordeling




In[43]:
```
range1 = np.linspace(-13,17,100)
plt.plot(range1, st.norm.pdf(range1,0,3)) #Just a sample plot, data just... picked.
```



    [<matplotlib.lines.Line2D at 0xb4ce28c>]



[!image]()

<b>Ex:</b>

In[42]:
```
st.norm.pdf(300,290,10)
#This is the chance of being paid over 300 bucks if the middle is 290, and the variance 10.
```



    0.024197072451914336



In[36]:
```
1-st.norm.cdf(39,34.5,2.07) #Chance of being late
# Here, it is estimated that a dude has a middle of 34.5 minutes to work, spread 2.07, and is late at 39min+
# We use cdf because we want not ONLY 39, but everything over 39. So we calculate everything under, and substract
# it from 1.
```



    0.014855833143976649




#### Log-Normal distribution


X ~ LN(alpha,beta), beta > 0

Typicallly skews to the right.

In[48]:
```
herp = st.lognorm(1) #This is simply a different example of using the stats distributions. Works on the others aswell.
herp.pdf(1)
```



    0.3989422804014327



In[56]:
```
herp = st.lognorm(0.733,0.44) # Here, we want to find an interval of particles. We have alpha and beta,
herp.cdf(3)-herp.cdf(2)       # and want to figure the particles in the interval [2;3]
```



    0.17218720184665137




#### Uniform distribution


Equal chance of everything. So, if employees get in between 8:00 and 8:30, they
have 0% prob of being outside that interval,
and 1/3 prob of hitting between 8:20 and 8:30, and so on.

In[ ]:
```

```
