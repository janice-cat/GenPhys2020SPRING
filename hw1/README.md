# VP10: Non-ideal Capacitor

## [HW PDF](https://drive.google.com/file/d/1nKZOmtCD4nJeACdTGcAEUlqfQBtWzsH6/view)  
> In this semester, there would be no video explanation, **only hw PDF is provided**. But the programming concepts won't exceed what are taught during last semester, and you will learn in class the physics knowledeg on which each Vpython HW is based.

## Contents  

+ [Non-ideal Capacitor & Numerical Laplacian Solver](#i-non-ideal-capacitor--numerical-laplacian-solver)  
+ [Homework](#ii-homework)  

## I. Non-ideal Capacitor & Numerical Laplacian Solver
A parallel-plate capacitor, shown in the figure, has an infinite length in z-axis. The distance between the plates is d = 1 mm, the width of both plates is L = 5 mm, and the voltage is 100 Volt on the top plate and -100 Volt on the bottom. If we want to consider the edge effect of the non-ideal capacitor, we need to calculate numerically the total charge on each plate per meter length in z-axis in order to obtain the capacitance value per meter length in z-axis.  

<img width="240" height="140" src="../graph/hw1-1.png"/> 

From General Physics course, we already know that anywhere <img src="https://render.githubusercontent.com/render/math?math=\vec{E}=-(\frac{\partial{V}}{\partial{x}}\hat{x} %2B \frac{\partial{V}}{\partial{y}}\hat{y} %2B \frac{\partial{V}}{\partial{z}}\hat{z})" height=36 style="margin-bottom: -5px"/>. Now we choose an infinitesimal cube of volume <img src="https://render.githubusercontent.com/render/math?math=dxdydz" height=13/>. In the two faces perpendicular to the x-axis, we have the net electric flux for the two faces as   
<img src="https://render.githubusercontent.com/render/math?math=E_{x}(x %2B dx)dydz-E_{x}(x)dydz=(\frac{\partial{E_{x}}}{\partial{x}}dx)dydz=\frac{\partial{E_{x}}}{\partial{x}}dV" height=36 style="margin-bottom: -5px"/>.  

<img width="240" height="140" src="../graph/hw1-2.png"/>  

Similiarly the net flux for the two faces perpendicular to y-axis is <img src="https://render.githubusercontent.com/render/math?math=\frac{\partial{E_{y}}}{\partial{y}}dV" height=36 style="margin-bottom: -5px"/>, and the two faces to z-axis is <img src="https://render.githubusercontent.com/render/math?math=\frac{\partial{E_{z}}}{\partial{z}}dV" height=36 style="margin-bottom: -5px"/>. Therefore, the total flux around the cube is <img src="https://render.githubusercontent.com/render/math?math=\phi=(\frac{\partial{E_{x}}}{\partial{x}} %2B \frac{\partial{E_{y}}}{\partial{y}} %2B \frac{\partial{E_{z}}}{\partial{z}})dV" height=36 style="margin-bottom: -5px"/>. If no charge is inside this cube, by Gauss' Law, <img src="https://render.githubusercontent.com/render/math?math=\phi=\frac{q}{\epsilon_{0}}=0" height=36 style="margin-bottom: -5px"/>, meaning <img src="https://render.githubusercontent.com/render/math?math=\frac{\partial{E_{x}}}{\partial{x}} %2B \frac{\partial{E_{y}}}{\partial{y}} %2B \frac{\partial{E_{z}}}{\partial{z}}=0" height=36 style="margin-bottom: -5px"/>. With  <img src="https://render.githubusercontent.com/render/math?math=\vec{E}=-(\frac{\partial{V}}{\partial{x}}\hat{x} %2B \frac{\partial{V}}{\partial{y}}\hat{y} %2B \frac{\partial{V}}{\partial{z}}\hat{z})=E_{x}\hat{x} %2B E_{y}\hat{y} %2B E_{z}\hat{z}" height=36 style="margin-bottom: -5px"/>, it then becomes <img src="https://render.githubusercontent.com/render/math?math=\frac{\partial^2{V}}{\partial{x^2}} %2B \frac{\partial^2{V}}{\partial{y^2}} %2B \frac{\partial^2{V}}{\partial{z^2}}=0" height=36 style="margin-bottom: -5px"/>, which is called a Laplace's Equation and is usually written as <img src="https://render.githubusercontent.com/render/math?math=\nabla^2{V}=0" height=13/>. The operator <img src="https://render.githubusercontent.com/render/math?math=\nabla^2" height=13/> is called an Laplacian operator.  

Since in this problem, there is no charge variation along the z-axis, by symmetry, <img src="https://render.githubusercontent.com/render/math?math=E_{z}=0" height=13/> and <img src="https://render.githubusercontent.com/render/math?math=\frac{\partial^2{V}}{\partial{z^2}}=0"  height=36 style="margin-bottom: -5px"/> everywhere. We can reduce the 3-dimensional Laplace's Equation to 2-dimensonal, <img src="https://render.githubusercontent.com/render/math?math=\frac{\partial^2{V}}{\partial{x^2}} %2B \frac{\partial^2{V}}{\partial{y^2}}=0" height=36 style="margin-bottom: -5px"/>. With the condition that at the position of the top and bottom plates <img src="https://render.githubusercontent.com/render/math?math=V= %2B 100V" height=13/> and <img src="https://render.githubusercontent.com/render/math?math=-100V" height=13/> respectively, we can try to solve this Laplacian problem by the numerical Laplacian solver. The simplest numerical Laplacian solver is illustrated as the following and starts from the Taylor's expansion:  

<img src="https://render.githubusercontent.com/render/math?math=V(x %2B h,y) \approx V(x,y) %2B h\frac{\partial{V}}{\partial{x}} %2B \frac{h^2}{2}\frac{\partial^2{V}}{\partial{x^2}}" height=36 style="margin-bottom: -5px"/> <img src="https://render.githubusercontent.com/render/math?math=\qquad\qquad" height=36 style="margin-bottom: -5px"/><img src="https://render.githubusercontent.com/render/math?math=\qquad\qquad" height=36 style="margin-bottom: -5px"/><img src="https://render.githubusercontent.com/render/math?math=V(x,y %2B h) \approx V(x,y) %2B h\frac{\partial{V}}{\partial{y}} %2B \frac{h^2}{2}\frac{\partial^2{V}}{\partial{y^2}}" height=36 style="margin-bottom: -5px"/>  

<img src="https://render.githubusercontent.com/render/math?math=V(x-h,y) \approx V(x,y)-h\frac{\partial{V}}{\partial{x}}&plus;\frac{h^2}{2}\frac{\partial^2{V}}{\partial{x^2}}" height=36 style="margin-bottom: -5px"/> <img src="https://render.githubusercontent.com/render/math?math=\qquad\qquad" height=36 style="margin-bottom: -5px"/><img src="https://render.githubusercontent.com/render/math?math=\qquad\qquad" height=36 style="margin-bottom: -5px"/> <img src="https://render.githubusercontent.com/render/math?math=V(x,y-h) \approx V(x,y)-h\frac{\partial{V}}{\partial{y}} %2B \frac{h^2}{2}\frac{\partial^2{V}}{\partial{y^2}}" height=36 style="margin-bottom: -5px"/> 

We add the above four eqations and will obtain<img src="https://render.githubusercontent.com/render/math?math=V(x,y)=\frac{1}{4}[V(x %2B h,y) %2B V(x-h,y) %2B V(x,y %2B h) %2B V(x,y-h)]\qquad(*1)" height=36 style="margin-bottom: -5px"/>   

because <img src="https://render.githubusercontent.com/render/math?math=\frac{\partial^2{V}}{\partial{x^2}} %2B \frac{\partial^2{V}}{\partial{y^2}}=0" height=36 style="margin-bottom: -5px"/>.  

Therefore, the potential at each grid-point is simply the mean value of its nearest neighbors. To find the soulution one must fix the values of the grid-points on the boundaries or on the positions according to the required conditions and then iterate the potentials until successive results agree each other to within the desired tolerance. This usually can be done with many enough iterations.  

## II. Homework
### MUST (5%)
In the following program:  
**1.** We use the finite-difference methods for the grid points on the region of interest and set the potential on the top and bottom plates to be <img src="https://render.githubusercontent.com/render/math?math=\pm100V" height=13/>.  
**2.** We solve the 2-D Laplace's equation at each grid-point  
**3.** By taking the gradient of the potential, we obtain the electric field on x-y plane.  
**4.** By numerically integrating the Gauss surface, we obtain the total charge on the capacitor.  
**5.** Dividing the total charge by the voltage difference, we obtain the capacitance.  

Your job is to complete the template code for **2.**, **4.**, and **5.** and compare the value of **5.** to the value of an ideal parallel-plate capacitor.  
(Note: You can change this program easily to calculate the capacitance of a rectangular parallel-plate capacitor, i.e. the length in z is not infinite)  

```python
from numpy import * 
from vpython import *

epsilon = 8.854E-12 
N = 101
h = 1E-2/(N-1)
L, d= 5E-3,1E-3
V0 = 200
def solve_laplacian(u, u_cond, h, Niter=5000): 
	V = array(u)
	for i in range(Niter):
		V[u_cond] = u[u_cond]
		V[1:-1, 1:-1] = 0  # replace this 0 by your Laplacian Solver
	return V

def get_field(V, h):
	Ex, Ey = gradient(V)
	Ex, Ey = -Ex/h, -Ey/h 
	return Ex, Ey


u = zeros([N, N])
u[int(N/2)-int(L/h/2.0):int(N/2)+int(L/h/2.0), int(N/2) - int(d/h/2.0)] = -V0/2 
u[int(N/2)-int(L/h/2.0):int(N/2)+int(L/h/2.0), int(N/2) + int(d/h/2.0)] = V0/2 
u_cond = not_equal(u, 0)

V = solve_laplacian(u, u_cond, h)

scene = canvas(title='non-ideal capacitor', height=1000, width=1000, center = vec(N*h/2, N*h/2, 0))
scene.lights = []
scene.ambient=color.gray(0.99)
box(pos = vec(N*h/2 , N*h/2 - d/2 - h, 0), length = L, height = h/5, width = h)
box(pos = vec(N*h/2 , N*h/2 + d/2 - h, 0), length = L, height = h/5, width = h)

for i in range(N):
	for j in range(N):
		point = box(pos=vec(i*h, j*h, 0), length = h, height= h, width = h/10, color=vec((V[i,j]+100)/200,(100-V[i,j])/200,0.0) )

Ex, Ey = get_field(V, h)

for i in range(0, N):
	for j in range(0, N):
		ar = arrow(pos = vec( i*h, j*h, h/10), axis =vec (Ex[i,j]/2E9, Ey[i,j]/2E9, 0), shaftwidth = h/6.0, color=color.black)

#find Q, find C_nonideal = Q/(delta V) 
#Compare C_nonideal to C_ideal
```

### HW submission (PLZ be particularly aware!!)

+ Please upload a `zip` file (a compressed file) to CEIBA. Note that the filename extension should be `.zip`, and other format (e.g. `.rar` , `.tar` ...) is not allowed!!  
	> In this semester, please always upload the `zip` file even if there is only `must.py` to submit. (This would be helpful for me when downloading the hw. Thanks for the cooperation \~\~ :grin:)  

+ In the zip file, there will be **a directory whose name is your student ID.** The directory should contain 1 python scripts. Please name the script of must part: `must.py`.  


Example of submitted format: 
```
homework.zip
└── r07222016
    └── must.py
```

### Deadline
`03/26 THURS 22:00, Late submission deadline: 03/29 SUN 22:00`  
(for future hw, will make the release date and due date be on Sunday, as what we do in the last semester.)

### Grading Criteria (For Reference)    
Must  
    0: No Submission.  
    1: The program is totally not runnable.  
    2: Wrong with the animation (electric field lines).  
    3: Electric field lines is correct, but wrong with the answer (`C_nonideal`, `C_ideal`).  
    4: Electric field lines is correct, but wrong with the answer (`C_nonideal`, `C_ideal`).  
    5: You complete all the requirements, and they are all correct.   
        
