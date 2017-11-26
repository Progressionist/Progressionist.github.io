---
title: "week 1"
draft: true
---
### I. Union-Find and Dynamic Connectivity Problem
#### 1. Quick Find
The first algorithm to solve dynamic connectivity problem is "quick find". 

For a list of number and their id's
$$ \begin{matrix} num:&0&1&2&3&4&5&6&7&8&9 \newline \hline id:&0&1&2&3&4&5&6&7&8&9 \end{matrix}$$

**Find**: if any two numbers' id are the same, then they are connected <br>
**Union**: when union two numbers p and q, change the first one q'id and all other numbers id is p to q. <br>
For example, if we have:
$$ \begin{matrix} num:&0&1&2&3&4&5&6&7&8&9 \newline \hline id:&0&1&1&8&8&0&0&7&8&8 \end{matrix}$$

and we want to **union(6, 1)**, then we'll get
$$ \begin{matrix} num:&0&1&2&3&4&5&6&7&8&9 \newline \hline id:&0&1&1&8&8&\color{red}{1}&\color{red}{1}&1&8&8 \end{matrix}$$

Although **Find** is very fast in Quick-Find algorithm, **Union** is too expensive.
Since for each Union operation, we need to go through the entire list to find the same id, 
it takes $N^2$ array access to process N union commands on N objects. And we will later know that 
an Quadratic time algorithm is too slow. 

The reason is that this type of algorithm don't scale with technology. For example, let's say an old computer holds 
10 object in the memory, and each operation cost 1 second. Use quick-find algorithm, we need 10 objects x 10 operations x 1 second =
100 second to touch everything in the memory. Lets say the latest computer is better, it holds 100 objects in the memory and operation only cost 
0.1 second, now we need 100 objects x 100 objects times 0.1 sec = 1000 seconds! That's 10 times slower than the older computer.
The key point here is that faster computer also contains more objects, if we use $N^2$ algorithm, the operation speed increase won't
catch the object size increase. <br>
The code implementation for quick-find is below:

    class QuickFind:
        def __init__(self, size):
            self.id = []
            for i in xrange(size):
                self.id.append(i)
    
        def union(self, num1, num2):
            temp = self.id[num1]
            for i in xrange(len(self.id)):
                if self.id[i] == temp:
                    self.id[i] = self.id[num2]
    
        def connected(self, num1, num2):
            return True if self.id[num1] == self.id[num2] else False

