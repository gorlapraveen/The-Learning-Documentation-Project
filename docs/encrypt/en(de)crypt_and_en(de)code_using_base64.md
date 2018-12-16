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