# Messcrypt
Looking to keep something a secret? How about encrypting that secret with an image.
The image key can be an image already in your camera roll which means there is no need to keep a long encryption key around.

<br>

![](https://i.imgur.com/B5UNvQ2.png)

## Crypto
The Node.js Crypto module is used here for the encrypting and decrypting of messages. 
The way the AES encryption key is generating depends on the image key’s data URL representation. 
Decryption generates a key using this method in reverse.


## Still in development
A lot of the main functionality has been implemented. The features page, contact page, and the help tab still need to be set up.