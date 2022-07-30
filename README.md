# Unity-Internship-Coding-Challenge
Solutions to Unity internship coding challenge phase.

**Part I**

[Challenge 1 - Plane Programming](https://learn.unity.com/tutorial/challenge-1-steer-a-plane-through-obstacles-in-the-sky?uv=2020.3) - Assets package with solution [here](Challenge_1_Solved.unitypackage).

[Challenge 2 - Play Fetch](https://learn.unity.com/tutorial/challenge-2-play-fetch-with-random-values-and-arrays?uv=2020.3) - Assets package with solution [here](Challenge_2_Solved.unitypackage).

**Part II**
*****
1. (a) and (b)

    (a) Describe the difference between a stack and a queue. (4 points)
    > They differ in the insertion and remotion methods. A stack follows the LIFO logic (Last In, First Out), in which elements are "pushed" in the beginning of the stack and "popped" on the same spot. On the other hand, the queue follows the FIFO logic (First In, First Out), in which the elements are inserted in the "head" of the queue and removed from the "tail". Given a same insertion order to both structures, removing elements from the queue will give the exactly insertion order, while removing from the stack will give the inverse order.

    (b) Describe a typical programming use for a queue. (4 points)
    > In the Breadth First Search (BFS), used to find the shortest path between two vertices in an unweighted graph, we start from an initial vertex, put its non-marked neighboors in the queue and mark it. From then on, we remove a vertex from the queue and do the same process until the target vertex is found or the queue is empty. Because of the FIFO logic, the vertex removed from the queue is always at a greater or equal distance from the starting one than the previous removed vertex, which gives us the certainty that we are finding the shortest path.
*****
2. (a) and (b)

    (a) Use C/C++ to show the structure of an element in a doubly-linked list in which each element holds a single character. Describe briefly what any pointers point to. (4 points)
    > We just need three atributes: id (identifying each vertex singularly), previous and next. These two last are pointers (memory adresses) that indicates the previous and the next elements relative to the element in question.
    ```cpp
    class ElementDoubleList{
        public:
            ElementDoubleList *previous, *next;
            char id;
    };
    ```

    b) Use C/C++ to show the operations necessary to insert a list element given a pointer to the new element and a pointer to the element after which the new element needs to be inserted. (5 points)
    > Using a `insertElement(ElementDoubleList *actual, ElementDoubleList *after)` function:
    ```cpp
    void insertElement(ElementDoubleList *actual, ElementDoubleList *after){
        actual->next = after;
        actual->previous = after->previous;
        after->previous = actual;
    }
    ```
*****
3. (a) and (b)

    (a) Use C/C++ to show the structure of an element of a sorted, binary tree in which each element contains a single character. Describe briefly what any pointers point to. (6 points)
    > Sorting the binary tree by the elements's singular ids, we have always a partial order relation between every pair of elements. We structure this order by having a left and right child of each element for elements with lesser or greater ids, respectively. To simplify, we  use an array of two pointers representing the left and right childs, in this exactly order.
    ```cpp
    class ElementBinTree{
        ElementBinTree *child[2];
        char id;
    };
    ```

    (b) Use C/C++ to show the operations necessary to locate the element in the sorted binary tree which matches a given character. (6 points)
    > Using a `findElement(ElementBinTree *root, char id)` function, with root being the element that isn't a child of any other element. If the element doesn't exist in the tree, we just return `NULL`. To spare a couple lines of code we can use the branchless programming technic of accessing an array index by an unique expression for two cases: `id > root->id` equals 0 if the id is lesser than the root id, otherwise it is equal to 1.
    ```cpp
    ElementBinTree* findElement(ElementBinTree *root, char id){
        while(*root != NULL){
            if (id == root->id)
                return root;
            root = root->child[id > root->id];
        }
        return NULL;
    }
    ```
*****
4. Compare the following function and macro definitions. In what cases will they produce different results and/or side effects? (4 points)
 
   * ```int square(int val) { return val*val; }```

   * ```#define square(val) (val*val)```
 
    > The first is a function that receives an integer value and returns it's square correctly. The second is a macro that will search for a function `square(x)` being used in the code and replace it with `(x*x)`. The problem with this second approach is when we use more than simple arguments in the function. For example: `square(x+1)` would be replaced by `(x+1*x+1)` that is equal to $2x+1$, not $x²$.
*****
5. Write a C function that converts a character string into a signed integer without using any library functions. Assume that the string contains a valid integer and no white space. (10 points)

    > Using a `srtToInt(string str)` function to convert integer strings with signal `+`, `-` or none: 
    ```cpp
    int srtToInt(string str){
        int answer = 0;
        int i = 0;
        if (str[0] < '0' or str[0] > '9')
            i = 1;
        while (i < str.length()){
            answer *= 10;
            answer += str[i]-'0';
            i++;
        }
        if (str[0] == '-')
            answer *= -1;
        return answer;
    }
    ```
*****
6. (a) and (b)

    (a) Given a 2D vector A in the x-y plane of length |A| and angle theta to the x-axis, give the equations for the x and y components of A. (4 points)
    > $(x,y) = (|A|*\cos(\theta), |A|*\sin(\theta))$.

    (b) Given the x,y,z components of a 3D vector A, give the equation for the angle between the vector and the x-y plane. (5 points)
    > Let $\phi$ be the angle between $A$ and the $x-y$ plane. Note that $\phi$ plus the angle of $A$ with the $z$ axis is equal to $90$. Then, $\phi = 90 - \arccos (\frac{A \cdot(0,0,1)}{|A|})$.
*****
7. (a) and (b)

    (a) Given a 3D point starting at position P1 and moving with constant velocity vector V, write an equation for position P2 of the point after elapsed time t. (5 points)
    > $P_2 = P_1 + V*t$.

    (b) Given a 3D point starting at position P1 and moving with initial velocity vector V and constant acceleration vector A, write an equation for the position P2 of the point after elapsed time t. (5 points)
    > $P_2 = P_1 + V*t + \frac{1}{2}*A*t^2$.
*****