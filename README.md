Download Link: https://assignmentchef.com/product/solved-csci1913-project-2
<br>
For this project, you will implement an efficient algorithm to sort linear singly-linked lists of integers. (We’ll discuss algorithms that sort arrays later in the course.) The project is intended to give you some practice working with linked data structures.

<ol>

 <li></li>

</ol>

To start, we need a notation for lists of integers. We’ll write something like [5, 8, 4, 9, 1, 2, 3, 7, 6] to mean such a list. This list has nine nodes: its first node contains a 5, its second node contains an 8, its third node contains a 4, etc., all the way to its ninth node, which contains a 6. We’ll write an empty list of integers as []. Java <em>does not</em> use this notation, so don’t put it in your programs.

We want to sort lists like these into <em>nondecreasing order.</em> That means that the integers in the list don’t decrease from left to right. For example, if we sort [2, 3, 1, 1, 2] into nondecreasing order, then we get [1, 1, 2, 2, 3]. Similarly, if we sort [5, 8, 4, 9, 1, 2, 3, 7, 6] into nondecreasing order, then we get [1, 2, 3, 4, 5, 6, 7, 8, 9]. We’ll use this list as a running example in the rest of this description.

We also want our sorting algorithm to be as efficient as possible. To explain what we mean by that, let’s consider an inefficient sorting algorithm. It might sort a list by traversing it, looking for pairs of adjacent integers that are in the wrong order, like 8 and 4 in the list shown above. Whenever it finds such a pair of integers, it exchanges their positions, so that 4 now comes before 8. The algorithm might repeatedly traverse the list in this way, exchanging integers until all are in the right order. Although this algorithm is simple, it needs <em>O</em>(<em>n</em>²) comparisons to sort <em>n</em> integers.

The sorting algorithm we’ll describe here is more complex, but also more efficient. It works without exchanging adjacent integers, and without traversing lists repeatedly, both of which can make a sorting algorithm slow. Our algorithm needs only <em>O</em>(<em>n</em> log <em>n</em>) comparisons to sort a list of <em>n</em> integers. The algorithm works in four phases: <em>testing</em>, <em>halving</em>, <em>sorting</em>, and <em>combining.</em> We’ll describe each phase in detail.

<strong>Testing.</strong> Suppose that the variable <em>unsorted</em> is an unsorted list of integers that we want to sort. We test if <em>unsorted</em> has length 0 or 1. If so, then the list is already sorted, so the algorithm simply stops and returns <em>unsorted</em> as its result.

<strong>Halving.</strong> In this phase, <em>unsorted</em> has two or more integers. We split <em>unsorted</em> into two halves, called <em>left</em> and <em>right,</em> with approximately equal lengths. The order of integers within <em>left</em> and <em>right</em> doesn’t matter. We start (step 01) with <em>left</em> and <em>right</em> as empty lists. Then, for odd numbered steps (01, 03, etc.) we delete the first integer from <em>unsorted</em> and add it to the front of <em>left.</em> For even numbered steps (02, 04, etc.), we delete the first integer from <em>unsorted</em> and add it to the front of <em>right</em> instead. We continue in this way until <em>unsorted</em> becomes empty.

<table width="312">

 <tbody>

  <tr>

   <td width="44">  <strong>STEP</strong></td>

   <td width="78">  <strong><em>left</em></strong></td>

   <td width="62">  <strong><em>right</em></strong></td>

   <td width="129">  <strong><em>unsorted</em></strong></td>

  </tr>

  <tr>

   <td width="44"> 01</td>

   <td width="78"> []</td>

   <td width="62"> []</td>

   <td width="129"> [5, 8, 4, 9, 1, 2, 3, 7, 6]</td>

  </tr>

  <tr>

   <td width="44"> 02</td>

   <td width="78"> [5]</td>

   <td width="62"> []</td>

   <td width="129"> [8, 4, 9, 1, 2, 3, 7, 6]</td>

  </tr>

  <tr>

   <td width="44"> 03</td>

   <td width="78"> [5]</td>

   <td width="62"> [8]</td>

   <td width="129"> [4, 9, 1, 2, 3, 7, 6]</td>

  </tr>

  <tr>

   <td width="44"> 04</td>

   <td width="78"> [4, 5]</td>

   <td width="62"> [8]</td>

   <td width="129"> [9, 1, 2, 3, 7, 6]</td>

  </tr>

  <tr>

   <td width="44"> 05</td>

   <td width="78"> [4, 5]</td>

   <td width="62"> [9, 8]</td>

   <td width="129"> [1, 2, 3, 7, 6]</td>

  </tr>

  <tr>

   <td width="44"> 06</td>

   <td width="78"> [1, 4, 5]</td>

   <td width="62"> [9, 8]</td>

   <td width="129"> [2, 3, 7, 6]</td>

  </tr>

  <tr>

   <td width="44"> 07</td>

   <td width="78"> [1, 4, 5]</td>

   <td width="62"> [2, 9, 8]</td>

   <td width="129"> [3, 7, 6]</td>

  </tr>

  <tr>

   <td width="44"> 08</td>

   <td width="78"> [3, 1, 4, 5]</td>

   <td width="62"> [2, 9, 8]</td>

   <td width="129"> [7, 6]</td>

  </tr>

  <tr>

   <td width="44"> 09</td>

   <td width="78"> [3, 1, 4, 5]</td>

   <td width="62"> [7, 2, 9, 8]</td>

   <td width="129"> [6]</td>

  </tr>

  <tr>

   <td width="44"> 10</td>

   <td width="78"> [6, 3, 1, 4, 5]</td>

   <td width="62"> [7, 2, 9, 8]</td>

   <td width="129"> []</td>

  </tr>

 </tbody>

