Download Link: https://assignmentchef.com/product/solved-cop3502-assignment-1-varg
<br>
In COP 3223 (Introduction to C Programming), you encountered many functions – such as <em>printf()</em> – that were capable of taking a different number of arguments every time you call them. However, the functions you wrote in that class probably never had that ability; instead, they were always restricted to taking the same number of arguments each time they were called.

In this programming assignment, you will write two <a href="https://en.wikipedia.org/wiki/Variadic_function">variadic functions</a> – that is, functions that take a variable number of arguments. By completing this assignment, you will acquire a new, advanced C programming skill. Because of one of the restrictions placed on the functions, you will also gain a small amount of experience developing an algorithm with a focus on runtime efficiency.

On the software engineering side of things, you will learn to construct programs that use multiple source files and custom header (.h) files. This assignment will also help you hone your ability to acquire new knowledge by reading technical specifications. If you end up pursing a career as a software developer, the ability to rapidly digest technical documentation and work with new software libraries will be absolutely critical to your work, and this assignment will provide you with a gentle exercise in doing just that.

Finally, this assignment is specifically designed to require relatively few lines of code so that you can make your first foray into the world of Linux without a huge, unwieldy, and intimidating program to debug. As the semester progresses, the programming assignments will become more lengthy and complex, but for now, this assignment should provide you with a gentle introduction to debugging in a foreign development environment.

<strong>Attachments</strong>

<em>Varg.h</em>, <em>varsum.c</em>, <em>testcase{01-06}.c</em>, <em>output{01-06}.txt</em>, and <em>test-all.sh</em>

<strong>Deliverables</strong>

<em>Varg.c</em>

(<strong><em>Note!</em></strong> Capitalization and spelling of your filename matters!)

<h1><a name="_Toc11916"></a>1. Overview</h1>

In this assignment, you’ll write two variadic functions – functions that take variable numbers of arguments, just like printf() is capable of doing. (There are also two other functions for you to write. A complete list of required functions, including their functional prototypes, is given below in Section 8, “Function Requirements”.)

You will submit a single source file, named Varg.c, that contains all required function definitions, as well as any auxiliary functions you deem necessary. In Varg.c, you will have to #include any header files necessary for your functions to work, including the custom Varg.h file we have distributed with this assignment (see Section 5, “Varg.h”).

<strong>Note: You will <em>not</em> write a main() function in the source file you submit!</strong> Rather, we will compile your source file with our own main() function(s) in order to test your code. We have attached example source files that have main() functions, which you can use to test your code. You can write your own main() functions for testing purposes, but the code you submit must not have a main() function. We realize this is completely new territory for most of you, so don’t panic. We’ve included instructions for compiling multiple source files into a single executable (e.g., mixing your Varg.c with our Varg.h and testcaseXX.c files) in Sections 11 and 12 of this PDF.

Although we have included test cases with sample main() functions to get you started with testing the functionality of your code, we encourage you to develop your own test cases, as well. Ours are by no means comprehensive. We will use much more elaborate test cases when grading your submission.

<em>Start early. Work hard. Good luck!</em>

<h1><a name="_Toc11917"></a>2. Important Note: Test Case Files Look Wonky in Notepad</h1>

Included with this assignment are several test cases, along with output files showing exactly what your output should look like when you run those test cases. You will have to refer to those as the gold standard for how your output should be formatted. Please note that if you open those files in Notepad, they will appear to be one long line of text. That’s because Notepad handles end-of-line characters differently from Linux and Unix-based systems. One solution is to view those files in an IDE (like CodeBlocks), or you could use a different text editor (like <a href="https://atom.io/">Atom</a> or <a href="https://www.sublimetext.com/3">Sublime</a><a href="https://www.sublimetext.com/3">)</a>.

<h1><a name="_Toc11918"></a>3. Adopting a Growth Mindset</h1>

A word of advice before we dive in to the details: When faced with an assignment like this, which has many different facets, some of which might appear foreign and/or challenging, it’s important not to look at it as an instrument that is being used to measure how much you already know (whether that’s knowledge of programming, operating systems, or even what some might call “natural intellectual capability”). Rather, it’s important to view this assignment as a chance to learn something new, grow your skill set, and embrace a new challenge.

It’s also important to view intellectual capability as something that can grow and change over one’s lifetime. Adopting that mindset will allow you to reap greater benefits from this assignment (and from all your college-level coursework) regardless of the grades you earn.

For more on the importance of adopting a growth mindset throughout your academic career and how that can impact your life, see the following:

