## Encrypt a file to sent to your firend/other person

-------------------------------------------------------
1. ***Import your friends publice key** and **verify the key** from global keyserers.

   1. Import Keys: import Keys using your friend `KEY-ID` or `email` or `Real Name`
     
    
        $ gpg --search-keys --keyserver keys.gnupg.net 'KEY-ID'

        or
 
        $ gpg --search-keys --keyserver keys.gnupg.net 'E-Mail ID'

        or

        $ gpg --search-keys --keyserver keys.gnupg.net 'Real Name'

        or If your frineds gives his publices in `Friend_Publice_key.gpg` you can import using following command 
        gpg --import Friend_Publice_key.gpg

  2. Then Verify the Keys :
    
     Verify the successful import of your friend publice key by `gpg --list-keys`, then you have you friend's `Raksi` Key.

           pub   4096R/AB2724A8 2017-12-03
           uid                  raksi (Raksi's test ID)
           sub   4096R/84RF55EE 2014-12-03 
  
2. Then **Encrypt a file** `test.tx`  using your friend's publice key (Where he can only decrypt this message with his own private key) and send it to him.
 

          gpg --encrypt --recipient raksi a.txt

          gpg: 84RF55EE: There is no assurance this key belongs to the named user

          pub  2048R/84RF55EE 2012-12-03 raksi (Raksi's test ID)
         Primary key fingerprint: FF32 7764 A0AE 1E85 AC4B  C2F7 8AED B292 F2B7 42A8
         Subkey fingerprint: D6A5 7107 77C8 6845 2F86  765C EEED DD85 84RF 55EE

         It is NOT certain that the key belongs to the person named
         in the user ID.  If you *really* know what you are doing,
         you may answer the next question with yes.

         Use this key anyway? (y/N) y
   1. A file `test.txt.pgp` will be created with some binary data. If you dont want it tobe in binary format , you can choose to have in ASCII format by using the `gpg --encrypt --armor --recipient raksi test.txt` which creates `test.txt.pgp` having ASCII values.
    
   2. Send this `test.txt.pgp` file to your firend by any means, preferably use end-to-end encrypted channels (it couls be mail, chat or etc).


3. **Decrypt a File (By your friend)**
      

