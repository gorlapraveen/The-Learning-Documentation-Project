Kill process running on port 80

There are several ways to find which running process is using a port.

Using fuser it will give the PID(s) of the multiple instances associated with the listening port.

sudo apt-get install psmischttp://unix.stackexchange.com/questions/244531/ddg#244534
sudo fuser 80/tcp

80/tcp:               1858  1867  1868  1869  1871

After finding out, you can either stop or kill the process(es).

You can also find the PIDs and more details using lsof

sudo lsof -i tcp:80

COMMAND  PID     USER   FD   TYPE DEVICE SIZE/OFF NODE NAME  
nginx   1858     root    6u  IPv4   5043      0t0  TCP ruir.mxxx.com:http (LISTEN)  
nginx   1867 www-data    6u  IPv4   5043      0t0  TCP ruir.mxxx.com:http (LISTEN)  
nginx   1868 www-data    6u  IPv4   5043      0t0  TCP ruir.mxxx.com:http (LISTEN)  
nginx   1869 www-data    6u  IPv4   5043      0t0  TCP ruir.mxxx.com:http (LISTEN)  
nginx   1871 www-data    6u  IPv4   5043      0t0  TCP ruir.mxxx.com:http (LISTEN)  

To limit to sockets that listen on port 80 (as opposed to clients that connect to port 80):

sudo lsof -i tcp:80 -s tcp:listen

To kill them automatically:

sudo lsof -t -i tcp:80 -s tcp:listen | sudo xargs kill

--Rui F Ribeiro
More at [Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/244531/ddg#244534)  