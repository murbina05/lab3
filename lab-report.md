# Lab Report #3


## Part 1

Bellow is a method that would take a array and return it in reverse. However it is not correctly implemented. I will show two different tests one that would pass and one that would fail. First I pass it an array of 1, 2, 3. If you look closely at the method we never assign any values to newArray so when we copy we copy over nothing so if we give it 1, 2, 3 it will return an empty array which is wrong and will fail the assertArrayEquals.
```
 // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }


  @Test
  public void testReversed() {
    int[] input1 = {1, 2, 3};
    assertArrayEquals(new int[]{1, 2, 3}, ArrayExamples.reverseInPlace(input1));
  }

```


In this example bellow although the implementation of the method above is incorect if we give it an empty array when we call the method and it returns another empty array this technecally is the true it did as the method is supposed to. I think this highlights how important it is to have good testing. 

```
@Test
  public void testReversed() {
    int[] input1 = {};
    assertArrayEquals(new int[]{ }, ArrayExamples.reverseed(input1));
  }

```



![Image](https://i.imgur.com/DTfttIc.png)


In the image above you will see three tests for the reversed method. You can see that one passes and two fail. This is because the implementation of the method is incorrect. When we pass an empty array it passes because the method retruns an empty array. However, when we pass it an array with any values the method fails becuase it returns and empty array. Wehn we pass the method an array with only one values (1) we can see that it fails. This tells us that even when we have one values the method fails. Next we test passing an array with multiple values and you can see that it still fails. Which means that there is something broken. The fix for this code is actually pretty simple and I will show it bellow.



```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

The fix that I made was simple. The issue with the code was that it would make a new array but never assign it any values so when it would read from it it would actually override the arr array with nothing. What I did was make it so it copies the values in reverse order to a new array and return that instead. Bellow you will see the old implementation if you need a refresher on how it looked.



```
 // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```




## Part 2


For this part I will focus on the find command as I think that this command is one of the most useful command that you can use whenever you are working with text. 


You can use it to find everything in a directory. I will not include the whole output becuase it is too long however I will include a couple of the last results

```

murbina@Max:/mnt/c/Users/maxur/cse15/lab3/docsearch$ find technical/ *
technical/plos/pmed.0020275.txt
technical/plos/pmed.0020278.txt
technical/plos/pmed.0020281.txt

```


The example bellow is simialr to the one above except this time I will pipe it to wc to find the number of files

```

murbina@Max:/mnt/c/Users/maxur/cse15/lab3/docsearch$ find technical/ * | wc
   2811    2811  109050

```



Next I will include one that some may find boring, however I can not tell you how many times I have used this command when I am working on some projects

```
murbina@Max:/mnt/c/Users/maxur/cse15/lab3/docsearch$ find --help
Usage: find [-H] [-L] [-P] [-Olevel] [-D debugopts] [path...] [expression]

default path is the current directory; default expression is -print
expression may consist of: operators, options, tests, and actions:
operators (decreasing precedence; -and is implicit where no others are given):
      ( EXPR )   ! EXPR   -not EXPR   EXPR1 -a EXPR2   EXPR1 -and EXPR2
      EXPR1 -o EXPR2   EXPR1 -or EXPR2   EXPR1 , EXPR2
positional options (always true): -daystart -follow -regextype

normal options (always true, specified before other expressions):
      -depth --help -maxdepth LEVELS -mindepth LEVELS -mount -noleaf
      --version -xdev -ignore_readdir_race -noignore_readdir_race
tests (N can be +N or -N or N): -amin N -anewer FILE -atime N -cmin N
      -cnewer FILE -ctime N -empty -false -fstype TYPE -gid N -group NAME
      -ilname PATTERN -iname PATTERN -inum N -iwholename PATTERN -iregex PATTERN
      -links N -lname PATTERN -mmin N -mtime N -name PATTERN -newer FILE
      -nouser -nogroup -path PATTERN -perm [-/]MODE -regex PATTERN
      -readable -writable -executable
      -wholename PATTERN -size N[bcwkMG] -true -type [bcdpflsD] -uid N
      -used N -user NAME -xtype [bcdpfls]      -context CONTEXT

actions: -delete -print0 -printf FORMAT -fprintf FILE FORMAT -print
      -fprint0 FILE -fprint FILE -ls -fls FILE -prune -quit
      -exec COMMAND ; -exec COMMAND {} + -ok COMMAND ;
      -execdir COMMAND ; -execdir COMMAND {} + -okdir COMMAND ;

Valid arguments for -D:
exec, opt, rates, search, stat, time, tree, all, help
Use '-D help' for a description of the options, or see find(1)

Please see also the documentation at https://www.gnu.org/software/findutils/.
You can report (and track progress on fixing) bugs in the "find"
program via the GNU findutils bug-reporting page at
https://savannah.gnu.org/bugs/?group=findutils or, if
you have no web access, by sending email to <bug-findutils@gnu.org>.

```

I know a lot of text however whenever you work a lot with linux you will know how helpful --help is when you are useing something new for the first time. This will a lot of information on the command and give you insight into how to command works


Next if this is too much text you can pipe it to head and get only a little bit of text


```

murbina@Max:/mnt/c/Users/maxur/cse15/lab3/docsearch$ find --help | head
Usage: find [-H] [-L] [-P] [-Olevel] [-D debugopts] [path...] [expression]

default path is the current directory; default expression is -print
expression may consist of: operators, options, tests, and actions:
operators (decreasing precedence; -and is implicit where no others are given):
      ( EXPR )   ! EXPR   -not EXPR   EXPR1 -a EXPR2   EXPR1 -and EXPR2
      EXPR1 -o EXPR2   EXPR1 -or EXPR2   EXPR1 , EXPR2
positional options (always true): -daystart -follow -regextype

normal options (always true, specified before other expressions):

```


In the example bellow I will use -name argument. This searches for the pattern that you give it

```

murbina@Max:/mnt/c/Users/maxur/cse15/lab3/docsearch/technical$ find . -name *plos
./plos
```

For the example above I search for a the directory "plos" and the command runs and returns the path to that directory. This is useful to search for specific patterns and remember that you can chain this. If you wanted you could have a command you ran previously give you a pattern and then you use it here and look for it.


For the next example I will use the results of the command above and pipe it into another command. The reason why I like doing this is becasue often times when you are working in the command line you will have to something that will take multiples steps. What I mean by this is that there no command that can do it in one stepp so you use multiple different commands to get the answer that you want.


```
murbina@Max:/mnt/c/Users/maxur/cse15/lab3/docsearch/technical$ find ./plos/ -name pmed* | wc
    150     150    3600

```

The command above will look for the specific pattern that you give it and then you pipe it to wc. This is useful when you want to know how many files you are working with.



The next argument that I wnat to highlight is the argument -newer. This will look for files that are newer then the file that you give it. 

```
murbina@Max:/mnt/c/Users/maxur/cse15/lab3/docsearch/technical$ find -newer ./plos/pmed.0020275.txt
./plos
./plos/pmed.0020278.txt
./plos/pmed.0020281.txt
```

You can see that it returns a few files that is becuase those are the files that were edited/downlowad after the file that I gave. This would be useful if you are trying to debug a program and want to see if you are editing something before or after a file such a a log file.


Lastly I am going to once more pipe it into wc. The reason that I like doing this is because within wc you can do a lot and I wish I could include some more examples.



```
murbina@Max:/mnt/c/Users/maxur/cse15/lab3/docsearch/technical$ find -newer ./plos/pmed.0020275.txt | xargs wc | sort -k2
wc: ./plos: Is a directory
      0       0       0 ./plos
     41     372    2738 ./plos/pmed.0020278.txt
     40     387    2811 ./plos/pmed.0020281.txt
     81     759    5549 total
```

In the example above I will look for all files that are newer then the file I passed it, I will then cound the number of characters in the file and sort based on that. This is a nice trick you can use and shows how you can chain multiple commands with the piping operator.


For this lab report I did not use any other resources. Most of these examples have just been different uses that I have found with find and have been able to use for multiple different purposes. 
