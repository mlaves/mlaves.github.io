---
layout: post
title:  'Graph theory on "House of Santa Claus"'
date:   2018-01-17 21:04:13 +0100
categories: jekyll update
---

The "House of Santa Clause" is a famous german drawing game and riddle. My grandfather introduced it to me when I was a little child. Its task is to draw a "house" with exactly 8 lines without lifting the pen or drawing a line twice. The drawing is accompanied by the simultaneously spoken rhyme of 8 syllables: "This is the house of San-ta Claus", or in the german original "Das ist das Haus vom Ni-ko-laus".

![Santa's House]({{ "/assets/HouseOfSantaClaus.gif" | absolute_url }})

*Fig. 1: A solution of [Santa's House](https://de.wikipedia.org/wiki/Haus_vom_Nikolaus#/media/File:Blender3D_HouseOfStNiclas.gif) by [SoylentGreen](https://commons.wikimedia.org/wiki/User:SoylentGreen) [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)*

## Numerical Solution

Everyone in Germany knows at least one solution to this problem. The question arises: "How many solutions exist?". Let's help ourselfs with brute force of computers! We first define a function that checks if a path is a solution to the problem and we then use this function to filter a list of possible solutions. Let's denote the blue spots in Fig. 2 as *nodes* and the lines between two nodes as *edges*. We quickly figure out, that a complete solution visits every edge once and every node twice, except for node 4. That is, every valid solution visits 9 nodes and we therefore write possible paths as a string of node numbers with length of 9, e.g. `'123153452'`.

<img src="{{"/assets/house_of_santa_nodes.svg" | absolute_url }}" width="150" height="150" alt="Nodes of Santa's House" />

*Fig. 2: The nodes of Santa's house*

Next, we write an edge as consecutive numbers of nodes, e.g. `'15'` or `'51'`. With this, we create a list containting all 8 possible edges once and deal with the reverse variant later.

```python
edges = ['15', '53', '34', '45', '52', '21', '13', '32']
```

Our filter function, which simply looks if every edge is present in the possible solution (in either direction) and returns `True` if so or `False` if otherwise.

```python
def is_solution(x):
    # convert to string so we can iterate over the elements
    x = str(x)
    
    # check if all edges are visited
    for e in edges:
        if e in x or e[::-1] in x:  # also check for reverse direction
            continue
        else:
            return False
    
    return True
```

In the last step, we create a list of acending numbers from `111111111` to `155555555` (assuming that we start at node `1`) and filter this list for solutions:

```python
possible_solutions = range(111111111, 155555555)
s = filter(is_solution, possible_solutions)
print(list(s))
```

Try it [here](https://repl.it/repls/ImperturbableDisfiguredMonads)!
This reveals 44 possible solutions when starting at node `1`:

```
123153452, 123154352, 123451352, 123453152, 123513452, 123543152, 125134532,
125135432, 125315432, 125345132, 125431532, 125435132, 132153452, 132154352,
132534512, 132543512, 134512352, 134512532, 134521532, 134523512, 134532152,
134532512, 135123452, 135125432, 135215432, 135234512, 135432152, 135432512,
152134532, 152135432, 152345312, 152354312, 153123452, 153125432, 153213452,
153254312, 153452132, 153452312, 154312352, 154312532, 154321352, 154325312,
154352132, 154352312
```

By looking at the results, we see that all solutions end at `2`. We can imagine, that if we start at `2` and reverse all found paths, we have 88 solutions.
But what if we do not restrict ourselfs to start at node `1` or `2`? Let's try it out:

```python
# CAUTION: this may take some time
possible_solutions = range(111111111,555555555)
s = list(filter(is_solution, possible_solutions))
print(len(s))
```

The result will be (drumroll): 88! Or to put it another way: You __have__ to start at node `1` or `2` to solve the problem. For the sake of completeness, all 88 results are given at the end of this post. But now, let's tackle this problem in a more mathematical way.

## Euler Path

The problem of "House of Santa Claus" can be modeled with graph theory. A graph is a mathematical structure, which models pairwise relations between objects. The objects are called vertices or nodes which are connected by edges or lines. Santa's house has 5 nodes and 8 edges. The graph is *undirected* as there is no given direction between two nodes connected by an edge. However, when trying to find solutions to Santa's house, you quickly find out that you have to start at the lower left node and end at the lower right one (as shown above).

More specifically, the problem of "House of Santa Claus" it is an *Eulerian path* problem where we want to find a path in a finite graph which visits every edge exactly once. When discussing the problem of the [Seven Bridges of Königsberg](https://en.wikipedia.org/wiki/Seven_Bridges_of_Königsberg) in 1736, Euler found out that an Eulerian path exists for graphs with exactly zero or two nodes having an odd degree. The degree of a node is its number of edges. If a graph has zero nodes with odd degree, the starting node will be the ending node, and is therefore called *Eulerian cycle*. Euler himself did not provide any proof for this theorem and it was not until 1873 that Carl Hierholzer published a proof in the article *Ueber die Möglichkeit, einen Linienzug ohne Wiederholung und ohne Unterbrechung zu umfahren*. In: Mathematische Annalen (1873) 6: 30. doi:[10.1007/bf01442866](https://doi.org/10.1007/bf01442866).  Santa's house has two nodes with degree of 3 (node 1 and 2) and the Eulerian path must start and end at them. There is no Eulerian cycle in Santa's house.

![Santa Claus]({{ "/assets/Jolly-old-saint-nick.gif" | absolute_url }})

*Fig. 3: Santa lives in this house (public domain by [Anrie](https://commons.wikimedia.org/wiki/File:Jolly-old-saint-nick.gif))*

However, when I started to think about this problem, I thought that graphy theory would provide me with some analytical solutions by e.g. solving some linear equations. To my limited knowledge, it seems that only *algorithmic* solutions exist, like the one above using brute force (trying out all possible ways). There are, at least, some more clever algorithms, like Fleury's algorithm or one provided by Carl Hierholzer. Even counting the numbers of possible Euler paths is a problem known to be #P-complete, which is a term from computational complexity theory. To my understanding, this translates to *intractable* or *infeasible*. Very disappointing.

## All 88 Solutions

```
253451321, 125435132, 234531251, 153452132, 213452351, 235431251, 125315432,
253215431, 123451352, 154312532, 235134521, 123154352, 132153452, 132543512,
231254351, 134521532, 254351321, 215325431, 152345312, 235125431, 135234512,
135215432, 213253451, 235215431, 125135432, 123153452, 253123451, 253451231,
231534521, 153254312, 215435231, 253213451, 253154321, 134532512, 254351231,
134512352, 215345231, 132534512, 152134532, 213523451, 154352132, 231543521,
234521531, 153125432, 213254351, 254312351, 254315321, 132154352, 235213451,
123453152, 234512531, 235431521, 213453251, 135432152, 134532152, 153452312,
153123452, 251235431, 134523512, 153213452, 254321351, 234521351, 213543251,
154321352, 251234531, 135125432, 125134532, 152135432, 234531521, 231253451,
234513521, 125345132, 254321531, 135432512, 123513452, 215235431, 135123452,
154352312, 123543152, 215234531, 125431532, 154312352, 215432531, 251354321,
251345321, 134512532, 152354312, 154325312
```
