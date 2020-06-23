# Encryption, decryption & hashing

# Encryption

Encryption is the practice of scrambling information in a way that it can only be unscrambled with a corresponding key. Encryption is a **two-way** function - when we encrypt something, we do it with the intention of **decrypting** it later.

## Manual decryption methods

* Ceasar chiffre - letters are shifted in a certain way (left or right, example: A B C D E --->  C D E F G), very easy & unsafe
* Skytale - parchment roll wrapped around a stick of a certain diameter and written - can only be read with a stick with the exact same diameter

## Digital encryption methods

### History

#### DES - Data Encryption Standard

56-bit key length, could be broken by brute force key serach. Still used in online-banking today.

#### AES

Block chiffres based on a substitution-permutation-network (SPN). The transformation of the initial text happens in multiple rounds with the same structure.

Block length: 128 Bit.

**Algorithm:**

1. KeyExpansion - round keys are derived from the cipher key, separate round key block for each round plus one more.
2. Initial round key addition:
    * AddRoundKey - each byte of the state is combined with a byte of the round key using bitwise xor.    
3. 9, 11 or 13 rounds:
    * SubBytes - each byte is replaced with another according to a lookup table
    * ShiftRows - last three rows are shifted cyclically a certain number of steps
    * MixColumns - operates on the columns, combining the four bytes in each column
    * AddRoundKey
4. Final round (making 10, 12 or 14 rounds in total):
    * SubBytes
    * ShiftRows
    * AddRoundKey

**Usages:**

* IEEE 802.11 (Wifi)
* SSH
* OpenSSL
* Encryption of disk images or file archives
* VoIP


#### RSA

Based on the difficulty of splitting large numbers into their prime factors.

### Practical usages for encryption

#### Data encryption

//TODO continue

# Hashing