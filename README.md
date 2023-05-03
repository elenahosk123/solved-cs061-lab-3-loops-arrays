Download Link: https://assignmentchef.com/product/solved-cs061-lab-3-loops-arrays
<br>
<h1>1      High Level Description</h1>




Today’s lab will introduce arrays: constructing and traversing them with both counter-controlled loops and (new) sentinel-controlled loops.







<h1>2      Our Destination This Week</h1>




<ol>

 <li>Lab 2 review</li>

 <li>Pseudo-ops revisited</li>

 <li>More indirection! Exercise 1</li>

 <li>Hurray for Arrays! ​ Exercises 2 – 3​</li>

 <li>More loopiness! Exercise 4  So do I know everything yet??</li>

</ol>










<strong>3    Processing data </strong>




<h1>Lab 2 review</h1>

If there is anything you don’t yet understand about the differences between <strong>LEA</strong>​  , ​ <strong>LD/ST</strong>​           , ​ <strong>LDI/STI</strong>​ , and​    <strong>LDR/STR</strong>​ – <u>​ask now</u>​!




<strong><em>Remember to always open the Text Window of your simpl LC-3 emulator!</em></strong>




<strong><u>Exercise 0</u> </strong>

<em> </em>

Write a program that takes a single character from the keyboard,  using Trap x20 (aka GETC).




<strong><em>Whenever you GETC, you must always immediately OUT, to echo the captured</em></strong>​ ​<strong><em>character  </em></strong>

<em>– otherwise the user has no feedback to confirm what key they just typed (we call that “ghost typing”).</em> The ​<em><u>only</u></em>​ exception to this might be when capturing a password, when you don’t want to echo the characters for security reasons ​<em>(another approach is to echo every character with ‘*’)</em>​.




Using the simpl emulator, “step” through the program and examine the contents of R0 immediately following the GETC routine: you will see that LC3 stores each character as an 8-bit ascii code in the lower byte of a 16-bit word, setting the upper byte to 0 ​<em>(check an ascii table to confirm the code for the character you typed)</em>​.







<h2><strong>3.1     Pseudo-ops revisited </strong></h2>

All assembly languages have several “pseudo-ops”, assembler “directives” that instruct the assembler

program how to set up the object code – just like C++ compiler directives like ​#include A quick review: read ​<a href="https://docs.google.com/document/d/10Q1lFYmInYbrSKHdttUs4VRJAesdCmKGIpuk3nTxpG4/edit?usp=sharing">LC-3 Pseudo-ops summary</a><u>​</u> in the LC-3 Resources folder.




You encountered most of the LC3 pseudo ops already in lab 1:

.ORIG ​tells the assembler where to start loading the code ​<em>(usually x3000, except when we tell you otherwise)</em>​;

.END ​tells the assembler that there is no more code to assemble (like the ​’}’​ after main() in C++) .FILL​ stashes a single “hard-coded” value into a memory location; you can specify it as a decimal (#​ ​), hex (​x​), or ascii character (use ​’ ‘​, e.g. ​’a’​ or ​’
’​) and​ .STRINGZ​ creates a c-string, i.e. a null-terminated character array. You may use 
 inside a string to insert a newline at any point.




The last of the pseudo-ops we’ll need is ​.BLKW​ ​<em>(“block words”)</em>​: it tells the assembler to set aside ​<strong>n</strong> memory locations for later use. Note that it does not explicitly “zero out” the designated memory space, so there may be “junk values” in those locations if they have been used previously. We’ll be using this pseudo-op in today’s exercises.







<u>Example</u>​:

ARRAY_1 .BLKW  #10 ; Reserves 10 memory locations, starting at address ARRAY_1 DEC_25    .FILL #25  ; stores the vale #25 at the memory address labelled DEC_25

; this will be located at the first address following ARRAY_1




<em>Figure 1: .BLKW Illustration </em>

<em>Note that even though the label DEC_25 immediately follows label ARRAY_1 in the code, its address is </em>

<h1>(address of ARRAY_1) + #10</h1>

<em>Note also that the ten memory locations are </em><u>​<em>not</em></u>​<em> guaranteed by the LC3 specs to be initialized to 0.</em>







<strong>3.2    More indirection!  </strong>




<h2>Exercise 1</h2>

Let’s take another look at Exercise 3 from last week.

<em> </em>

At the time, we told you to hard code both remote addresses in the local data block – but this is not really very efficient ​<em>(suppose you had a dozen data values up there </em>…<em>) </em>




We know that the two data values are in contiguous memory locations (x4000 and x4001), so we ought to be able to just hard-code the first address and then use ​<em>address arithmetic</em>​ to get to the next.




So copy your <u>​Lab 2 Exercise 3​</u> from last week into the lab3_ex1.asm file in your current directory, but this time use just a ​<em><u>single</u></em>​ pointer in the local data block, with the address of the start of the remote data block. Call it DATA_PTR.

You already know how to get the first data item from the remote location: how will you get the next? <em>Hint: LDI won’t work, because we don’t have a pointer to it in an accessible memory location. </em>




When you have figured this out, run the code (read the two remote data values, modify them, &amp; store the modified data back to the remote location).

As in lab 2, manually inspect the memory in simpl to confirm.




<strong>             </strong>

<strong>3.3    Hurray for Arrays!  </strong>

<strong> </strong>

<h2>Exercise 2</h2>

