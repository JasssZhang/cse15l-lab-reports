# Lab 5
*Jasmine Zhang A17371205*

## Part 1 – Debugging Scenario
**Original Student Post of Bug**

Hi, I am having difficulty for passing the tests in lab7. I have correctly changed line 15 to result.add(s), and line 44 to index2, but the second merge test failed. Is it anything I did that caused the error, or are there other bugs in the program that I did not notice? 

Also, when I'm trying to run the bash script to test the program, it's giving me strange error message in the terminal saying things like `org.junit` does not exist, or `@Test` symbol is not found, etc. I double checked that I did not changed the bash script given in the cloned repository, also JUnit is correctly installed and imported. I wonder what might be the issue there. Thank you so much for your time!


**TA's Response**

**Student's Try and Output**

**Additional Information**

1. File & directory

   I designed this bug from `https://github.com/ucsd-cse15l-s23/lab7` in Week7's lab activity. File used are `ListExamples.java`, `ListExamplesTests.java`, and `test.sh`. Directory is `lab7`.

2. Before fixing the bug

   Edits I made to design the bug in `ListExamples`:

   Line 15: change result.add(0, s) to result.add(s);

   

4. Triggering the bug

5. Fix the bug




## Part 2 – Reflection
One thing I learnt from lab in this second half of quarter is the Java Debugger(jdb) in Week8. I find it cool and useful as it allows users to test the program, edit from the command line, and find potential bugs in the program. Once we type in the compile and run command of jdb, we can enter a "debugging shell" in the terminal that allows us to freely enter commands to design our own specific debugging program. Here, `stop at` stops the program after certain line, `run` initializes jdb and gives us the output of tests. From those output information, we can deduce what is potentially going wrong in the program. What is more, we can further type in `locals` to get all values of current local values, or `print` to print out certain variable's value. These are commands that can give us further knowledge on the program and help us find the bug more efficiently.
