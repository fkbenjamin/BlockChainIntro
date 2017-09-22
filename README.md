# An Introduction into Blockchain
I created this repository in order to explain the basics of blockchain to some friends and family. If you have any comments, if I explained something wrong or if you just want to say "Hi", just send me an email to flo.liss@gmail.com
If you want to support me, I  really appreciate donations to 0x00000
# Abbreviations
I will use the following abbreviations:

**BC** - *Blockchain*
# What is a Hash?
Hashes are an important concept for understanding how a BC works. A hash function is a mathematical function/ an algorithm that maps data of arbitrary size to data of a fixed size. So whatever we use as input for a hash function, the output will always have the same format. The output of a hash function is called a hash. 

There are many types of hash functions, one of them are cryptographic hash functions. As the name states they are used in cryptography. Cryptographic hash functions have special properties. 
  1) They are *deterministic*. That means that a certain input will always produce the same output.
  2) They are *one-way functions* which means, that it is easy to calculate the output of the functions for a certain input, but it is really hard to find the input for a given output.
  3) They are supposed to be *collision-free*. That means that there shouldn't be two different inputs that map to the same hash.  Since there are endless possibilities of inputs and only a fixed number of possible outputs, there will always be some collisions. But modern hash functions are so sophisticated that the probability of two inputs mapping to the same hash is close to zero.
  
###### KECCAK-256
**KECCAK-256** is a hash function that is part of the **SHA-3** family. **SHA-3** stands for *Secure Hash Algorithm 3* and is an established standard for hash functions. **KECCAK-256** is interesting for us since it is used by Ethereum, the BC we will focus on in this introduction. The number 256 in the name stands for the size of a resulting hash of that function. So every hash produced by this function is 256 **bit** long. *bit* is the abbreviation of ***bi**nary digi**t*** and is the basic unit for modern computer systems. Every bit can either be *0* or *1*. Since **KECCAK-256** is using 256 bit, it has **2^256** possible hashes as output for the algorithm. 

To understand how big this number is, here is a little analogy: 2^256 is about 10^168. It is estimated that the whole universe has 10^82 atoms in it. So we could hash every atom in the universe with this function and we still wouldn't have used all possilbe hashes. Therefore the probability of a collision is also unimaginably small.

Since it would take up a lot of space to display and would be hard to read a combination of 256 1s and 0s, we shorten it by using numbers and letters to display hashes. Here are some hashes, so that you know how they look like:

```
"test"  - 9c22ff5f21f0b81b113e63f7db6da94fedef11b2119b4088b89664fb9a3cb658
"Test"  - 85cc825a98ec217d960f113f5f80a95d7fd18e3725d37df428eb14f880bdfc12
"Test1" - d283f3979d00cb5493f2da07819695bc299fba34aa6e0bacb484fe07a2fc0ae0
```

As you can see, the slightest change to the input changes the whole output. Go ahead and [try it yourself](https://emn178.github.io/online-tools/keccak_256.html)!
