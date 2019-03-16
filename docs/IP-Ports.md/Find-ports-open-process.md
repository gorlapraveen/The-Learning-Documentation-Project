 `netstat -pln`

`-l` will list listening ports, `-p` will also display the process, `-n` will
show port numbers instead of names. Add -t to only show TCP ports.


For the `-p` to work properly, you need to run this as root, so sudo `netstat -tpln`,
otherwise the process column will not be particularly useful, unless you're the user whose process is listening on a given port.

---------------------------------------------------------------------------
You can do:`netstat -an | egrep 'Proto|LISTEN'`

or simply:`netstat -anl` which will give you all listening sockets on the system.

----------------------------------------------------

Source at https://serverfault.com/questions/357323/how-can-i-list-my-open-ports-on-debian