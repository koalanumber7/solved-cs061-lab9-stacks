Download Link: https://assignmentchef.com/product/solved-cs061-lab9-stacks
<br>
The purpose of this lab is to investigate the innermost intricacies of the stack data structure by implementing one and then using it in a “simple” application.

<ul>

 <li><strong>Our Objectives for This Week </strong></li>

</ul>

<ol>

 <li>Understand what a stack is</li>

 <li>Understand how to PUSH onto and POP from a stack</li>

 <li>Exercise 1 ~ Implement PUSH</li>

 <li>Exercise 2 ~ Implement POP</li>

 <li>Exercise 3 ~ Use Ex1 and Ex2 to build a Reverse Polish Notation Calculator<strong>  </strong></li>

</ol>

<ol start="3">

 <li><strong> 1 What is this “stack” you speak of?!</strong></li>

</ol>

<strong>High Level: </strong>

A stack is a data structure that stores items in a LIFO order – “​<strong>L</strong>​ast ​<strong>I</strong>​n ​<strong>F</strong>​irst ​<strong>O</strong>​ut”.

In other words, the last item you put onto your stack is the first item you can take out. Unlike an array, you cannot take items out of a stack in any order you like, nor can you put items into a stack in any order you like.

<strong>LIFO Analogy: </strong>

Imagine that you had a Pez dispenser. Each candy is inserted into the Pez dispenser and falls to the bottom. Whenever you want to extract a piece of candy from the dispenser, you can only take the one on top (that last one that you put in). You cannot get the first piece of candy back without taking the second piece of candy out of the dispenser first. Thus, the <strong>last</strong>​       piece of candy that you put ​  <strong>in</strong>​ to the​ dispenser must be the ​<strong>first</strong>​ piece of candy you take ​<strong>out</strong>​.

<strong>Visual Stack Example: </strong>

Below is a numerical example. Let’s say you are given the numbers {17, 314, 8, 42}. You can PUSH these onto a stack in the manner depicted below.

Now that your stack has a bunch of items in it, you can take them out by calling POP on the stack—remember, they have to come out in LIFO order. Note that the order of items popped is always the <u>reverse​</u><em> of the PUSH order</em>​. Popping is visually depicted below.

Notice how the PUSH order was {17, 314, 8, 42} but the POP order was {42, 8, 314, 17}.

<strong>Important Stack Lexicon: </strong>

Definition: ​<strong>Overflow </strong>

To overflow a stack is to try to PUSH an element onto it when it is full.

Definition: ​<strong>Underflow </strong>

To underflow a stack is to try to POP an element off of it when it is empty.

<strong>How to implement a stack in LC3: </strong>

The easiest way to implement a stack that checks for overflow and underflow is as follows:

<strong>Specs for a stack located from xA001 to xA005</strong>​<em> (i.e. a total of 5 “slots”) </em>

<ul>

 <li>A stack structure consists of three members:

  <ol>

   <li>BASE: A pointer to the bottom of the stack (we’ll use R4) – actually, to ​<em>1 slot below the lowest available address</em>​, in this case ​<strong>BASE = xA000 </strong></li>

   <li>MAX: The “highest” available address in the stack (R5), in this case <strong>xA005</strong>​</li>

   <li>TOS: A pointer to the <em><u>current</u></em><u>​ </u>​ ​<strong>T</strong>​op ​<strong>O</strong>​f the ​<strong>S</strong>​tack (R6);  in this case, for the empty stack, ​<strong>TOS starts at BASE = xA000</strong></li>

  </ol></li>

</ul>

<ul>

 <li>To ​<strong>PUSH</strong>​ a value onto a stack ​<em>(we will use the value currently in R0)</em>​:

  <ul>

   <li>Verify that TOS is <u>less than</u>​ MAX (if not, print Overflow message &amp; quit)​              – Increment TOS</li>

   <li>Write the desired value to the Top Of Stack: <strong>Mem[TOS] &lt;- (R0)</strong></li>

  </ul></li>

</ul>

<ul>

 <li>To ​<strong>POP</strong>​ a value off a stack ​<em>(we will “capture” the value into R0)</em>​:

  <ul>

   <li>Verify that TOS is ​<u>greater than​</u> BASE (if not, print Underflow message &amp; quit)</li>

   <li>Copy the value at the Top Of Stack to the destination register: <strong>R0 &lt;- Mem[TOS]</strong> – Decrement TOS</li>

  </ul></li>

</ul>

Note that when pushing, we <em><u>first increment</u></em><u>​ </u>​, then write;  when popping, we <u>​<em>first read</em></u>​, then decrement.

<strong>Setup/Initialization of a 5-slot stack: </strong>

<ul>

 <li>Set R4 = BASE to xA000</li>

 <li>Set R5 = MAX to xA005</li>

 <li>Set R6 = TOS to BASE = xA000 ​<em>(i.e. stack starts out empty) </em></li>

</ul>

Note that you don’t have to actually “remove” anything when you POP; all you have to do is decrement TOS after reading. Any PUSH you do later will simply overwrite whatever was there previously.<strong>          </strong>