</table>

We do the halving phase this way because it’s easy to delete an integer from the front of a linked list (as in a linked stack), and easy to add a new integer to the front of a linked list (again as in a linked stack). Also, it works without having to know the length of <em>unsorted.</em>

<strong>Sorting.</strong> Now we have two unsorted lists from the halving phase, <em>left</em> and <em>right.</em> In the example, <em>left</em> is [6, 3, 1, 4, 5], and <em>right</em> is [7, 2, 9, 8]. We sort <em>left</em> and <em>right</em> into nondecreasing order, by recursively using the sorting algorithm (the same one we’re describing!) on both lists. After that, <em>left</em> is [1, 3, 4, 5, 6], and <em>right</em> is [2, 7, 8, 9]. The recursion always terminates, because <em>left</em> and <em>right</em> are shorter than the original list <em>unsorted,</em> so they will eventually have only one integer, stopping the algorithm during its testing phase.

<strong>Combining.</strong> Here we combine <em>left</em> and <em>right</em> into one sorted list, called <em>sorted,</em> which is initially empty (step 01). We look at the first integers from <em>left</em> and <em>right,</em> choosing the one that’s smallest. If the integer from <em>left</em> is smallest, then we delete it and add it to the end of <em>sorted</em> (as in step 01). If the integer from <em>right</em> is smallest, then we delete it and add it to the end of <em>sorted</em> (as in step 02). If both integers are equal, then we can do either one. We continue in this way until <em>left</em> or <em>right</em> becomes empty.

<table width="274">

 <tbody>

  <tr>

   <td width="41"> <strong>STEP</strong></td>

   <td width="24"> </td>

   <td width="66"> <strong><em>sorted</em></strong></td>

   <td width="78"> <strong><em>left</em></strong></td>

   <td width="65"> <strong><em>right</em></strong></td>

  </tr>

  <tr>

   <td width="41"> 01</td>

   <td width="24"> []</td>

   <td width="66"> </td>

   <td width="78"> [1, 3, 4, 5, 6]</td>

   <td width="65"> [2, 7, 8, 9]</td>

  </tr>

  <tr>

   <td width="41"> </td>

   <td width="24"> </td>

   <td width="66"> </td>

   <td width="78"> </td>

   <td width="65"> </td>

  </tr>

 </tbody>

</table>

02        [1]                        [3, 4, 5, 6]        [2, 7, 8, 9]

<table width="274">

 <tbody>

  <tr>

   <td width="41"> 03</td>

   <td width="90"> [1, 2]</td>

   <td width="78"> [3, 4, 5, 6]</td>

   <td width="65"> [7, 8, 9]</td>

  </tr>

  <tr>

   <td width="41"> 04</td>

   <td width="90"> [1, 2, 3]</td>

   <td width="78"> [4, 5, 6]</td>

   <td width="65"> [7, 8, 9]</td>

  </tr>

  <tr>

   <td width="41"> 05</td>

   <td width="90"> [1, 2, 3, 4]</td>

   <td width="78"> [5, 6]</td>

   <td width="65"> [7, 8, 9]</td>

  </tr>

  <tr>

   <td width="41"> 06</td>

   <td width="90"> [1, 2, 3, 4, 5]</td>

   <td width="78"> [6]</td>

   <td width="65"> [7, 8, 9]</td>

  </tr>

  <tr>

   <td width="41"> 07</td>

   <td width="90"> [1, 2, 3, 4, 5, 6]</td>

   <td width="78"> []</td>

   <td width="65"> [7, 8, 9]</td>

  </tr>

 </tbody>

</table>

At this point, one of <em>left</em> and <em>right</em> may not be empty (step 07). If that happens, then we add the entire nonempty list to the end of <em>sorted. </em>In the example, we get the list [1, 2, 3, 4, 5, 6, 7, 8, 9]. It’s sorted into nondecreasing order, so we stop the sorting algorithm and return this list as its result.

