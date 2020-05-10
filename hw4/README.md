# VP13 RLC and Transient Behavior

## [HW PDF](https://drive.google.com/file/d/1ndl65XcoWwrAJ016tCGLgYfA_ZhW_zUK/view)

## Contents  

+ [I. Introduction](#i-introduction)  
+ [II. Homework](#ii-homework)  

## I. Introduction

<img src="../graph/circuit.png" height=200/>

An RLC circuit, with <img src="https://latex.codecogs.com/svg.latex?\dpi{300}&space;&space;\text{R}&space;=&space;30\&space;(\Omega)" height=16/>, <img src="https://latex.codecogs.com/svg.latex?\dpi{300}&space;\&space;\text{L}&space;=&space;200\&space;(\text{mH})" height=16/>, <img src="https://latex.codecogs.com/svg.latex?\dpi{300}&space;&space;\text{C}&space;=&space;20\&space;(\mu\textup{F})" height=16/>. The driving voltage source is

<img src="https://latex.codecogs.com/svg.latex?\dpi{300}&space;v(t)&space;=&space;\left\{\begin{matrix}&space;0,&space;&&space;\text{if}\&space;t&space;<&space;0&space;\\&space;36&space;\cdot&space;\sin(2\pi&space;f_d&space;t),&space;&&space;\text{if}\&space;0&space;\leq&space;t&space;<&space;12\text{T}&space;\\&space;0,&space;&&space;\text{if}\&space;12\text{T}&space;\leq&space;t&space;\end{matrix}\right." title="v(t) = \left\{\begin{matrix} 0, & \text{if}\ t < 0 \\ 36 \cdot \sin(2\pi f_d t), & \text{if}\ 0 \leq t < 12T \\ 0, & \text{if}\ 12T \leq t \end{matrix}\right."  height=80/>

\
where <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;f_d&space;=&space;120\&space;(\text{Hz})" title="f_d = 120\ (\text{Hz})" />, <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;\text{T}&space;=&space;1/f_d" title="\text{T} = 1/f_d" />.


## II. Homework

### (1)

Solve this circuit numerically and plot the voltage <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;v(t)" title="v(t)" /> and the current <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;i(t)" title="i(t)" /> as a function of <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;t" title="t" /> for <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;t&space;\in&space;[0,&space;20\text{T}]" title="t \in [0, 20\text{T}]" /> in `scene1` and the total energy <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;\text{E}(\text{T})" title="\text{E}(\text{T})" /> stored in the system in `scene2`.

### (2)

You will see a transient behavior of the current <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;i(t)" title="i(t)" /> before it reaches a steady-state oscillation around <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;t&space;=&space;9\text{T}" title="t = 9\text{T}" />. Find <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;I" title="I" />, the amplitude of the oscillating current, and <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;\phi" title="\phi" /> the phase constant of the oscillating current relative to the voltage source during the 9-th period. Compare them to the theoretical values.

### (3)

After the voltage is turned off at <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;t&space;=&space;12&space;\text{T}" title="t = 12 \text{T}" />, you will see both the current and the total energy decays. Find the time <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;t" title="t" /> such that the energy decays to 10% of the energy at the time the voltage is just turned off, i.e., <img src="https://latex.codecogs.com/svg.latex?\dpi{150}&space;\text{E}(t)&space;=&space;0.1\text{E}(t=12\text{T})" title="\text{E}(t) = 0.1\text{E}(t=12\text{T})" />.

### Template codes

```python
from vpython import *

fd = 120                # 120 Hz
# ===== Add your parameters here =====

t = 0
dt = 1.0 / (fd*5000)    # 5000 simulation points per cycle

scene1 = graph(align='left', xtitle='t', ytitle='i(A) blue, v(100V) red', background=vector(0.6, 0.9, 0.6))
scene2 = graph(align='left', xtitle='t', ytitle='Energy(J)', background=vector(0.6, 0.9, 0.6))

i_t = gcurve(color=color.blue, graph=scene1)
v_t = gcurve(color=color.red, graph=scene1)
E_t = gcurve(color=color.red, graph=scene2)

# ===== Your codes here =====
 
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
`05/31 SUN 22:00; Late submission deadline: 06/03 WED 22:00`  

### Grading Criteria (For Reference)    
Must  
	0: No Submission.  
	1: The program is totally not runnable.  
	2: Fail to correctly provide all of the requirements -- 1. i/v/E-t plots, 2.  calculation of current amplitude and phase, 3. calculation of 10% energy decay time.  
	3: Fail to correctly provide two of the requirements -- 1. i/v/E-t plots, 2.  calculation of current amplitude and phase, 3. calculation of 10% energy decay time.  
	4: Fail to correctly provide one of the requirements -- 1. i/v/E-t plots, 2.  calculation of current amplitude and phase, 3. calculation of 10% energy decay time.  
	5: You complete all the requirements, and they are all correct.  
    