<a href="https://ed.ted.com/featured/qrZmOV7R">Growth Mindset vs Fixed Mindset: An Introduction</a> (Watch time: 2 min 42 sec)

<a href="https://www.youtube.com/watch?v=pN34FNbOKXc">The Power of Belief – Mindset and Success</a> (Watch time: 10 min 20 sec)

<h1><a name="_Toc11919"></a>4. Writing Variadic Functions</h1>

One of the trickiest things about writing a variadic function is that you must somehow tell the function how many arguments you’re passing to it. When you call printf(), you do this implicitly, because printf() goes through your first argument (a string), and every time it sees a conversion code (such as “%d” or “%c”), it knows there is another input argument waiting to be processed. By reading the format string, the function figures out how many arguments to read after the initial one.

Included with this assignment is a file called varsum.c, which I wrote to show you how to implement a simple function to add up an arbitrary number of integer arguments passed to a function. The file has two versions of that function: mySum() and myOtherSum(). The only difference between the two implementations is how each function figures out how many integers it will be processing.

From that source file, you’ll see that when writing a variadic function, all the magic happens with the va_list data type and the va_start and va_arg functions. In order to use va_list, va_start, and va_arg, you must include stdarg.h at the top of your source code, like so:

#include &lt;stdarg.h&gt;

Note that stdarg.h is a standard system library, just like stdio.h and string.h.

<h1><a name="_Toc11920"></a>5. Varg.h</h1>

Included with this assignment is a customer header file that includes functional prototypes for all the functions you will be implementing. You should #include this file from your Varg.c file, like so:




#include “Varg.h”

The “quotes” (as opposed to &lt;brackets&gt;) indicate to the compiler that this header file is found in the same directory as your source, not a system directory.

You should not modify Varg.h in any way, and you should not send Varg.h when you submit your assignment. We will use our own unmodified copy of Varg.h when compiling your program.

If you write auxiliary functions (“helper functions”) in your Varg.c file (which is strongly encouraged!), you should <strong><em>not</em></strong> add those functional prototypes to Varg.h. Our test case programs will not call your helper functions directly, so they do not need any awareness of the fact that your helper functions even exist. (We only list functional prototypes in a header file if we want multiple source files to be able to call those functions.) So, just put the functional prototypes for any helper functions you write at the top of your Varg.c file.

<strong>Think of </strong>Varg.h<strong> as a bridge between source files. </strong>It contains functional prototypes for functions that might be defined in one source file (such as your Varg.c file) and called from a different source file (such as the testcaseXX.c files we have provided with this assignment).

<h1><a name="_Toc11921"></a>6. Test Cases and the test-all.sh Script</h1>

We’ve included multiple test cases with this assignment, which show some ways in which we might test your code. These test cases are not comprehensive. You should also create your own test cases if you want to test your code comprehensively. In creating your own test cases, you should always ask yourself, “How could these functions be called in ways that don’t violate the program specification, but which haven’t already been covered in the test cases included with the assignment?”

We’ve also included a script, test-all.sh, that will compile and run all test cases for you. You can run it on Eustis by placing it in a directory with Varg.c, Varg.h, and all the test case files, and typing:

bash test-all.sh

<h1><a name="_Toc11922"></a>7. Output</h1>

The functions you write for this assignment should not produce any output. If your functions cause anything to print to the screen, it will interfere with our test case evaluation.

Please be sure to disable or remove any printf() statements you have in your code before submitting this assignment.

<h1><a name="_Toc11923"></a>8. Function Requirements</h1>

In the source file you submit, Varg.c, you must implement the following functions. You may implement auxiliary functions (helper functions) to make these work, as well, although that is probably unnecessary for this assignment. Please be sure the spelling, capitalization, and return types of your functions match these prototypes exactly.

char mostFrequentChar(int n, …);

<strong>Description:</strong> This function takes a single non-negative integer, <em>n</em>, followed by a list of exactly <em>n </em>lowercase, alphabetic characters (any characters on the range ‘a’ through ‘z’), and returns the most frequently occurring character it received as input. If multiple characters are tied for the distinction of “most frequently occurring,” you should return the first one that occurred that number of times when processing the argument list from left to right. For example, when processing the input to the function call mostFrequentChar(5, ‘a’, ‘b’, ‘b’, ‘a’, ‘c’), both ‘a’ and ‘b’ are tied (with two occurrences each), but the first character to rack up two occurrences when reading the list in order (from left to right) is ‘b’. (For further examples, see the test cases included with this assignment.)

