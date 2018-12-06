If your GPG private key becomes compromised, you need to revoke it to warn others not to trust future signatures or encrypt data to your public key. However, by the time a key compromise happens, you might not have your GPG key available, such as if it resided on hardware stolen from you, or the attacker removed it after accessing it. This article shows you how to generate and preserve a revocation certificate now, before you actually need it.

A revocation certificate consists of a signed message, stating in machine-readable form that 
a key no longer has validity for future cryptographic operations. 
To generate a revocation certificate for a key, use the `--gen-revoke` option to `gpg`, passing it the `key ID` of the key you want a revocation certificate for. 
You should also supply the `--output` option to specify where to put the certificate. The exchange with gpg looks like this:


## Generating Revocation Certificates:

The exchange with gpg looks like this:


      $ gpg --output revocation-certificate.asc --gen-revoke 8C730530

      sec  1024D/8C730530 2018-10-23 Your Name <your.email@example.org>

     Create a revocation certificate for this key? (y/N) y
     Please select the reason for the revocation:
       0 = No reason specified
       1 = Key has been compromised
       2 = Key is superseded
       3 = Key is no longer used
       Q = Cancel
        (Probably you want to select 1 here)
      Your decision? 0
     Enter an optional description; end it with an empty line:
      > 
    Reason for revocation: No reason specified
    (No description given)
      Is this okay? (y/N) y

    You need a passphrase to unlock the secret key for
      user: "Your Name <your.email@example.org>"
      1024-bit DSA key, ID 8C730530, created 2018-10-23

    ASCII armored output forced.
     Revocation certificate created.

     Please move it to a medium which you can hide away; if Mallory getsaccess to this certificate he can use it to make your key unusableIt is smart to print this certificate and store it away, just in caseyour media become unreadable.  But have some caution:  The print system ofyour machine might store the data and make it available to others!


## Using Revocation certificates : In the event of loss of Private key/No Longer used/Key Compromised


Heed `gpg`'s warning here: anyone with this certificate can revoke your private key. I recommend printing it out and storing it in a secure location. You could also burn it to a CD and store the CD in a secure location.

f the worst happens, and you need to revoke your key, obtain the revocation certificate, and import it into gpg:

    $ gpg --import revocation-certificate.asc
      gpg: key 8C730530: "Your Name <your.email@example.org>" revocation certificate imported
      gpg: Total number processed: 1
      gpg:    new key revocations: 1
     gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
    gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
    
    
You can now observe the key revocation via --list-keys with your key ID:

    $ gpg --list-keys 8C730530
      pub   1024D/8C730530 2018-10-23 [revoked: 2018-10-23]
      uid                  Your Name <your.email@example.org>

In order for others to see the revocation, you should send the revoked key to a keyserver, with

     gpg --send-keys 8C730530

For more information on using gpg, the GNU Privacy Guard, see the GNU Privacy Handbook.

    
    