The technique you just discovered ​<em>(if you didn’t, go back to exercise 1, and don’t join us here until you’ve figured it out!)</em>​ is a standard mechanism for constructing and traversing <u>​<em>arrays</em></u>​ – not just in LC3 programming, but in <u>​<em>all</em></u>​ languages.




So now write a program (lab3_ex2.asm) that builds and populates an array in the local data area:

<ul>

 <li>Use .BLKW to set up a blank array of 10 locations in the local data area.</li>

 <li>Then have the program prompt the user to enter exactly 10 characters from the keyboard, and populate that array with the characters as they are input</li>

</ul>




This will require a counter-controlled loop (DO-WHILE loop), which you should already know how to construct. ​<em>(Check </em><a href="https://drive.google.com/drive/folders/0B9AugYlANDZkVUtZajFkNUFBX0U?usp=sharing">​</a><a href="https://drive.google.com/drive/folders/0B9AugYlANDZkVUtZajFkNUFBX0U?usp=sharing"><em>here</em></a><a href="https://drive.google.com/drive/folders/0B9AugYlANDZkVUtZajFkNUFBX0U?usp=sharing">​</a> <em>if you need a refresher!) </em>

Test your program, inspecting the contents of the array in simpl after every character input. <em>(By the way: you should now understand one of the deep mysteries of C++ – why the number of elements in a static array variable </em><u>​<strong><em>must</em></strong></u>​<em> be known at compile time, and can’t be changed after that). </em>




<h2>Exercise 3</h2>

First, go read the ​<a href="https://docs.google.com/document/d/14vaOKv7-IpuY8VWcoQnq8opl5CpcLHay7sTZG4BzoY4/edit?usp=sharing">basic i/o doc</a>

Now copy exercise 2 into lab3_ex3.asm, and extend it by adding  another loop to traverse the array again, and output each stored character to the console, <u>one per line​        </u> (i.e. print a newline ‘
’ = ASCII​         x0A – <u>​after each character</u>).<u>​</u>

Your program will now be complete: it will accept exactly 10 characters from input, storing them one by one in a remote array, and then output the whole list to console.

<strong> </strong>

<strong>3.4    More loopiness!  </strong>

<strong> </strong>

<h2>Exercise 4</h2>

In the previous exercises, you were able to traverse the arrays because you knew up front how many elements were in them – in fact that number was hard-coded into the .BLKW pseudo-op.




Can you think of a way to create and/or traverse an array without knowing beforehand how many elements it will contain, and without using .BLKW?

<u>Hint</u>​: think about the difference between counter &amp; sentinel control of loops.

<u>Another hint</u>:<u>​</u> we will actually need <em>two separate sentinels!</em>​ ​ (see below for detail)

<em><u>First</u></em>​, you have to use a specific key to tell the program to stop collecting characters from the keyboard; ​<em><u>then</u></em>​ you have to store a sentinel ​<u>in the array​</u> to mark the end of the collected characters.




Now copy Exercise 3 into your lab3_ex4.asm file, and modify it as follows:

<ul>

 <li>It must capture a sequence of characters as long as you like ​<em>(within reason – for now, let’s keep our tests to less than 100)</em>​, and stop when you enter your “input” sentinel character.</li>

 <li>The program will store each character as it is entered in an array starting at x4000 ​<em>(we will just assume for now that there is a vast amount of free memory up there)</em>​, with a sentinel character marking the end of the data; and then output them to the console in a separate loop.</li>

 <li>Remove the newline after each character output – i.e. the entire array will now be output on a single line. DO terminate that line with a newline.</li>

</ul>




There are three separate problems to be solved here:




<ul>

 <li>How do I communicate to the program that I have finished input?</li>

</ul>

<em>Hint: what is the most common keyboard method of signaling “I’m done with this message” in, say, Facebook chat? </em>

<ul>

 <li>How do I build the array so that it “knows” where it stops – i.e. what sentinel do I store at the end of the array? This can be different from your “input” sentinel. <em>Hint: how does .STRINGZ do it? </em></li>

 <li>How does the program know when to stop traversing the array for output? <em>See previous hint, and think PUTS! </em></li>

</ul>




Once you solve these problems you will have in your algorithmic toolkit a very powerful technique – <em><u>sentinel-controlled loops</u></em>​—that you will be using to manage i/o for the rest of the course.







<h3>3.5     Submission</h3>

Demo your lab exercises to your TA <strong><em>before you leave lab</em></strong>​ ​.




If you are unable to complete all exercises in lab,  show your TA how far you got, and request permission to complete it after lab.

Your TA will usually give you partial credit for what you have done, and allow you to complete &amp; demo the rest later for full credit, so long as you have worked at it seriously for the full 3 hours.

When you’re done, demo it to any of the TAs or instructors in office hours <strong><em><u>before</u></em></strong>​  ​<strong><em> your next lab</em></strong>​.  <em>Office hours are posted on Piazza, under the “Staff” tab.</em>







<strong>4        So what do I know now? </strong>

You should now know:

<ul>

 <li>How the .BLKW pseudo-op works to reserve memory locations</li>

 <li>How to use .BLKW to build arrays, and use counter-controlled loops to traverse them How to test for a specific value, and use such tests in sentinel-controlled loops.</li>

 <li>How to build arrays without .BLKW, and use sentinel-controlled loops to traverse them.</li>

 <li>How to use prompts to communicate with the user.</li>

 <li>How to do basic i/o</li>

 <li>Did I mention that sentinel-controlled loops are very, very important?</li>

</ul>





