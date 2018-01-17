---
layout: post
title:  'Graph theory on "House of Santa Claus"'
date:   2018-01-17 21:04:13 +0100
categories: jekyll update
---

The "House of Santa Clause" is a famous german drawing game and riddle. My grandfather introduced it to me when I was a little child. Its task is to draw a "house" with exactly 8 lines without drawing a line twice. The drawing is accompanied by the simultaneously spoken rhyme of 8 syllables: "This is the house of San-ta Claus", or in the german original "Das ist das Haus vom Ni-ko-laus".

![Santa's House]({{ "/assets/HouseOfSantaClaus.gif" | absolute_url }})

*Fig. 1: A solution of [Santa's House](https://de.wikipedia.org/wiki/Haus_vom_Nikolaus#/media/File:Blender3D_HouseOfStNiclas.gif) by [SoylentGreen](https://commons.wikimedia.org/wiki/User:SoylentGreen) [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)*

The problem of "House of Santa Claus" can be modeled with graph theory. A graph is a mathematical structure, which models pairwise relations between objects. The objects are called vertices or nodes which are connected by edges or lines. Santa's house has 5 nodes and 8 edges. The graph is *undirected* as there is no given direction between two nodes connected by an edge. However, when trying to find solutions to Santa's house, you quickly find out that you have to start at the lower left node and end at the lower right one. More specifically, the problem of "House of Santa Claus" it is an *Eulerian path* problem where we want to find a path in a finite graph which visits every edge exactly once. When discussing the problem of the [Seven Bridges of Königsberg](https://en.wikipedia.org/wiki/Seven_Bridges_of_Königsberg) in 1736, Euler found out that an Eulerian path exists for graphs with exactly zero or two nodes having an odd degree. The degree of a node is its number of edges. If a graph has zero nodes with odd degree, the starting node will be the ending node, and is therefore called *Eulerian cycle*. Santa's house has two nodes with degree of 3 (node 1 and 2) and the Eulerian path must start and end at them.

![Santa Claus]({{ "/assets/Jolly-old-saint-nick.gif" | absolute_url }})

*Fig. 2: Santa lives in this house*

