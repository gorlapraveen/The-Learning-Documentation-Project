### Bash Scripting - With some used commands

Execting Linux commands in bash: `basch -c $(Linux command)`
**Arrays in bash script:**

        Ex: arr=(Hello world)
Prints: for `arr[0]`=`Hello`, for `arr[1]`=`world`

         for : echo ${arr[0]} ${arr[1]}

prints `Hello world`

Extracting a Substring from Variable:
     
         test="Welcome to the Land of Linux"
         echo "Our variable test is ${#test} characters long"
         test1=${test:0:7}
         test2=${test:15:13}
         test3=${test:0}
         echo $test1
         echo $test2
         echo $test3

Output:

 
        Our variable test is 28 characters long
        Welcome
        Land of Linux
        Welcome to the Land of Linux

**Reading file to array, Find leangth of array**
    
Suppose we have a file `inactivity.txt` and the file contains the following:


     Apple
     12
     32
     cat
     56
     45
 
 Then in `bash` to read the file in array, lenghth of array and processing array as follows:
 
 
     #!/bin/bash
     readarray array < inactivity.txt     #Exports file to an array
     lenarray=${#array[@]}                # {#arry}Finds the length of the array,*or@ is used to define the entire array. 
     echo ${array[$lenarray-4}            # Output is `32`  #Indexing starts from 0
     echo ${array[$lenarray-1]}           # Output is `45`
     
     