#### 2. Quick Union
In this algorithm: <br>
**Find**: is to check if p and q have the same root. <br>
**Union**: is to merge p and q, and set the id of p's root to the q's root. Notice, we're setting two numbers root 
to be the same, so we need to find both number's root first, then change the id. It's called quick-union since each
union operation we only change one id instead of all the same id (like we did in quick-find algorithm) <br>
For example we have a list and its tree-representation below:
![quick-union](https://user-images.githubusercontent.com/25803108/33235952-109cbcc2-d1fa-11e7-91c4-51af73cf0697.png)

now we want to ***union(7, 3)***, the id of 7 is 1, so the root of 7 is not itself, we then got number 1; the id of 1 is 
1, so we find 7's root which is 1.  We then find the id of 3 is 8, then the id of 8 is 8, so 3's root is 8. Finally
we change the root of 7, in this case number 1's id to the root of 3, this case number 8's id. The result will be:
![quick-union2](https://user-images.githubusercontent.com/25803108/33235969-eacee69a-d1fa-11e7-817c-5f15e253b93b.png)
The code implementation for quick-union is below:

    class QuickUnion:
        def __init__(self, size):
            self.id = []
            for i in xrange(size):
                self.id.append(i)
    
        def union(self, num1, num2):
            self.id[self.find_root(num1)] = self.id[self.find_root(num2)]
    
        def connected(self, num1, num2):
            return self.find_root(num1) == self.find_root(num2)
    
        def find_root(self, num):
            num_temp = num
            while self.id[num_temp] != num_temp:
                num_temp = self.id[num_temp]
            return num_temp
 
 Now let's compare the pros and cons of **Quick-Find** and **Quick-Union** algorithm:
 ![comparison](https://user-images.githubusercontent.com/25803108/33236044-9ce0c6fe-d1fc-11e7-93e3-ce13643a63ce.png)
Both need N operations to initilize (use 1 for loop); both need N operations to union; quick-union needs N operations to find
since it needs to find the root. Notice that the union and find cost the same, because union also use find to find the root<br>
Also, there're two defects for the quick-union algorithm: <br>
1. trees can get very tall <br>
2. Find is too expensie (could be N operations) <br>
It seems like quick union algorithm is even worse that the quick find, don't worry, we will next modify it to make it actually
useful.

#### 3. Weighted Quick Union
In weighted quick union algorithm we need to 2 extra things: <br>
1. maintain a new list that keep track the size of each tree <br>
2. when union, always link the root of smaller tree to the root of the larger tree. <br>
For example: If we have the list and its tree representation:
![weighted_quick_union](https://user-images.githubusercontent.com/25803108/33236145-4abe3d90-d1ff-11e7-8acf-98323ff0cb79.png)
and we want to **union(7, 3)**, we will have:
![weighted_quick_union2](https://user-images.githubusercontent.com/25803108/33236146-4c6aaf34-d1ff-11e7-97e5-d2cabacb5309.png)
We attach the smaller tree to the large one. **Notice**: we decide which tree to attach based on their sizes not their depths.

Now it's the fun part, if we use this weighted-quick-union algorithm, we claim that the depth of any node x's depth will be
at most $\lg N$ ($\lg$ is base-2 logarithm, $\log$ is base-10). Now, each time we union, if a node's depth increase, it will increase by 1,
and the size of its tree will at least doubles. (it got attach to a bigger tree, the bigger tree's size is >= to smaller tree). Now, 
how many times can a tree doubles when the over all size is N. Let's say the original size of the tree is 1, and it can only
doubles $\lg N$ times before exceed the total object number of N. 

If the we agree that a node's depth is at most $\lg N$, then that means the find operation in this algorithm is at most $\lg N$.
Remember we said that in quick-union algorithm, union and find are the same run time, because union also use find to get the root?
Boom! Our union operation's also $\lg N$. And now the weighted-quick-union algorithm takes $N\lg N$ access for N operations. This is 
the type of algorithm we are looking for, because, the increase of the runtime based on the size increase now it's much less compare to
quadratic algorithm. <br>
The code implementation for quick-find is below:

    class WeightedQuickUnion:
        def __init__(self, size):
            self.id = []
            self.size = numpy.ones(size)
            for i in xrange(size):
                self.id.append(i)
    
        def union(self, num1, num2):
            if self.size[num1] >= self.size[num2]:
                self.size[self.find_root(num1)] += self.size[self.find_root(num2)]
            else:
                self.size[self.find_root(num2)] += self.size[self.find_root(num1)]
        
        def connected(self, num1, num2):
            return self.find_root(num1) == self.find_root(num2)
    
        def find_root(self, num):
            num_temp = num
            while self.id[num_temp] != num_temp:
                self.id[num_temp] = self.id[self.id[num_temp]]
                num_temp = self.id[num_temp]
            return num_temp
            
#### 4. Weighted Quick Union with Path Compression
We can further improve this algorithm by adding a path compression function. Now the ideal path compression is when trying to 
find the root of a node, just move each node on that branch to the root. In practive, this is a little expensive, since we will only
know the root at the end of the loop, and need to maintain another list to record each node on that branch, and another loop to operate that. T
herefore, instead of move each node on that branch to the root, we just move to its parent's parent. This way, we can do 
this operation while we finding its root. And this is just one extra code in implementation, as shown below:

    class WeightedQuickUnionWithPathCompression:
        def __init__(self, size):
            self.id = []
            self.size = numpy.ones(size)
            for i in xrange(size):
                self.id.append(i)
    
        def union(self, num1, num2):
            if self.size[num1] >= self.size[num2]:
                self.size[self.find_root(num1)] += self.size[self.find_root(num2)]
                self.id[self.find_root(num2)] = self.id[self.find_root(num1)]
            else:
                self.size[self.find_root(num2)] += self.size[self.find_root(num1)]
                self.id[self.find_root(num1)] = self.id[self.find_root(num2)]
        
        def connected(self, num1, num2):
            return self.find_root(num1) == self.find_root(num2)
    
        def find_root(self, num):
            num_temp = num
            while self.id[num_temp] != num_temp:
                self.id[num_temp] = self.id[self.id[num_temp]]
                num_temp = self.id[num_temp]
            return num_temp
**Warning**: you should update the size first, because path compression will change the size of that tree.

In practice this algorithm is close to linear run time (very fast!)


### II. Analysis of Algorithms