<strong>Special Restriction:</strong> As you read the list of input arguments, you are not allowed to store that list anywhere in memory (for example, in a linked list or a string). In other words, you can read the list of arguments passed to your function exactly once. You should not try to save that list in memory so that you can re-read it multiple times within your function.

<strong>Output:</strong> This function should not print anything to the screen.

<strong>Return Value: </strong>The most frequently occurring character in the argument list. (See the description above for an explanation of how to handle ties.) If <em>n</em> is equal to zero, your function should return the ‘ ’ character, which is C’s null sentinel.




char fancyMostFrequentChar(char c, …);

<strong>Description:</strong> This function takes as its input a list of characters. The function is guaranteed to receive at least one argument. The last argument passed to the function will always be the ‘ ’ character, which is C’s null sentinel. All other characters in the list will be lowercase, alphabetic characters (any characters on the range ‘a’ through ‘z’). Your function should return the most frequently occurring character in the list. In the event of ties, you should handle them in the same way that the mostFrequentChar() function handles ties (described above). Note that it’s possible for ‘ ’ to be the only argument given, in which case you should return ‘ ’.

<strong>Special Restriction:</strong> This function is subject to the same special restriction listed above for the mostFrequentChar() function.

<strong>Output:</strong> This function should not print anything to the screen.

<strong>Return Value:</strong> The most frequently occurring character in the argument list. (See the description above for an explanation of how to handle ties.) If ‘ ’ is the only argument passed to this function, then you should return ‘ ’.

double difficultyRating(void);

<strong>Output:</strong> This function should not print anything to the screen.

<strong>Return Value:</strong> A double indicating how difficult you found this assignment on a scale of 1.0 (ridiculously easy) through 5.0 (insanely difficult).

double hoursSpent(void);

<strong>Output:</strong> This function should not print anything to the screen.

<strong>Return Value:</strong> An estimate (greater than zero) of the number of hours you spent on this assignment.

<h1><a name="_Toc11924"></a>9. Input Specifications Are a Contract</h1>

In testing, you can rest assured that we will only call your functions in ways that jive with the function descriptions above. For example, we will never call mostFrequentChar() without specifying an integer as the first argument, and that integer is always guaranteed to correctly indicate the number of arguments that follow. Similarly, we will never call fancyMostFrequentChar() without ending the list of parameters with a null sentinel (‘ ’), and neither function will receive unexpected characters in the argument list (such as a capital ‘Q’ or punctuation marks such as ‘!’).

<h1><a name="_Toc11925"></a>10. ASCII Character Values</h1>

<em>Note: If you haven’t thought about how to solve this problem yet, it might not be immediately obvious why the information in this section might be useful to you in this assignment.</em>

In C, each character has an underlying integer value called its ASCII value. (ASCII is an international standard for character numbering. If you want to read more about the topic, see the <a href="https://en.wikipedia.org/wiki/ASCII">ASCII article on </a><a href="https://en.wikipedia.org/wiki/ASCII">Wikipedia</a><a href="https://en.wikipedia.org/wiki/ASCII">.</a> For this assignment, however, you don’t need to know any more about ASCII than what I’ve written up in this section.)

To see a character’s underlying integer value, you can always just print it as an integer, like so:

printf(“%d”, ‘a’);

The ASCII value for ‘a’ is 97, so the above line of code should print out 97.

Lowercase letters are numbered sequentially: ‘a’ is 97, ‘b’ is 98, ‘c’ is 99, and so on. If for some reason you wanted to convert the characters ‘a’ through ‘z’ to integers 0 through 25 (maybe so you could use them to access indices in an array of length 26?), you could just subtract 97 from those characters. For example:

printf(“%d”, ‘a’ – 97);  // ‘a’ – 97 = 97 – 97 = 0 printf(“%d”, ‘b’ – 97);  // ‘b’ – 97 = 98 – 97 = 1 printf(“%d”, ‘c’ – 97);  // ‘c’ – 97 = 99 – 97 = 2

Personally, I never hard-code the value 97 when converting characters to integers (partly because I never used to be able to remember it off the top of my head). Instead, I just use ‘a’ in place of 97, because the math will always work out:

printf(“%d”, ‘a’ – ‘a’);  // ‘a’ – ‘a’ = 97 – 97 = 0 printf(“%d”, ‘b’ – ‘a’);  // ‘b’ – ‘a’ = 98 – 97 = 1 printf(“%d”, ‘c’ – ‘a’);  // ‘c’ – ‘a’ = 99 – 97 = 2

