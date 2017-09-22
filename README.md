# An Introduction into Blockchain
I created this repository in order to explain the basics of blockchain to some friends and family. If you have any comments, if I explained something wrong or if you just want to say "Hi", just send me an email to flo.liss@gmail.com
If you want to support me, I  really appreciate donations to 0x00000
# Abbreviations
I will use the following abbreviations:

- **BC** - *Blockchain*
- **BTC** - *Bitcoin (Currency)*
- **ETH** - *Ether (Currency)*

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

# What is a block?
So now that you know what a hash is and how they are generated we can look into what a *block* is. A block basically constists of 4 things:
- A hash
- A block number
- Block data
- A nonce


I will explain each of those in detail, so don't worry :)

###### Hash
This Keccak-256 Hash is calculated by a combination of block number, block data and the nonce as input.

###### Block number
Since a BC will have a lot of blocks, we need a way to identify and distinguish them from each other. This is the block number. It starts with zero and increases by 1 block by block. Ethereum currently reached block number 4,3 million.

###### Block Data
The data part of a block is basically the information we want to store in a block. As you probably know **Bitcoin** was the first blockchain released. It is used to transfer BTC, a *digital currency*. So if **A**lice would like to send **1BTC** to **B**ob, that information would be stored in the data section of a block.

###### Nonce
*Nonce* stands for *number once used*. The block number and the data we want to store in a block are sort of fixed values. The block number always depends on the previous block and therefore can't be changed. The block data could be changed, but then we would change the information we store in the block. And we don't want to do that. So if we want to change the hash of a block, we need another variable that can get changed. This is the purpose of the nonce. Why we would want to change the hash of a block I'll explain later. For now just remember that the nonce is the part of a block that will decide, how the hash of a block looks like.

# Validating and Signing
Let's get back to **A**lice and **B**ob. As we said, **A**lice wants to send 1BTC to **B**ob and that information will be stored in a block. But how do we know if **A**lice even has 1BTC? Somebody needs to **validate** if **A**lice owns in fact 1BTC. That is what **miners** do. They iterate through every block of the blockchain and by processing all of **A**lice's transactions, how much BTC she owns. 
