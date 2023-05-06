Download Link: https://assignmentchef.com/product/solved-ece421-assignment-4-lifetimes-in-rust
<br>
A linked list is a linear data structure in which each element is a separate object. Every element in the list consists of two items:

<ul>

 <li>The data of this element.</li>

 <li>A reference to the next node.</li>

</ul>

The last node has a reference to an empty node. The entry point into a linked list is called the head of the list. It should be noted that head is not a separate node, but the reference to the first node. If the list is empty, then the head is an empty list.

A linked list is a dynamic data structure. The number of nodes in a list is not fixed and can grow and shrink on demand. Any application  has to deal with an unknown number of objects within a linked list.

<u>Source code:</u> linked_list.rar

<strong>Question 1:</strong> Given the following implementation of a linked list in main.rs in the attached source code:

pub enum LinkedList&lt;T&gt;{

Tail,

Head(T,Box&lt;LinkedList&lt;T&gt;&gt;), }

The code is missing the implementation for 4 functions, empty, new, push, and push_back.

<ul>

 <li>Implement the function <em>empty</em> to return an empty linked list. The function should have the following signature:</li>

</ul>

pub fn empty()-&gt;self{…}

<ul>

 <li>Implement the function <em>new</em> which creates a new linked list with the following signature:</li>

</ul>

pub fn new(t:T)-&gt;self{…}

<ul>

 <li>Implement the function <em>push</em> to insert a new element on the front of the list.</li>

</ul>

For example, if we have a list as follows:

2 → 3 → 5 → 7

.push(1) should result in the following list:

<ul>

 <li>→ 2 → 3 → 5 → 7</li>

</ul>




The function has the following signature:

pub fn push(self, t:T)-&gt;self{

<ul>

 <li>Implement the function push_back to insert a new element at the back of the list. The function has the following signature:</li>

</ul>

pub fn push_back(self, t:T)-&gt;self{

Similarly, if we have a list as follows:

2 → 3 → 5 → 7

push_back(1) should result in the following list:

<ul>

 <li>→ 3 → 5 → 7 → 1</li>

</ul>

<ul>

 <li>Run the tests defined in the main function and make sure that all the tests pass successfully.</li>

</ul>

<strong>Question 2:</strong> Refer to the function cons (<a href="https://docs.rs/im/5.0.0/im/list/fn.cons.html">https://docs.rs/im/5.0.0/im/list/fn.cons.html</a><a href="https://docs.rs/im/5.0.0/im/list/fn.cons.html">)</a> and  a- provide an explanation of the function, the answer should provide a description of what the function does, and a detailed explanation of each parameter of the function.

b- Update your code in question 1 to use the function cons. Please save the updated code in a different project with the name: <em>linked_list_question2.rar</em>

<strong>Question 3:</strong> Rust has a lot of smart pointers, such as <em>Rc&lt;T&gt;</em>, <em>Arc&lt;T&gt;</em>, <em>Cell&lt;T&gt;</em>, and <em>RefCell&lt;T&gt;</em>. Smart pointers wrap the contained values to provide extended functionality beyond that provided by references. Consider the following example:

<table width="639">

 <tbody>

  <tr>

   <td width="639">enum Level {     Low,Medium,High}  struct Task {     id: u8,     level: Level}fn main() {     let task = Task {         id: 10,level: Level::High};task.id=100;println!(“Task with ID: {}”, task.id); }</td>

  </tr>

 </tbody>

</table>

Executing the previous example should result in an error, mention the error and explain how interior mutability can be applied to the problem to solve it. Rewrite the previous code so it runs. (<strong><u>Hint</u></strong>: <em>Consider using Cell&lt;T&gt;</em>)

<h1>Skip List</h1>

A subway system can be expressed as a simple list of stops (expressed as a stop number):

c- stop_1 -&gt; stop_2 -&gt; stop_3 -&gt; stop 4 -&gt; stop 5 -&gt; stop_6

However, some cities in Europe have something called express trains which reduce the number of stops to cover larger distances faster. Suppose someone wants to go from stop_1 to stop_5. Instead of seeing the doors open and close four times, they can switch between the express and the local at the third stop.

<strong>Express:</strong><strong>          </strong>stop_1 ———–&gt; stop_3 ———————&gt; stop_6

<strong>Local: </strong><strong>             </strong>stop_1 -&gt; stop_2 -&gt; stop_3 -&gt; stop 4 -&gt; stop 5 -&gt; stop_6<strong>          </strong>

The local service trains stops at every stop along the way, but the express service trains skips certain smaller stops only to halt at shared stations where travelers can switch between the two trains. The skipping happens quite literally on some stops where trains simply drive through, sometimes confusing tourists and locals alike.

Similarly, a skip list is essentially several lists, each at a different level. The lowest level contains all nodes, where the upper levels are their “<em>express services”</em> that can skip some nodes to get further ahead quicker. This results in a multilayered list, fused together only at certain nodes that have a connection on these particular levels:

next ——-| next ———————————–&gt; next ——-| next ——-&gt; next ———————&gt; next ——-|

next ——-&gt; next ——-&gt; next ——-&gt; next ——-&gt; next——-|

<h2> 1              2            3             4             5</h2>

Ideally, each level has half the number of nodes that the previous level has, which means that there needs to be a decision-making algorithm that can work with growing lists and still maintain this constraint. If this constraint is not kept, search times get worse, and in the worst-case scenario, it’s a regular linked list with a lot of overhead.

<strong>Question 4: </strong>Provide an implementation of <em>skip list</em>, as shown in the following figure, to complete the following code. Remember a skip list is a linked list — this means the only element that can be directed accessed is the head, and you have to travel through elements to find the one you need. (Hint: you may reuse some of your code from questions 1 and 2)




<table width="639">

 <tbody>

  <tr>

   <td width="639">pub struct SkipList&lt;T&gt;{//add your code here} impl&lt;T&gt; SkipList&lt;T&gt;{   fn new() -&gt; self{// creates a new skip list.//add your code here}   fn len(&amp;self) -&gt; usize{// returns the number of elements at level 0 of the skip list.//add your code here}   fn is_empty(&amp;self) -&gt; bool{// checks if the skip list is empty.//add your code here}   fn push(&amp;mut self, value: T){// add an element with value T (strat from the beginning of the skiplist).//add your code here}   fn push_back(&amp;mut self, value: T){// add an element with value T (start from the end of the skiplist).//add your code here}}</td>

  </tr>

 </tbody>

</table>