<em>Continued on the following page…</em>




<h2> Compilation and Testing (CodeBlocks)</h2>

The key to getting multiple files to compile into a single program in CodeBlocks (or any IDE) is to create a project. Here are the step-by-step instructions for creating a project in CodeBlocks, which involves importing Varg.h, testcase01.c, and the Varg.c file you’ve created (even if it’s just an empty file so far).

<ol>

 <li>Start CodeBlocks.</li>

 <li>Create a New Project (<em>File -&gt; New -&gt; Project</em>).</li>

 <li>Choose “Empty Project” and click “Go.”</li>

 <li>In the Project Wizard that opens, click “Next.”</li>

 <li>Input a title for your project (e.g., “Varg”).</li>

 <li>Choose a folder (e.g., Desktop) where CodeBlocks can create a subdirectory for the project.</li>

 <li>Click “Finish.”</li>

</ol>

Now you need to import your files. You have two options:

<ol>

 <li>Drag your source and header files into CodeBlocks. Then right click the tab for <strong><u>each</u></strong> file and choose “Add file to active project.”</li>

</ol>

<em>– or –</em>

<ol start="2">

 <li>Go to <em>Project -&gt; Add Files…</em>. Browse to the directory with the source and header files you want to import. Select the files from the list (using CTRL-click to select multiple files). Click “Open.” In the dialog box that pops up, click “OK.”</li>

</ol>

You should now be good to go. Try to build and run the project (F9).

Note that if you import both testcase01.c <em>and</em> testcase02.c, the compiler will complain that you have multiple definitions for main(). You can only have one of those in there at a time. You’ll have to swap them out as you test your code.

Yes, constantly swapping out the test cases in your project will be a bit annoying. You can avoid this if you’re willing to migrate away from an IDE and start compiling at the command line instead. If you’re interested in doing that in Windows, please look around online for instructions on how to make that happen, and see a TA in office hours if you get stuck. Alternatively, you might consider installing Linux on a separate partition of your hard drive. If you take that approach, just be sure to back up your hard drive first.

<strong><em>Note!</em></strong> Even if you develop your code with CodeBlocks on Windows, you ultimately have to transfer it to the Eustis server to compile and test it there. See the following page (Section 12, “ Compilation and Testing (Linux/Mac Command Line)”) for instructions on command line compilation in Linux.

<h2> Compilation and Testing (Linux/Mac Command Line)</h2>

To compile multiple source files (.c files) at the command line:

gcc Varg.c testcase01.c

By default, this will produce an executable file called a.out, which you can run by typing:

./a.out

If you want to name the executable file something else, use:

gcc Varg.c testcase01.c -o Varg.exe

…and then run the program using:

./Varg.exe

Running the program could potentially dump a lot of output to the screen. If you want to redirect your output to a text file in Linux, it’s easy. Just run the program using the following command, which will create a file called whatever.txt that contains the output from your program:

./Varg.exe &gt; whatever.txt

Linux has a helpful command called diff for comparing the contents of two files, which is really helpful here since we’ve provided several sample output files. You can see whether your output matches ours exactly by typing, e.g.:

diff whatever.txt output01.txt

If the contents of whatever.txt and output01.txt are exactly the same, diff won’t have any output. It will just look like this:

<strong><a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="88fbede9e6fbf2c8edfdfbfce1fb">[email protected]</a>:~$</strong> diff whatever.txt output01.txt <strong><a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="0b786e6a6578714b6e7e787f6278">[email protected]</a>:~$</strong> _

If the files differ, it will spit out some information about the lines that aren’t the same. For example:

<strong><a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="1764727679646d57726264637e64">[email protected]</a>:~$</strong> diff whatever.txt output01.txt

1c1

&lt; fail whale &#x1f641;

—

&gt; Hooray!

<strong><a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="d5a6b0b4bba6af95b0a0a6a1bca6">[email protected]</a>:~$</strong> _

<h2> Getting Started: A Guide for the Overwhelmed</h2>

Okay, so, this might all be overwhelming, and you might be thinking, “Where do I even start with this assignment?! I’m in way over my head!”

Don’t panic! There are plenty of TA office hours where you can get help, and here’s my general advice on starting the assignment:

