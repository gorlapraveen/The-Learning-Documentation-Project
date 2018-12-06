# SSH and GPG Generation/Usage 


**SSH Keys:**
  
  1. SSH-Client :If you don't have ssh installed, normally the client is installed by default. If not it suffices to run as root:  Install it with `apt-get install openssh-client` .
  2. SSH-server : The server allows to connect remotely and gets installed by running as root: `apt-get install openssh-server`
For generating, show existing list, shh-add etc..
         
* ssh key generation: `ssh-keygen -t rsa -b 4096 -C "your_email@example.com" `. This creates a new ssh key, using the provided email as a label.
`Generating public/private rsa key pair`.
* ssh exsiting key ID check: Enter `ls -al ~/.ssh` to see if existing SSH keys are present:
`
* ssh existing public display : `cat ~/.ssh/id_rsa.pub` its ssh key  should look like
 
      ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSUGPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XAt3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/EnmZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbxNrRFi9wrf+M7Q== schacon@mylaptop.local

* Adding your SSH key to the ssh-agent :
  - * Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key. 
     - * Start the ssh-agent in the background.`eval "$(ssh-agent -s)"` 
     - * Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.
        `ssh-add ~/.ssh/id_rsa`
     - * If you are working in git directory and if you want to add ssh access, you need to past your ssh publice keys in your git server and initiate ssh authentication in your local repo by simply issuing command in local repo as `ssh-add` or `ssh-add agent_id_number`
     `



**Adding SSH-Agent to (GIT Kind of) Local repository:**

This makes you not to enter `ssh-agent` password every time you push or pull the remote repository.

  * Once you have started the SSH agent with: `eval $(ssh-agent)`

   *    You have to add your private key to it: `ssh-add` 
   This will ask you your passphrase just once, and then you should be allowed to push, provided that you uploaded the public key to Github.

   *  To save key permanently: `ssh-add -k`  This will persist it after you close and re-open it by storing it in user's keychain.
   * for more vist ` https://stackoverflow.com/questions/10032461/git-keeps-asking-me-for-my-ssh-key-passphrase#10032655`


For more vist https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key
 and 
https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

 ------------------------------------------------------------------------------------------------
 
  ------------------------------------------------------------------------------------------
 
**GPG : Keysigning**
 Install gnupg (or) gnupg2 by : `apt install gnupg` or `apt installl gnupg2`(for latest version of GNUpg 2)

The intent of this manual is to explain how you can create and sign a GPG key. 
 
* Generatin(creating) a RSA Keypair :`gpg --full-generate-key`  [`gpg --gen-key` can also be used but results in onlydefault basic key generation, such as default 2048 start for below,  option (3), giving no option for choosing  4096 or any other Encryption Algoritham] or `gpg2 --full-generate-key` 
 - * Select `(1) RSA and RSA (default)`
 - * select `4096` for strong key(debian recomended)
 - * Enter expiry date
 - * Enter `Real name`, `Email[trusted]` and `comment`
 - * After this gpg random key generation takes place and it looks something like this.
 

       `gpg: /home/user/.gnupg/trustdb.gpg: trustdb created`
       
     `gpg: key 23955501 marked as ultimately trusted`
     
     `public and secret key created and signed.`

     `gpg: checking the trustdb`
     
     `gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model`
     
     `gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u`
     
     `gpg: next trustdb check due at 2021-05-11`
     
     `pub   4096R/23955501 2016-05-12 [expires: 2021-05-11]`
     
     `Key fingerprint = 519D 4592 3D31 56E6 B7A8  269E F9E2 35C3 2395 5501`
     
     `uid                  Test User <test@example.org>`
     
     `sub   4096R/653CA81D 2016-05-12 [expires: 2021-05-11] `
 
 
 **ADD other UID(other email to same GPG key):**
 
 If you need to add more than one email address to your key:
 
 - * Edit existing key to associate other UID(emial) by `gpg --edit-key '519D 4592 3D31 56E6 B7A8  269E F9E2 35C3 2395 5501'`
 - * add user by `gpg> adduid` then `Real name`, `Email address`, `Comment`
 - * Give `previous passphrase` to unlock the existing key and associate this email to that key.
 - * * It look that 2 of your UID is added:(like)
 - * * * [ultimate] (1). Test User <test@business.example>
 - * * * [ultimate] (2)  Test User <test@example.org>
 - * Finally save it by `gpg> save`.

**SET primary UID(When two or more UID are associate with GPG same key):**

  - * Edit existing key: `gpg --edit-key '519D 4592 3D31 56E6 B7A8  269E F9E2 35C3 2395 5501'`
  - If you(we) want `uid 2` i.e `[ultimate] (2)  Test User <test@example.org>` to be used as primary key thwn 
  - * * Give `gpg> uid 2` and`gpg> primary`.
  - * * Finally `gpg> save` .
  

**List gpg key in LONG Format**: `gpg --armor --export KEY_ID` here `KEY_ID` is `23955501` , the last 8 digits for gpg key.

Find more at https://keyring.debian.org/creating-key.html

  ----------------------------------------------------------------------------------------------

