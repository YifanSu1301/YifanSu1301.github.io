---
layout: post
title:  "Planning - Sensor Based"
date:   2022-05-25 20:00
category: robotics
icon: git
keywords: planning, robotics
image: 2022-02-11-storyboard.png
preview: 1
---

# Robotics - Computational Motion Planning (Artificial Potential Field - Sensor based)



## Two Main Function

<img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-25 下午6.24.33-3517481.png" alt="截屏2022-05-25 下午6.24.33" style="zoom:67%;" />

## Attractive Potential Field ($f_a$)

- When getting far away from the goal, $f_a$ will get larger quickly

  

**$$f_a(x) = c(\|x - x_g\|^2)$$**



- $x = \pmatrix {x1\\x2} $, the current position of the robot
- $x_g = \pmatrix{x_1^g \\ x_2^g}$, the desired goal location
- c is simply a constant scaling parameter

<img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-25 下午6.28.43.png" alt="截屏2022-05-25 下午6.28.43" style="zoom:66%;" />

## Repulsive Potential Field ($f_r$)

- When getting close to the obstacle, $f_r$ will get larger quickly.



$f_r(x) = \{\begin{array}{lr} \eta(\frac{1}{\rho(x)} - \frac{1}{d_0})^2 \text{           if $\rho(x) \leq$ $d_0$} \\ 0 \text{      if $\rho(x) \gt d_0$}\end{array}$



- $\rho(x)$, return distance to the closest obstacle from a given point in configuration space, x.

- $\eta$ and $d_0$ are a parameters that control the influence of the repulsive potential

  <img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-25 下午6.39.24-3518371.png" alt="截屏2022-05-25 下午6.39.24" style="zoom:67%;" />



**Add them up !!**

**<img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-25 下午6.40.02.png" alt="截屏2022-05-25 下午6.40.02" style="zoom:67%;" />**



### Gradient Based Control Strategy

- While robot position is not close enough to goal

  - Choose direction of robot velocity based on the gradient of the artificial potential field

    $v \varpropto -\nabla f(x) = - \pmatrix{\frac{\partial f(x)}{\partial x_1} \\ \frac{\partial f(x)}{\partial x_2}}$

  - choose an appropriate robot speed, $\|v\|$

### Quiver Plot

<img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-25 下午6.56.13.png" alt="截屏2022-05-25 下午6.56.13" style="zoom:67%;" />



- The arrows denote the direction of the gradient vector at various points in the configuration space
- <img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-25 下午6.57.08.png" alt="截屏2022-05-25 下午6.57.08" style="zoom:67%;" />

### NOTE

- May produce local minima  -> cannot find the destination -> use back tracking procedure to detect these situations and switch to different planning strategy.
- 