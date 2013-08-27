#Introduction

**PyS<sup>3</sup>DE** is a solver of stochastic differential equations (SDE) implemented by Python, which both symbolic and numeric schemems are supported.
Numerical solvers include schemes for both with and without jumps.
<br>
**PyS<sup>3</sup>DE** = **Py**thon Solver via **S**ympy + **S**ciPy/NumPy for **S**tochastic **D**ifferential **E**quations!

##Requirements:

1. <a href="http://sympy.org">Sympy</br>
2. <a href="http://www.scipy.org">Scipy and Numpy</a></br>
 
##Optional:

1. <a href="http://code.google.com/p/scitools/">scitools</a><br>
2. <a href="http://matplotlib.org">matplotlib</a>

##Installation

Copy **\_\_init\_\_.py** and **sde.py** into the directory, $Python/site-packages/pysde/


##Usages

* Symbolic Computation
<pre>
from sympy import *
from pysde import *
""" Main Codes Here """
x,dx,w,dw,t,dt,a=symbols('x dx w dw t dt a')
x0 =Symbol('x0'); t0 = Symbol('t0')
drift=2*x/(1+t)-a*(1+t)**2;diffusion=a*(1+t)**2
sol=SDE_solver(drift,diffusion,t0,x0)
pprint(sol)  
</pre>
Got
<pre>
       2 ⎛              2                2               2     ⎞
(t + 1) ⋅⎝- a⋅t⋅(t₀ + 1)  + a⋅t₀⋅(t₀ + 1)  + a⋅w⋅(t₀ + 1)  + x₀⎠
────────────────────────────────────────────────────────────────
                                   2                            
                           (t₀ + 1)                             
</pre>
* Numeric Computation
<pre>
import matplotlib.pylab as plt
from matplotlib import rc
rc('font',**{'family':'sans-serif','sans-serif':['Helvetica']})
rc('text', usetex=True)
""" setup picture info """
plt.figure(figsize=(5,2))
plt.ylim(-0.5,1.5)
""" Initial data """
x0=1.;t0=0.;tn=10.
x,dx=symbols('x dx')
[a,b,c,d]=[0,-1.,0,1.]
drift=a+b*x
diffusion=c+d*x#
nt=200
T= linspace(t0, tn, nt+1)
""" Numerical Computation"""
X=Euler(drift,diffusion,x0,t0,tn,nt)
X,Y=Milstein(drift,diffusion,x0,t0,tn,nt)
"""Make picture"""
plt.plot(T, X, color="blue", linewidth=2.5, linestyle="-", label="Euler")
plt.plot(T, X, color="red", linewidth=2.5, linestyle="--", label="Milstein")
plt.plot(T, np.exp(-T), color="green", linewidth=2.5, linestyle="--", label=r"$\exp(-t)$")
plt.ylim(X.min()-0.2, X.max()+0.2)
plt.title(r"$d X_t=-dt+d W_t,X_0=1$")
plt.legend()
plt.savefig('Milstein.eps')
</pre>
##Note

* Althought this module is tested in Python2.6~2.7, it can also run in Python3.x by using 2to3 converting the source code. It is also
tested on the notebook() interface of both Sage-5.x and IPython-1.
Or try <a href="https://github.com/cchuang2009/PyS-3DE-for-Python3">the sources of other branch</a>. This 
version gets rid of the scitools packages since it is developed based on &lt;  Python-3.x.

* **PyS<sup>3</sup>DE** also avails the **plot** function, sdeplot, based on *scitools*; but it
only works in python-2.x but not python-3.x since scitools is a python-2.x library. Thanks for Matplotlib
which provides plot functions, capable of doing high-performance pictures.

##DEMO

1. python code: http://diffusion.cgu.edu.tw/ftp/sde (demo.py)
2. TeXmacs with Python plugin: http://diffusion.cgu.edu.tw/ftp/sde (sdedemo.py)
3. TeXmacs with Python plugin: SDE with jumps http://diffusion.cgu.edu.tw/ftp/sde (sdejump.py)
4. Sage notebook(): http://diffusion.cgu.edu.tw/ftp/sde DiffusionJumps.sws, DiffusionJumps-1.sws

##Developer:


chu-ching huang: cchuang2009@gmail.com
