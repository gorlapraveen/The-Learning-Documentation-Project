Encrypt and decrypt using a standard encryption algorithm (from a library), and encode the encrypted sting using base 64 (from the base64 module).

**Your workflow becomes:**

    Encrypt the plaintext using a crypto library (gives you the ciphertext)
    Encode the ciphertext using base 64 (gives you an encoded ciphertext, this is URL proof)
    Decode the encoded ciphertext using base 64 (gives you the ciphertext back)
    Decrypt the ciphertext using a crypto library (gives you the plaintext back)

A few encryption libraries:
[m2crypto](http://chandlerproject.org/Projects/MeTooCrypto)

[pycrypto](https://www.dlitz.net/software/pycrypto/)

[pynacl](https://pynacl.readthedocs.org/en/latest/)

Source - https://stackoverflow.com/questions/19369154/encrypting-and-decrypting-in-python-without-using-special-characters

------------------------------------------

1. In general for gpg encryption(decryption) see my repo [docs](/docs/encrypt/ssh-gpg.md)

To encode text to base64, use the following syntax:

     $ echo -n 'scottlinux.com rocks' | base64
     
    c2NvdHRsaW51eC5jb20gcm9ja3MK

To decode, use base64 -d. To decode base64, use a syntax like the following:

    $ echo -n c2NvdHRsaW51eC5jb20gcm9ja3MK | base64 -d
    
    scottlinux.com rocks

