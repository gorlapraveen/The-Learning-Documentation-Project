
## Searx

**Install `searx` in your local system and make `firefox` to use it through your localhost for browsing Internet**

Initially I followed basic installation as described in https://github.com/asciimoo/searx . It includes

## Installation

clone source: `git clone https://github.com/asciimoo/searx.git && cd searx`

install dependencies: `./manage.sh update_packages`

edit your settings.yml (set your secret_key!) ##Actuall no need, unless you host this as online for others user to access, you can give any arbitary key as described in https://github.com/asciimoo/searx/issues/1473 
run `python searx/webapp.py` to start the application

By Default `searx` search is runs in your local system and available to you at `localhost:8888` 
 1. Go to firefox
 2. Enter `localhost:8888` in the search bar
 3. `searx` search engine is available as shown below and you can search the web. 
 

<p align="center">
<center><img src="images/searx-1.png" text="Logo" width="50%" /></center>
</p>


**But I thought of Automate the process So, I did the following**

4. In order to make your local `serax` as your default search engine in firefox,   vist your loal `searx` page at `localhost:8888`. After that at the search bar, fint `page options` >> `Add Search engine`
 **But Everytime you need to go to the directory where you have cloned and need run `python searx/webapp.py ` to access your local `searx` engine in firefox (or any other browser through `localhost:8888`)**. Instead you can automate the process just by issuing the command in your termianl from any directory with the following script. 


    #!/bin/bash
     bash -c "sudo lsof -t -i tcp:8888 -s tcp:listen | sudo xargs kill -KILL" #to kill the proper process on 8888 port.
     bash -c "python /path_to_searx/searx/webapp.py"

Name the script as `searx` (or anyname) and place it in `/usr/bin/` (in Debian Based systems) and assign user permissions for the script

5. Then open terminal and run `searx` or anynmae that you assigned for script

----------------------------------------------------


**But If you want to run the loacl searx engine at the sart up and avoid issuing commands to start, you the following script**




 
 