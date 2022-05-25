---
layout: post
title:  "Planning - Graph Search"
date:   2022-05-25 20:00
category: robotics
icon: git
keywords: planning, robotics
image: 2022-02-11-storyboard.png
preview: 1
---

# Robotics - Computational Motion Planning (Graph Search)



## Grassfire Algorithm (BFS)

- Begin by marking the destination node with a distance of 0

- On every iteration find all the unmarked nodes adjacent to marked nodes and mark them with that distance value + 1

- The distance values produced by the grassfire algorithm indicate the smallest number of steps needed to move from each node to the goal

  <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午4.38.45.png" alt="截屏2022-05-06 下午4.38.45" style="zoom:33%;" />

- To move towards the destination from any node simply move towards the neighbor with the smallest distance value breaking ties arbitrarily. 



### Pseudo code

- For each node n in the graph

  - n.distance = Infinity

- Create an empty list

- goal.distance = 0, add goal to list

- While list not empty

  - Let current = first node in list, remove current from list

  - For each node, n that is adjacent to current

    if n.distance = Infinity

    ​	n.distance = current.distance + 1

    ​	add n to the back of the list

### Other example

<img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午4.41.10.png" alt="截屏2022-05-06 下午4.41.10" style="zoom:33%;" />

- In this example, the procedure terminates before the start node is marked indicating that no path exists

### Computational Complexity - Grassfire

**O(|V|)**: Linearly

Where |v| denotes the number of nodes of graph

- Number of nodes in a 2D grid $100 \times 100 = 10^4$
- Number of nodes in a 3D grid $100 \times 100 \times = 10^6$ 

**Grows exponentially as we increase the number of dimensions or degrees of freedom**



## Dijkstra's Algorithm

### Example

- $[(A,\infin),(B,\infin),(C,\infin),(D,\infin),(E,\infin),(F,\infin),(G,\infin)]$ and visited list $[]$

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午5.33.27.png" alt="截屏2022-05-06 下午5.33.27" style="zoom:10%;" /> 

  $[(A,0),(B,\infin),(C,\infin),(D,\infin),(E,\infin),(F,\infin),(G,\infin)]$ and visited list $[A]$

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午5.56.17.png" alt="截屏2022-05-06 下午5.56.17" style="zoom:10%;" /> based on adjacent list, update the distance . $[(A,0),(B,1),(C,\infin),(D,2),(E,\infin),(F,5),(G,\infin)]$ 

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午5.58.25.png" alt="截屏2022-05-06 下午5.58.25" style="zoom:10%;" /> Since B has the **smallest** distance from A and B is not in visited list, so we choose B as next node we will visit. 

  visited list $[A,B]$

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午6.00.55.png" alt="截屏2022-05-06 下午6.00.55" style="zoom:10%;" /> update the distance 

  $[(A,0),(B,1),(C,8),(D,\textbf{2}),(E,\infin),(F,5),(G,\infin)]$ since $2 < 3$ the distance to D don't change.

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午6.02.43.png" alt="截屏2022-05-06 下午6.02.43" style="zoom:10%;" /> Visit D 

  visited list $[A,B,D]$

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午6.03.34.png" alt="截屏2022-05-06 下午6.03.34" style="zoom:10%;" /> Update the distance 

  $[(A,0),(B,1),(C,\textbf{5}),(D,2),(E,\infin),(F,5),(G,10)]$

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午6.05.56.png" alt="截屏2022-05-06 下午6.05.56" style="zoom:10%;" /> visit F, since now F is with least distance to A and not in visited list, then update 

  visited list$[A,B,D,F]$

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午6.07.04.png" alt="截屏2022-05-06 下午6.07.04" style="zoom:10%;" /> Update distance 

  $[(A,0),(B,1),(C,\textbf{5}),(D,2),(E,\infin),(F,5),(G,9)]$

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午6.07.55.png" alt="截屏2022-05-06 下午6.07.55" style="zoom:10%;" /> visited C, and update 

  visited list $[A,B,C,D,F]$

- <img src="/Users/andrewsu/Library/Application Support/typora-user-images/截屏2022-05-06 下午6.09.20.png" alt="截屏2022-05-06 下午6.09.20" style="zoom:10%;" /> Update distance 

  $[(A,0),(B,1),(C,5),(D,2),(E,6),(F,5),(G,9)]$

- visited E, we knoe the shortest way to E is 6.

### Pseudo code

- For each node n in the graph
  - n.distance = Infinity

- Create an empty list.

- Start.distance = 0, add start to list