<ol>

 <li>First and foremost, start working on this assignment early. Nothing will be more frustrating than running into unexpected errors or not being able to figure out what the assignment is asking you to do on the day that it is due.</li>

 <li>Secondly, glance through this entire PDF to get a general overview of what the assignment is asking you to do, even if you don’t fully understand each section right away.</li>

 <li>Thirdly, before you even start programming, open up the test cases and sample output files included with this assignment and trace through a few of them to be sure you have an accurate understanding of what the function calls are supposed to be doing.</li>

 <li>Once you’re ready to begin coding, start by creating a skeleton c file. Add a header comment with your name and NID, add some standard #include directives, and be sure to #include “Varg.h” from your source file. Then copy and paste each functional prototype from Varg.h into Varg.c, transform those prototypes into functions by removing the semicolon and setting up curly braces for each function signature, and then set up all those functions to return dummy values (some arbitrary char or float, as appropriate).</li>

 <li>Test that your c source file compiles. Do this before you’ve even taken a stab at making the functions work! If you’re at the command line on a Mac or in Linux, your source file will need to be in the same directory as Varg.h, and you can test compilation like so:</li>

</ol>

gcc -c Varg.c

Alternatively, you can try compiling it with one of the test case source files, like so:

gcc Varg.c testcase01.c

For more details, see Section 12, “ Compilation and Testing (Linux/Mac Command Line).”

If you’re using an IDE (i.e., you’re coding with something other than a plain text editor and the command line), open up your IDE and start a project using the instructions above in Section 11,

“ Compilation and Testing (CodeBlocks)”. Import Varg.h, testcase01.c, and your new Varg.c source file, and get the program compiling and running before you move forward. (Note that CodeBlocks is the only IDE we officially support in this class.)

<ol start="6">

 <li>Once you have your project compiling, go back to Section 8, “Function Requirements”, and read through the function requirements. Do some brainstorming on how you want to solve the problem. Don’t even try to write any code yet. Just assume you’ll be able to get your function to</li>

</ol>




read all the arguments one by one, and think about what you’ll do with each argument as you receive it.

<ol start="7">

 <li>Load up c and give it a read. You might need to read it a couple times before it all starts to click. Don’t be discouraged by that. Your brain is re-wiring yourself as you read, and setting itself up to comprehend documents like that much more rapidly in the future.</li>

 <li>Once you kind of have a grasp of how to write variadic functions (even if it feels a bit vague at first), dive in fearlessly. Be bold! Go back to the list of required functions (Section 8, “Function Requirements”), and try to implement one function at a time, while referring to c regularly. Always stop to compile and test your code before moving on to another function! Throughout the semester, if you frequently stop to check whether your code is compiling, you will save yourself a lot of headaches.</li>

 <li>If you get stuck while working on this assignment, draw diagrams on paper or a whiteboard. Make boxes for all the variables in your program. Trace through your code carefully, step by step, using these diagrams.</li>

 <li>You’re bound to encounter errors in your code at some point. Use printf() statements liberally to verify that your code is producing the results you think it should be producing (rather than making assumptions that certain components are working as intended). You should get in the habit of being immensely skeptical of your own code and using printf() to provide yourself with evidence that your code does what you think it does.</li>

 <li>If you encounter a segmentation fault, you should always be able to use printf() and fflush() to track down the <em>exact</em> line you’re crashing on.</li>

 <li>This semester (especially in later programs), you’ll need to examine a lot of debugging output. You might want to set up a function that prints debugging strings only when you #define a DEBUG value to be something other than zero, so you can easily flip debugging output on and off. (Just be sure to remove your debugging statements before you submit your assignment, so your code is nice and clean and easy for us to read.)</li>

 <li>When you find a bug, or if your program is crashing on a huge test case, don’t trace through hundreds of iterations of some for-loop to track down the error. Instead, try to cook up a new main() function with a very small test case (as few lines as possible) that directly calls the function that’s crashing. The less code you have to trace through, the easier your debugging tasks will be.</li>

</ol>

<h2>14. Deliverables</h2>

Submit a single source file, named Varg.c, via Webcourses. The source file should contain definitions for all the required functions (listed above), as well as any auxiliary functions you need to make them work.

Your source file <strong>must not</strong> contain a main() function. Do not submit additional source files, and do not submit a modified Varg.h header file. Your source file (without a main() function) should compile at the command line using the following command:

gcc -c Varg.c

It must also compile at the command line if you place it in a directory with Varg.h and a test case file (for example, testcase01.c) and compile like so:

gcc Varg.c testcase01.c

Be sure to include your name and NID as a comment at the top of your source file.

<h2>15. Grading</h2>