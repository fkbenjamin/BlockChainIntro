# An Introduction into Blockchain
I created this repository in order to explain the basics of blockchain to some friends and family. If you have any comments, if I explained something wrong or if you just want to say "Hi", just send me an email to flo.liss@gmail.com
If you want to support me, I  really appreciate donations to 0x00000
# Abbreviations
I will use the following abbreviations:
BC - Blockchain
# What is a Hash?
Hashes are an important concept for understanding how a BC works. A hash function is a mathematical function/ an algorithm that maps data of arbitrary size to data of a fixed size. So whatever we use as input for a hash function, the output will always have the same format. The output of a hash function is called a hash. 

There are many types of hash functions, one of them are cryptographic hash functions. As the name states they are used in cryptography. Cryptographic hash functions have special properties. 
  1) They are deterministic. That means that a certain input will always produce the same output.
  2) They are one-way functions which means, that it is easy to calculate the output of the functions for a certain input, but it is really hard to find the input for a given output.
  3) They are supposed to be collision-free. That means that there shouldn't be two different inputs that map to the same hash.  Since there are endless possibilities of inputs and only a fixed number of possible outputs, there will always be some collisions. But modern hash functions are so sophisticated that the probability of two inputs mapping to the same hash is close to zero.
  
  
