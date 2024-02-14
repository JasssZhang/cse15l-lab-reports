# Lab Report 03
*Jasmine Zhang A17371205*

## Part 01 - Bugs

**Bug to analyze**

Here, I choose to work on the bugs in `ArrayExamples.java`, specifically, the bugs in method `reverseInPlace(int[] arr)`.

**Failure-inducing input**

```
@Test
public void testReverseInPlace2(){
   int[] threeElements = {1, 2, 3};
   ArrayExamples.reverseInPlace(threeElements);
   assertArrayEquals("check array updated", new int[]{3, 2, 1}, threeElements);
}
```

**Input does not induce failure**

```
@Test 
public void testReverseInPlace() {
   int[] oneElement = {1};
   ArrayExamples.reverseInPlace(oneElement);
   assertArrayEquals("check array updated", new int[]{1}, oneElement);
}
```

**Symptoms with screenshots**

![Image](L3S1.png)

From the screenshot above, we can see that two tests ran, with 1 failure. The succeeded test method is `testReverInPlace()`. The failure test method is `testReverseInPlace2()`. The value of the actual array at index 2 (which is 1) is different than the expected value (which is supposed to be 1). From this error message, we know that one of our test cases failed, and there is a wrong implementation in our method. Specifically, we did not return the correct array in reversed order.


**Bug with before-and-after code**

**Before**

```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

**After**

```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    //store original array
    int[] newArr = new int[arr.length];
    //copy arr to newArr
    for(int i = 0; i < arr.length; ++i){
      newArr[i] = arr[i];
    }
    //change input array to reversed order
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArr[newArr.length - i - 1];
    }
  }
