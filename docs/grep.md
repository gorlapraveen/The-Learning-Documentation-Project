The grep command syntax in Linux / Unix

The syntax is as follows:

    grep 'word' filename
    grep 'word' file1 file2 file3
    grep 'string1 string2'  filename
    cat otherfile | grep 'something'
    command | grep 'something'
    command option1 | grep 'data'
    grep --color 'data' fileName



Search /etc file for abc user, enter:
       
      $ grep abc /etc/

Sample outputs:

       foo:x:1000:1000:abc,,,:/home/abc:/bin/

You can force grep to ignore word case i.e match abc, Abc, ABC and all other combination with the -i option:
    
        $ grep -i "abc" /etc/passwd
     
How to use grep recursively

You can search recursively i.e. read all files under each directory for a string “192.158.15.5”
     
        $ grep -r "192.158.15.5" /etc/

OR

       $ grep -R "192.158.15.5" /etc/

Sample outputs:

       
      /etc/NetworkManager/system-connections/Wired connection 1:addresses1=192.158.15.5;

You will see result for 192.158.15.5 on a separate line preceded by the name of the file (such as /etc/ppp/options) in which it was found. The inclusion of the file names in the output data can be suppressed by using the -h option as follows:

       $ grep -h -R "192.158.15.5" /etc/

OR

         $ grep -hR "192.168.1.5" /etc/

Sample outputs:

     abc 192.158.15.5

How to use grep to search words only

When you search for abc, grep will match fooboo, boo123, barfoo35 and more. You can force the grep command to select only those lines containing matches that form whole words i.e. match only boo word:
     
     $ grep -w "abc" file
     
How to use grep to search 2 different words

Use the egrep command as follows:
    
    $ egrep -w 'word1|word2' /path/to/file
    
How can I count line when words has been matched

The grep can report the number of times that the pattern has been matched for each file using -c (count) option:
    
      $ grep -c 'word' /path/to/file

Pass the -n option to precede each line of output with the number of the line in the text file from which it was obtained:
      
      $ grep -n 'root' /etc/passwd



Force grep invert match

You can use -v option to print inverts the match; that is, it matches only those lines that do not contain the given word. For example print all line that do not contain the word bar:
      
      $ grep -v bar /path/to/file
      
UNIX / Linux pipes and grep command

grep command often used with shell pipes. In this example, show the name of the hard disk devices:
     
     dmesg | egrep '(s|h)d[a-z]'

Display cpu model name:
     
     cat /proc/cpuinfo | grep -i 'Model'

However, above command can be also used as follows without shell pipe:
      
       grep -i 'Model' /proc/cpuinfo

Sample outputs:

         model		: 30
         model name	: Intel(R) Core(TM) i7 CPU       Q 820  @ 1.73GHz
         model		: 30
        model name	: Intel(R) Core(TM) i7 CPU       Q 820  @ 1.73GHz

How do I list just the names of matching files?

Use the -l option to list file name whose contents mention main():
      
      $ grep -l 'main' *.c

Finally, you can force grep to display output in colors, enter:
       $ grep --color abc /etc/passwd
