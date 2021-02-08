---
layout: post
date: 2021-01-30 8:06
title: "Advent of code 2020 day 20"
category: docs
tags:
- documentation
comments: true

---
[Advent of code 2020](https://adventofcode.com/2020/day/20) day 20th problem arguably the most hardest problem I have ever solved
both in terms of complexity and also time taken to get the final output. If you want to know
more about why this was the hardest problem, various barriers I faced while solving the problem and how I have overcome barriers,
please continue reading this article. It is going to be a fun ride and a worth reading.

<!--more-->

## Advent of Code

In the month of December 2020, I have participated in a programming contest called [Advent of Code](https://adventofcode.com/) which is created by [Eric Wastl](https://twitter.com/ericwastl), 
with the recommendation from my colleague. Every year Eric creates problems set that covers topics such as regular expressions,
matrix operations, bitwise operations, recursive functions, depth first and breadth first search, mathematical problems such as Chinese Remainder Theorem,
binary search tree, stacks, queues, string combinations and permutations, importance of double-precision floating-point,
linked list representation as an array, so on and so forth. The contest opens from December 1st through 25th. I strongly
recommend this challenge to anyone who is looking to solve hard problems.

It was a fantastic experience for me getting to solve some of the toughest algorithmic problems I have ever come across.
One of the the problem which is the topic of the article is my favorite and the most challenging algorithmic problem I ever tackled.
It taught me so many things apart from technical perspective such as how to be patient solving tough problems, how to
strategically arrive to a solution, how helpful is divide and conquer approach among others. 

In the coming sections I am going to introduce the problem, challenges I faced at every tiny step I made and how
I have overcome those challenges to reach the end of tunnel!

## Day 20th problem

Given a set of two dimensional square matrix tiles each with a tileId, arrange the tiles to form a 2D square matrix image
such that the neighboring tiles should have the same values at the border. The tiles can be rotated or flipped or both so as to align with the neighbors.
Following is an example of how a tile looks like:

```$xslt
Tile 1217:
.#....#..#
#.#....###
##.#....#.
##...###..
###..#..#.
.#...##...
#.#..##...
#...#.##..
#..##....#
.##.#..#..
```

There are two subproblems:

1. Find the product of the tileIds of the borders in the final image. This should become trivial to solve as soon as the tiles are arranged.
2. Part 2 is the most toughest subproblem. After aligning the tiles, shave the edges and rotate or flip or perform both on the resultant image until
you find the following sea monsters pattern.

```$xslt
                  # 
#    ##    ##    ###
 #  #  #  #  #  #   
```
One you find sea monsters, count the remaining **#** that does't constitute sea monsters.

## My Github Code for day 20

If you wanted to look at the code, here is the link for [day 20 code](https://github.com/jitendra8911/advent-of-code/tree/master/src/day/20)

## Why was the problem hard to solve

1. Complexity in arranging the tiles adjacent to each other is proportional to time taken to find a robust algorithm
that satisfies neighbor tiles matching criteria. It took me about 2 weeks to come up with an algorithm that works.

2. Once the final image is obtained, finding the sea monsters using a regular expression was another mammoth task.
To give a brief idea, knowing the importance and difference between javascript regex methods matchAll and exec could unlock answer to the puzzle. 
But I learned difference between those methods while solving part 2 in a hard way.
More about it in coming sections.

## Arranging the tiles (Complexity 1)

Finding corners was simple. Just find tiles that have only 2 borders which are common with other tiles.
After solving part 1, I took the following approach to solve part2

#### First approach (non working solution)

I tried to build the final image by traversing the grid in undirected way. The algorithm is as follows:

1. Read the tiles. For each and every tile (call it source tile) do the following:
   1. If there is a destination tile that has a border in common with the source tile.
   2. If there is no such destination tile, try to rotate/flip source tile or the tile that is being compared to source
   depending on which can be rotated/flipped until one of the border of the two tiles align. 
   3. Maintain a link between the source and destination tiles. 
   Make sure both the source and destination tiles won't be rotated/flipped in future iterations.
   
This approach has following disadvantages:

1. We are not traversing the matrix in a fixed direction. Instead we are traversing in zigzag manner.

2. There is no easy way to compare the source and destination border after one of them is rotated/flipped.

3. There are chances of using the common borders of source and destination tiles while finding matched neighbors for other tiles.

4. Hard to maintain links between source and destination tile, i.e, whether destination tile is a left/right/top/bottom neighbor.

5. Hard to build image after the links are established.

#### Second approach (working solution)

The solution to build an image matrix is as follows:

1. It is guaranteed that all the corners have either a left neighbor or right neighbor.
2. Take any corner. Call it C1. Push it to stack
3. Check if C1 has right neighbor
   1. If it has, then find the right neighbor. Call it N1. Rotate/flip N1 until the left of N1 matches with right of N1. Push it to stack.
   2. If C1 doesn't have right neighbor, then find left neighbor. Call it N2. Rotate/flip N2 until the right of N2 matches with left of C1. Push N2 to stack.
   3. Repeat one of the above two steps for the current last tile in the stack until we don't find any neighbor.
   
4. At this point, we found all the tiles that are present in the top/bottom border of the image. If we traversed right to left of image matrix, then Col = 0. If we traversed left to right
then Col = n-1.
5. For each tile in the stack
   1. Pop the tile. Call it T1.
      1. Find the bottom/top neighbor of T1. Call it TN1. If bottom neighbor, row = 0. If top neighbor, row = n-1. Push T1 to image matrix to (row, col)
      2. Rotate flip TN1 so that top/bottom of TN1 matches with bottom/top of T1. If bottom neighbor, increment row or else decrement row. Push TN1 to (row,col).
      3. Find top/bottom neighbor of TN1 and repeat the above step until there are no neighbors.
      
If we take this approach we can successfully build the image matrix. Half the task is done. The remaining puzzle piece is to just find out sea monsters
from the image matrix and count number of `#` that is not part of sea monster. Initially what was thought to be straight forward turned out to be a nightmare.
Therefore it deserve an explanation in the following section on why it was complicated to find out sea monsters.

## Finding sea monsters (Complexity 2)

Now that the image is formed, we need to strip the borders of the tiles as per the problem's requirement. After the borders are stripped off,
we need to rotate/flip the final image until we find sea monsters.


#### First approach (non working solution)

After rotating/flipping the image:

1. I built a string of the resultant image.
2. I was finding sea monsters using string.match(). Even though I found sea monsters this way, I couldn't find the
exact number because of overlapping sea monsters, in which case string.match() will skip and not return the correct results.
This took me over a week to realize. Thanks to reddit user by name [davidlozzi](https://www.reddit.com/r/adventofcode/comments/kgo01p/2020_day_20_solutions/ghm9sej/)
whose solution helped me identify my mistake.

#### Second approach (working solution)

After rotating/flipping the image:

1. I built a string of the resultant image.
2. The regular expression to find sea monsters is 
`const regex = new RegExp('#.[^]{77}#....##....##....###.[^]{77}#..#..#..#..#..#...', 'g');`
3. Then execute `let match = regex.exec(image_matrix_string)`.
   1. If a match is found, increment the total number of sea monsters found and set the next index to start the search to `index + 1`.
   This way overlapping sea monsters can be found.
   2. Repeat the above step until no further sea monsters are found.
4. Finally count the number of `#` in the image matrix that is not part of sea monster. This is answer for part 2!!