<h1>Exercise 01: Stack PUSH</h1>

<ol>

 <li>Write the following subroutine:</li>

</ol>

;——————————————————————————————

; Subroutine: SUB_STACK_PUSH

; Parameter (R0): The value to push onto the stack

; Parameter (R4): BASE: A pointer to the base (​<strong><u>one less than</u></strong>​ the lowest available

;                       address) of the stack

; Parameter (R5): MAX: The “highest” available address in the stack

; Parameter (R6): TOS (Top of Stack): A pointer to the <u>​</u><em><u>current</u></em><u>​</u> top of the stack

; Postcondition: The subroutine has pushed (R0) onto the stack (i.e to address TOS+1).  ;     If the stack was already full (TOS = MAX), the subroutine has printed an ;     overflow error message and terminated.

; Return Value: R6 ← updated TOS

;——————————————————————————————

<u>Test Harness:</u>

To ensure that your subroutine works, write a short test harness. Make sure your stack stores the values as expected in memory and prints an overflow error message as necessary.

<h1>Exercise 02: Stack POP</h1>

Write the following subroutine:

;——————————————————————————————

; Subroutine: SUB_STACK_POP

; Parameter (R4): BASE: A pointer to the base (​<strong><u>one less than</u></strong>​ the lowest available

;                       address) of the stack

; Parameter (R5): MAX: The “highest” available address in the stack

; Parameter (R6): TOS (Top of Stack): A pointer to the <u>​</u><em><u>current</u></em><u>​</u> top of the stack ; Postcondition: The subroutine has popped MEM[TOS] off of the stack.

;          If the stack was already empty (TOS = BASE), the subroutine has printed ;                an underflow error message and terminated.

; Return Value: R0 ← value popped off the stack

;                R6 ← updated TOS

;——————————————————————————————

<u>Test Harness:</u>

Add a call to the POP s/r to your test harness from exercise 1. Make sure your tos value updates as expected, and that overflow/underflow error messages print appropriately.

<strong>           </strong>Exercise 03: Reverse Polish Calculator

Reverse Polish Notation (RPN) is an alternative to the way we usually write arithmetic expressions. When we want to add two numbers together, we usually write, “12 + 7” and get 19 as a result. In RPN, to express the same thing, we write, “12 7 +” and get 19 – i.e. we first specify the two operands, then the operation to be performed on them. In this exercise, you will implement a Reverse Polish Notation Calculator that performs a single operation, multiplication.

<u>Subroutine (write me!)</u>

;——————————————————————————————

; Subroutine: SUB_RPN_MULTIPLY

; Parameter (R4): BASE: A pointer to the base (​<strong><u>one less than</u></strong>​ the lowest available

;                       address) of the stack

; Parameter (R5): MAX: The “highest” available address in the stack

; Parameter (R6): TOS (Top of Stack): A pointer to the <u>​</u><em><u>current</u></em><u>​</u> top of the stack

; Postcondition: The subroutine has popped off the top <u>​</u><em><u>two</u></em>​ values of the stack,

;                 multiplied them together, and pushed the resulting value back

;                 onto the stack.

; Return Value: R6 ← updated TOS address

;—————————————————————————————— Your main program must do the following:

<ol>

 <li>Prompt user for a single digit numeric character, and convert it to a number in R0 <em>(</em>​ <em>if you wish, you can invoke a helper s/r to do this)</em>​; then invoke PUSH s/r to push R0 onto stack.</li>

 <li>Repeat, to get second operand &amp; push it onto stack.</li>

 <li>Prompt for the operation symbol (in this case, a “*”). You can simply discard it once received, since multiplication is the only operation we are implementing.</li>

 <li>Call the SUB_RPN_MULTIPLY subroutine to pop the top two values off the stack, multiply them, and push the result back onto the stack.

  <ul>

   <li>if you wish, you may use a helper s/r to do the actual multiplication – it only needs to handle the multiplication of two single digit numbers.</li>

  </ul></li>

 <li>POP the result off the stack and print it out to the console in decimal format.

  <ul>

   <li>use a helper s/r to do the output: pass in the number in R0, and print it as numeric characters; it only has to be able to print 1 or 2 digit numbers. <em>(</em>​ <em>You can use your lab 7 subroutine to do this).</em></li>

  </ul></li>

</ol>

<strong>Hints: </strong>

<ul>

 <li>You will need the following subroutines to get the job done:</li>

</ul>

○ SUB_STACK_PUSH                   (exercise 01)

○ SUB_STACK_POP                      (exercise 02)

○ SUB_RPN_MULTIPLY

○ SUB_MULTIPLY                         (optional)

○ SUB_GET_NUM                        (optional)

○ SUB_PRINT_DECIMAL              (use the subroutine from lab 7)

<ul>

 <li>You do not need to implement any input validation.</li>

 <li>As in assignment 5, you will have nested subroutine invocations – make sure you get the register backup &amp; restore exactly right!!</li>

</ul>