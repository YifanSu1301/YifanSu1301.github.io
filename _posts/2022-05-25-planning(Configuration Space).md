---
layout: post
title:  "Planning - Configuration Space"
date:   2022-05-25 20:00
category: robotics
icon: git
keywords: planning, robotics
image: 2022-02-11-storyboard.png
preview: 1
---
# Robotics - Computational Motion Planning (Configuration Space)

- Since in real world, most of the robotics we are going to build can move continuously through space, configuration is a mathematical and conceptual tool to help us think it in a unified framework

- **Configuration Space Obstacle:** Defined by **Minkowski** sum of the obstacle and the robot shape

  <img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-16 下午12.36.06.png" alt="截屏2022-05-16 下午12.36.06" style="zoom:50%;" />

  <img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-16 下午12.37.57.png" alt="截屏2022-05-16 下午12.37.57" style="zoom:50%;" >

  ![截屏2022-05-16 下午12.39.51](/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-16 下午12.39.51-2719196.png)

  # Visibility Graph

  ![截屏2022-05-18 下午10.18.04](/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-18 下午10.18.04.png)

- **Reformulating planning problem framed on a continuous configuration space in terms of graph -> apply former algorithm**

- Visibility graph: draw an edge between any two vertices that can be connected by straight line that lies entirely in free space -> use graph search 

# Cell decomposition

- Devide the robot's free space into a set of simpler regions
- Then, form a graph where the nodes of the regions and edges indicates which regions are adjacent to each other.
- ![截屏2022-05-18 下午10.32.06](/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-18 下午10.32.06.png)



# Collision Detection

- Let x denote the coordinates of a point in configuration space.

- `CollisionCheck(x)` should return 0 if x is in free space and 1 if x results in a collision with the obstacles.

- <img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-18 下午10.40.55-2928084.png" alt="截屏2022-05-18 下午10.40.55" style="zoom:20%;" /><img src="/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-18 下午10.41.39-2928104.png" alt="截屏2022-05-18 下午10.41.39" style="zoom:20%;" />

- Test where the two triangles intersect by checking all of the sides on both triangles, and testing whether any of those sides act as separating lines 

  ![](/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-18 下午10.45.36-2928350-2928355.png)

- Use collision function to make a grid graph

  - assume two points are both in freespace and close enough, the line between them is in free space.

![截屏2022-05-18 下午10.49.43](/Users/andrewsu/我的云端硬盘/CMU/Summer 2022/Planning/截屏2022-05-18 下午10.49.43.png)