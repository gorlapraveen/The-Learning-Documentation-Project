# Learning.PraveenGorla.org

## Documentation : ## 

**Documentation started:** *02-oct-2018*

*This documentation is about the new learning(s) and issue(s) resolvings on different aspects of academic, professional and personal thoughts.* 

It includes(or/with links): *Research topics(& resources), Programming(issues and code),  Advanced Linux commands, Networking commands, bash script command utilization, Linux packages(& scripts), Machinine learning, text documentation, images, tutorial(links) and gitlab links(Personal repository links).*

Note : *This documentation is mainly intend to reduce time consumption for solving some issues which are already solved/used earlier, This is from my past experience of wasting my time for searching for issues solving* -- by @gorlapraveen

---------------------------------------------------------------------------------------------------

### Advanced Used Linux Commnd - Utilization for scripting:

  **AWK Command:**
  
        For eaxmple to extract substring in a string .

            Ex: str1 =abcdefgh
  `awk substr($str1,2,4)`:output = `bcdef`
 
  **SSH Keys:**
  
For generating, show existing list, shh-add etc..
         
* ssh key generation: `ssh-keygen -t rsa -b 4096 -C "your_email@example.com" `. This creates a new ssh key, using the provided email as a label.
`Generating public/private rsa key pair`.
* ssh exsiting key presented check: Enter `ls -al ~/.ssh` to see if existing SSH keys are present:
`
* ssh existing public disply : `cat ~/.ssh/id_rsa.pub` its ssh key  should look like
 
      ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSUGPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XAt3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/EnmZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbxNrRFi9wrf+M7Q== schacon@mylaptop.local

* Adding your SSH key to the ssh-agent :
  - * Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key. 
     - * Start the ssh-agent in the background.`eval "$(ssh-agent -s)"` 
     - * Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.
        `ssh-add ~/.ssh/id_rsa`
     - * If you are working in git directory and if you want to add ssh access, you need to past your ssh publice keys in your git server and initiate ssh authentication in your local repo by simply issuing command in local repo as `ssh-add` or `ssh-add agent_id_number`
     `

For more vist https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key
 and 
https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/


** GPG : Keysigning **

The intent of this manual is to explain how you can create and sign a GPG key. 
 
* Generatin(creating) a RSA Keypair :`gpg --gen-key` or `gpg2 --gen-key` 
 - * Select `(1) RSA and RSA (default)`
 - * select `4096` for strong key(debian recomended)
 - * Enter expiry date
 - * Enter `Real name`, `Email[trusted]` and `comment`
 - * After this gpg random key generation takes place and it looks something like this.
 - * * 
 

--------------------------------------------------------------------------------------------------
### Bash Scripting - With some used commands
**Arrays in bash script:**

        Ex: arr=(Helloworld)
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



--------------------------------------------------------------------------------------------------
### Used Python Scripting :