```

The bug of this method is that it did not copy the original array over as a new array before entering the for loop to assign reversed value to the original array. In this situation, assigning elements from end of the array to start would alter elements in start of `arr`, thus when it comes to assigning from start to end, we would be assigning elements that has been overwritten already. We need to store the elements in `arr` so that elements in the array would not change as we assign elements from end to start to reverse the order.

To fix the bug, we can create a new array `newArr` and use a for loop to copy elements in `arr` to `newArr`. Now that every element is stored in `newArr`, we can write a for loop to assign the last element in `newArr` to first in `arr`, second last in `newArr` to second in `arr`, etc. In this way, we are assigning the correct elements from end to start, since elements in `newArr` are copied from `arr` and will not be changed as we alter the `arr` array itself. As a result, we would changed the input array to be its reversed order correctly by fixing the code.

## Part 02 - Researching Commands

**Interesting command line options**

For this part, I decide to research more interesting command line options on the command `find`.

**Option 1: `-type`**

One command option to use `find` is with `-type`. Here, for example, `-type f` represents only files while `-type d` represents only directories. With this command, we would be able to find just a single category of things, for example, finding only files and only directories.

**Option 2: `-path <pattern>`**

This command would take in a path as pattern, and return the path to a file or directory if there exists such file or diretcory that matches the input `<pattern>`. With `-path` command, we could predict a path and see if there exists something that matches with our prediction. Note that for the `<pattern>`, we need to make sure that the path we put in is absolute and correct.

**Option 3: `-daystart`**

`-daystart` is a set of command options that would measure time from the beginning of today. Using it as a `find` command option would return absolute path of files that satisfies the time limit condition. For example, `-amin` measures time in minute, while `-atime` measures time in 24 hours period (1 day), and our input integer after the command would help us locate files and directories that have been accessed within the time frame. 

**Option 4: `-iname`**

This command is similar to the `-name` command we learnt in class, but it is a more general and error-tolerant approach as it is less sensitive to user input. It would be able to locate file with characters of your input, regardless of whether they are types as capital or lower cases letter. 

**Two examples on each option**

**Option 1: `-type`**

*Example 1*

```
$ find -type d
.
./911report
./biomed
./government
./government/About_LSC
./government/Alcohol_Problems
./government/Env_Prot_Agen
./government/Gen_Account_Office
./government/Media
./government/Post_Rate_Comm
./plos
```

Here I `cd` into `technical` and used the command `find -type d`. The terminal output prints out the paths of all existing directories under `technical`. This command is useful because it allows us to count and see what directories are located within the current directory very clearly, without distractions from other types of files within the directory.

*Example 2*

```
$ find -type f
./journal.pbio.0020001.txt
./journal.pbio.0020010.txt
./journal.pbio.0020012.txt
./journal.pbio.0020013.txt
./journal.pbio.0020019.txt
./journal.pbio.0020028.txt
```

The output is too long so I did not copy down the whole code block, just a few at the front as example. Here, I `cd` into `plos` and used the command `find -type f`. The terminal prints out all absolute paths to existing files under the directory `plos`. Similarly, this command is useful as it would exclude other types and only return paths to existing files. This would help us check files of this specific type more clearly, without distractions from other types like the directory itself.


**Option 2: `-path <pattern>`**

*Example 1*
```
$ cd technical
$ find -path "./biomed"
./biomed
```

Here, I `cd` into `technical` and used the command as `-path "./biomed"` with `"./biomed"` as the input `<pattern>`. Since there is a directory that matches with our input under `technical`, the absolute path to that directory is printed out in the terminal. This is really useful since it can help us check if a certain directory exists quickly, without having to print out all directories and manually go through each one of them.

*Example 2*
```
$ cd plos
$ find . -path "./pmed.0020281.txt"
./pmed.0020281.txt
```

Here, I `cd` into `plos` from `technical` and used the command as `-path "./pmed.0020281.txt"` with `"./pmed.0020281.txt"` as the input `<pattern>`. Since we can find a file that matches with our input under `plos`, the terminal would print out the absolute path of that specific file in the terminal as output. Similarly, since there could be many files in a directory, it is tedious to check if a certain file exists. This command is thus useful since it allows us to see directly if a file with a certain path exists directly by looking at the terminal output.

**Option 3: `-daystart`**

*Example 1*

```
$ find -amin -5
.
./pmed.0010008.txt
```

Here, I have edited the file `pmed.0010008.txt` under `plos` in advance. I tried the command `-amin -5`, and the input integer `-5` part means that it would return files that were accessed or modified less than 5 minutes ago. This command is useful as it would help us to locate files that we were working on a few minutes ago if we lost track of it. This saves us the tedious step of checking each file one by one, especially when there are a lot of files in the directory.

*Example 2*
```
$ find -atime -1
.
./journal.pbio.0020001.txt
./journal.pbio.0020010.txt
./journal.pbio.0020012.txt
./journal.pbio.0020013.txt
./pmed.0010008.txt
```

Here, I tried the command '-atime -1', and the input integer `-1` means that it would return files that were accessed less than 1 day ago. This command is useful too as it can help us track back our progress within a given time period, in this case within one day, and it would help us find out directly which files were accessed and edited.

**Option 4: `-iname`**

*Example 1*

```
$ find -iname "PMed.0020281.txt"
./pmed.0020281.txt
```

Here, I `cd` into `plos` and used the `-iname` command to find files with the name `pmed.0020281.txt`. Here, my input is `PMed.0020281.txt`, which is not the exact file name, with difference in captalized letter. `-name` command will not be able to return the correct path to the file; however, the more insentitive `-iname` command would be able to locate the file if it exists and return its absolute path. This command is useful since it is more comprehensive and allows for more "errors" in input file name than regular `-name` command. It would be able to return the correct path even though user failed to put capital or lower cases letter correctly.

*Example 2*

```
$ find -iname "JouRnaL.pbio.0030051.txt"
./journal.pbio.0030051.txt
```

Here, working directory is `plos`. I wish to find the file `journal.pbio.0030051.txt` with the command `-iname`. My input is not the exact file name, with wrong capitalized letters. The terminal output was correct though with the right absolute path to the file I want. Similar to the first example, we can tell that this command is useful when we make typos for capitalized letters in the input pattern. It could tolerate more "errors" and is a more insensitive command comparing to `-name`.

**Source citation**

Websites used:

https://snapshooter.com/learn/linux/find

https://www.computerhope.com/unix/ufind.htm