- While list not empty

  - Let current = node in the list with the smallest distance, remove current from list.

  - For each node, n that is adjacent to current

    if n.distance > current.distance + length of edge from n to current

    ​	n.distance = current.distance + length of edge from n to current

    ​	n.parent = current

    ​	add n to list if it is not there already.



### Computational Complexity 

- A naive version will be **$O(|V|^2)$**
- By keeping the list of nodes sorted using  priority queue $O((|E|+|V|)log|V|))$, where |V| denotes the number of nodes in the graph and |E| denotes the number of edges



![img](https://1.bp.blogspot.com/-mybTIhrG_L0/XXIjdQjakOI/AAAAAAAAMwU/SB7L9Y9WRCEsJnW3_NrMBt7OOXL0_6ScQCLcBGAs/s1600/ezgif-1-54c497cb7a46.gif)

*Dijkstra/Grassfire Algorithm



**CODE：**

```matlab
function [route,numExpanded] = DijkstraGrid (input_map, start_coords, dest_coords)
% Run Dijkstra's algorithm on a grid.
% Inputs : 
%   input_map : a logical array where the freespace cells are false or 0 and
%   the obstacles are true or 1
%   start_coords and dest_coords : Coordinates of the start and end cell
%   respectively, the first entry is the row and the second the column.
% Output :
%    route : An array containing the linear indices of the cells along the
%    shortest route from start to dest or an empty array if there is no
%    route. This is a single dimensional vector
%    numExpanded: Remember to also return the total number of nodes
%    expanded during your search. Do not count the goal node as an expanded node.


% set up color map for display
% 1 - white - clear cell
% 2 - black - obstacle
% 3 - red = visited
% 4 - blue  - on list
% 5 - green - start
% 6 - yellow - destination

cmap = [1 1 1; ...
        0 0 0; ...
        1 0 0; ...
        0 0 1; ...
        0 1 0; ...
        1 1 0; ...
        0.5 0.5 0.5];

colormap(cmap);

% variable to control if the map is being visualized on every
% iteration
drawMapEveryTime = true;

[nrows, ncols] = size(input_map);

% map - a table that keeps track of the state of each grid cell
map = zeros(nrows,ncols);

map(~input_map) = 1;   % Mark free cells
map(input_map)  = 2;   % Mark obstacle cells

% Generate linear indices of start and dest nodes
start_node = sub2ind(size(map), start_coords(1), start_coords(2));
dest_node  = sub2ind(size(map), dest_coords(1),  dest_coords(2));

map(start_node) = 5;
map(dest_node)  = 6;

% Initialize distance array
distanceFromStart = Inf(nrows,ncols);

% For each grid cell this array holds the index of its parent
parent = zeros(nrows,ncols);

distanceFromStart(start_node) = 0;

% keep track of number of nodes expanded 
numExpanded = 0;

% Main Loop
while true
    
    % Draw current map
    map(start_node) = 5;
    map(dest_node) = 6;
    
    % make drawMapEveryTime = true if you want to see how the 
    % nodes are expanded on the grid. 
    if (drawMapEveryTime)
        image(1.5, 1.5, map);
        grid on;
        axis image;
        drawnow;
    end
    
    % Find the node with the minimum distance
    [min_dist, current] = min(distanceFromStart(:));
    
    if ((current == dest_node) || isinf(min_dist))
        break;
    end;
    
    % Update map
    map(current) = 3;         % mark current node as visited
    distanceFromStart(current) = Inf; % remove this node from further consideration
    
    % Compute row, column coordinates of current node
    [i, j] = ind2sub(size(distanceFromStart), current);
    
   % ********************************************************************* 
    % YOUR CODE BETWEEN THESE LINES OF STARS
    
    % Visit each neighbor of the current node and update the map, distances
    % and parent tables appropriately.
    
    ii=0;
    jj=0;
    if (i>1 && i<=nrows)
        ii = i-1;
        jj = j;
        if (map(ii,jj)~=2 && map(ii,jj)~=3 && map(ii,jj)~=5)
            map(ii,jj) = 4;
            parent(ii,jj) = current;
            distanceFromStart(ii,jj) = min_dist+1;
        end
    end
    if (i>=1 && i<nrows)
        ii = i+1;
        jj = j;
        if (map(ii,jj)~=2 && map(ii,jj)~=3 && map(ii,jj)~=5)
            map(ii,jj) = 4;
            parent(ii,jj) = current;
            distanceFromStart(ii,jj) = min_dist+1;
        end
    end
    if (j>1 && j<=ncols)
        jj = j-1;
        ii = i;
        if (map(ii,jj)~=2 && map(ii,jj)~=3 && map(ii,jj)~=5)
            map(ii,jj) = 4;
            parent(ii,jj) = current;
            distanceFromStart(ii,jj) = min_dist+1;
        end
    end
    if (j>=1 && j<ncols)
        jj =j+1;
        ii = i;
        if (map(ii,jj)~=2 && map(ii,jj)~=3 && map(ii,jj)~=5)
            map(ii,jj) = 4;
            parent(ii,jj) = current;
            distanceFromStart(ii,jj) = min_dist+1;
        end
    end
    
    numExpanded = numExpanded + 1;
    
    
    %*********************************************************************

end

%% Construct route from start to dest by following the parent links
if (isinf(distanceFromStart(dest_node)))
    route = [];
else
    route = [dest_node];
    
    while (parent(route(1)) ~= 0)
        route = [parent(route(1)), route];
    end
    
        % Snippet of code used to visualize the map and the path
    for k = 2:length(route) - 1        
        map(route(k)) = 7;
        pause(0.1);
        image(1.5, 1.5, map);
        grid on;
        axis image;
    end
end

end

```





## A* Algorithm

- Best first search algorithm
- incorporating a heurisitic function that guides the path planner

### 	Heuristic Functions

- map every node in the graph to a non-negative value

- Heuristic Function Criteria:

  - H(goal) = 0

  - For any 2 adjacent nodes x and y

    $H(x)\leq H(y) + d(x,y)$

    $d(x,y) = weight / length$ of edge from x to y

- These properties ensure that for all nodes, n

  - $H(n)\leq length$ of shortest path from n to goal.

- For path planning on a grid the following 2 heuristic functions are often used:

  - Euclidean distance

  $$
  H(x_n,y_n) = \sqrt{(x_n - x_g)^2 + (y_n-y_g)^2}
  $$

  - Manhattan Distance 
    $$
    H(x_n,y_n) = |(x_n - x_g)| + |(y_n - y_g)|
    $$
    where $(x_n,y_n)$ denotes the coordinates of the node n and $(x_g, y_g)$ denotes the coordinate of the goal.

### Pseudo code

- For each node n in the graph
  - n.f = Infinity, n.g = Infinity

- Create an empty list

- Start.g = 0, start.f = H(start) add start to list

- While list not empty

  - Let current = node in the list with the smallest f value, remove current from list

  - if (current == goal node) report success

  - For each node, n that is adjacent to current

    - if (n.g > (current. g + cost of edge from n to current))

      n.g = current.g + cost of edge from n to current

      n.f = n.g + H(n)

      n.parent = current

      add n to list if it isn't there already

<img src="https://1.bp.blogspot.com/-IrOAHxJ2mwI/XXIjmVefamI/AAAAAAAAMwY/AvP1jHHY4rYXMCnuWnhCzfwai377RiJjwCLcBGAs/s320/ezgif-1-64c3c2a743f0.gif" alt="img" style="zoom:150%;" />

NOTE: 

1. **g** = the distance between the current node and start location
2. **h** = the estimated movement cost to move from that given square on the grid to the final destination. 
3. **f** = the sum of the distance between the node and the start and the estimate for how much distance is left to go between that node and the goal location.



**CODE:**

```matlab
function [route,numExpanded] = AStarGrid (input_map, start_coords, dest_coords)
% Run A* algorithm on a grid.
% Inputs : 
%   input_map : a logical array where the freespace cells are false or 0 and
%   the obstacles are true or 1
%   start_coords and dest_coords : Coordinates of the start and end cell
%   respectively, the first entry is the row and the second the column.
% Output :
%    route : An array containing the linear indices of the cells along the
%    shortest route from start to dest or an empty array if there is no
%    route. This is a single dimensional vector
%    numExpanded: Remember to also return the total number of nodes
%    expanded during your search. Do not count the goal node as an expanded node. 

% set up color map for display
% 1 - white - clear cell
% 2 - black - obstacle
% 3 - red = visited
% 4 - blue  - on list
% 5 - green - start
% 6 - yellow - destination

cmap = [1 1 1; ...
    0 0 0; ...
    1 0 0; ...
    0 0 1; ...
    0 1 0; ...
    1 1 0; ...
    0.5 0.5 0.5];

colormap(cmap);

% variable to control if the map is being visualized on every
% iteration
drawMapEveryTime = true;

[nrows, ncols] = size(input_map);

% map - a table that keeps track of the state of each grid cell
map = zeros(nrows,ncols);

map(~input_map) = 1;   % Mark free cells
map(input_map)  = 2;   % Mark obstacle cells

% Generate linear indices of start and dest nodes
start_node = sub2ind(size(map), start_coords(1), start_coords(2));
dest_node  = sub2ind(size(map), dest_coords(1),  dest_coords(2));

map(start_node) = 5;
map(dest_node)  = 6;

% meshgrid will `replicate grid vectors' nrows and ncols to produce
% a full grid
% type `help meshgrid' in the Matlab command prompt for more information
parent = zeros(nrows,ncols);

% 
[X, Y] = meshgrid (1:ncols, 1:nrows);

xd = dest_coords(1);
yd = dest_coords(2);

% Evaluate Heuristic function, H, for each grid cell
% Manhattan distance
H = abs(X - xd) + abs(Y - yd);
H = H';
% Initialize cost arrays
f = Inf(nrows,ncols);
g = Inf(nrows,ncols);

g(start_node) = 0;
f(start_node) = H(start_node);

% keep track of the number of nodes that are expanded
numExpanded = 0;

% Main Loop

while true
    
    % Draw current map
    map(start_node) = 5;
    map(dest_node) = 6;
    
    % make drawMapEveryTime = true if you want to see how the 
    % nodes are expanded on the grid. 
    if (drawMapEveryTime)
        image(1.5, 1.5, map);
        grid on;
        axis image;
        drawnow;
    end
    
    % Find the node with the minimum f value
    [min_f, current] = min(f(:));
    
    if ((current == dest_node) || isinf(min_f))
        break;
    end;
    
    % Update input_map
    map(current) = 3;
    f(current) = Inf; % remove this node from further consideration
    
    % Compute row, column coordinates of current node
    [i, j] = ind2sub(size(f), current);
    
    % *********************************************************************
    % ALL YOUR CODE BETWEEN THESE LINES OF STARS
    % Visit all of the neighbors around the current node and update the
    % entries in the map, f, g and parent arrays
    %
    
    ii=0;
    jj=0;
    if (i>1 && i<=nrows) %% UP
        ii = i-1;
        jj = j;
        if (map(ii,jj)~=2 && map(ii,jj)~=3 && map(ii,jj)~=5)
            if g(ii,jj) > (g(i,j) + (H(ii,jj)-H(i,j)))
                g(ii,jj) = g(i,j) + (H(ii,jj)-H(i,j));
                f(ii,jj) = g(ii,jj) + H(ii,jj);
                map(ii,jj) = 4;
                parent(ii,jj) = current;
            end
        end
    end
    if (j>=1 && j<ncols) %RIGHT
        jj =j+1;
        ii = i;
        if (map(ii,jj)~=2 && map(ii,jj)~=3 && map(ii,jj)~=5)
            if g(ii,jj) > (g(i,j) + (H(ii,jj)-H(i,j)))
                g(ii,jj) = g(i,j) + (H(ii,jj)-H(i,j));
                f(ii,jj) = g(ii,jj) + H(ii,jj);
                map(ii,jj) = 4;
                parent(ii,jj) = current;
            end
        end
    end
    if (i>=1 && i<nrows) % DOWN
        ii = i+1;
        jj = j;
        if (map(ii,jj)~=2 && map(ii,jj)~=3 && map(ii,jj)~=5)
            if g(ii,jj) > (g(i,j) + (H(ii,jj)-H(i,j)))
                g(ii,jj) = g(i,j) + (H(ii,jj)-H(i,j));
                f(ii,jj) = g(ii,jj) + H(ii,jj);
                map(ii,jj) = 4;
                parent(ii,jj) = current;
            end
        end
    end
    if (j>1 && j<=ncols) % LEFT
        jj = j-1;
        ii = i;
        if (map(ii,jj)~=2 && map(ii,jj)~=3 && map(ii,jj)~=5)
            if g(ii,jj) > (g(i,j) + (H(ii,jj)-H(i,j)))
                g(ii,jj) = g(i,j) + (H(ii,jj)-H(i,j));
                f(ii,jj) = g(ii,jj) + H(ii,jj);
                map(ii,jj) = 4;
                parent(ii,jj) = current;
            end
        end
    end
    
    
    numExpanded = numExpanded + 1;
    
    f(current) = Inf; 
    
    
    
    %*********************************************************************
    
    
end

%% Construct route from start to dest by following the parent links
if (isinf(f(dest_node)))
    route = [];
else
    route = [dest_node];
    
    while (parent(route(1)) ~= 0)
        route = [parent(route(1)), route];
    end

    % Snippet of code used to visualize the map and the path
    for k = 2:length(route) - 1        
        map(route(k)) = 7;
        pause(0.1);
        image(1.5, 1.5, map);
        grid on;
        axis image;
    end
end

end

```