We did the combining phase this way because it’s easy to delete an integer from the front of a linked list (as in a linked stack) and also easy to add an integer to the end of a linked list (as in a linked queue). It’s also easy to add <em>left</em> or <em>right</em> to the end of <em>sorted</em>.

<ol start="2">

 <li><strong> Implementation.</strong></li>

</ol>

For this project, you must implement the sorting algorithm from the previous section in Java. The file <a href="https://html2pdf.com/files/a84fxbm19z6viagt/o_1e0hcphnk23bv2g1n2laap16niv/tests.java"><strong>tests.java</strong></a> is available on Canvas. It contains Java source code for the class Sort, which implements a linear singly-linked list of int’s that can be sorted. You must write a sorting method called sortNodes for Sort. The class Sort has the following members, all of which are static.

private static class Node

A nested class. The linked lists that you must sort are made from instances of Node. Each instance of Node has an int slot called number. It also has a Node slot called next, which points to the next Node in the list, or to null. And it has a constructor that initializes the number and next slots.

private static Node makeNodes(int … numbers)

This method takes a series of int’s as its arguments. It constructs a linear singly-linked list of Nodes that contains those int’s, then returns it. (It also uses Java syntax that was not discussed in the lectures—but you don’t have to know how it works.)

private static Node sortNodes(Nodes unsorted)

<strong>T</strong><strong>HIS IS THE ONLY METHOD THAT YOU MUST WRITE.</strong> It takes a linear singly-linked list of Nodes called unsorted as its argument, sorts the list in nondecreasing order of its number slots, and returns the sorted list.

private static void writeNodes(Node nodes)

This method writes the int’s in nodes, a linear singly-linked list of Node’s, separated by commas and surrounded by square brackets.

public static void main(String[] args)

Test the method sortNodes by making a few linear singly-linked lists of Node’s, sorting them, and writing them.

As stated above, the method sortNodes is all you must write for this project. However, to make the sort algorithm more efficient, and to make the project more interesting, sortNodes must follow all of these <span style="text-decoration: line-through;">scary</span> helpful rules:

You must not use the Java operator new in any way! You are not allowed to make new Node’s, new instances of classes, new arrays, etc. That means sortNodes must work in <em>O</em>(1) space, not counting the memory used for recursion.

Since you can’t make new Node’s, sortNodes must work only by changing the next slots of existing Node’s. You are not allowed to change the number slots of Node’s.

You must use the algorithm described above in the theory section, with its four phases: <em>testing, halving, sorting,</em> and <em>combining. </em>To simplify grading, you must use the same local variable names: <em>left, right, sorted,</em> and <em>unsorted.</em> If you need more local variables, then they can have any names you want.

Your testing phase must not use a loop to count how many Node’s are in <em>unsorted</em>. It must work in <em>O</em>(1) time.

Your halving phase must take <em>O</em>(<em>u</em>) time, where <em>u</em> is the length of <em>unsorted.</em> Adding a Node to <em>left</em> or <em>right</em> must take <em>O</em>(1) time. That means the halving phase can’t traverse <em>unsorted</em> more than once, and can’t traverse <em>left</em> and <em>right</em> at all. It also can’t count how many Node’s are in <em>unsorted</em>. Hint: recall how linked stacks work.

Your sorting phase must call sortNodes recursively to sort <em>left</em> and <em>right.</em>

Your combining phase must take <em>O</em>(<em>l</em> + <em>r</em>) time, where <em>l</em> is the length of <em>left,</em> and <em>r</em> is the length of <em>right.</em> Adding a Node to <em>sorted </em>must take <em>O</em>(1) time. That means the combining phase can’t traverse <em>left</em> and <em>right</em> more than once, and it can’t traverse <em>sorted</em> at all. Hint: recall how linked stacks and linked queues work.

Your method sortNodes must work correctly for lists of any length. It must work for lists other than those in main. In particular, it must work correctly for the empty list, and it must work correctly for lists with duplicate elements.

You may write additional private static helper methods, but they must also follow these rules. Your helper methods can have any names you want.

You can’t change any part of the class Sort, except its sortNodes method. But main is an exception to this rule: you can add more tests to show how your code works. Also, main is the only method that is allowed to print things.

If your code violates these rules, then you will lose a large number of points. As a result, if you have questions about whether you’re following the rules correctly, then you should contact me or the TA’s. Here are more hints:

Draw box-and-arrow diagrams! It helps to use a whiteboard. There are whiteboards available for student use in <a href="https://campusmaps.umn.edu/robert-h-bruininks-hall"><strong>Bruininks Hall </strong></a>and elsewhere on campus. If you can make the algorithm work with box-and-arrow diagrams, then you can make it work with Java code.

My implementation of sortNodes uses about 80 lines of Java code, not using helper functions, not counting comments, and indenting as I do in the lectures. This should give you a very rough idea of how complex sortNodes should be. Your code may be shorter or longer than mine, and still be correct.