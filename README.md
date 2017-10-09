# An Introduction into Blockchain
I created this repository in order to explain the basics of blockchain to friends and family. If you have any comments, if I explained something wrong or if you just want to say "Hi", just send me an email to flo.liss@gmail.com

# Abbreviations
I will use the following abbreviations:

- **BC** - *Blockchain*
- **BTC** - *Bitcoin (Currency)*
- **ETH** - *Ether (Currency)*
- **PoW** - *Proof of Work*
- **PoS** - *Proof of Stake*
- **EVM** - *Ethereum Virtual Machine*

# The blockchain - A distributed database
The financial crisis of 2007–2008, also known as the global financial crisis and the 2008 financial crisis, is considered by many economists to have been the worst financial crisis since the Great Depression of the 1930s.[https://en.wikipedia.org/wiki/Financial_crisis_of_2007%E2%80%932008] The financial crisis not only ruined the lives of many people world wide it also damaged people's trust in banks. It's probably no incident that shortly after the peak of this financial crisis, an unknown man with the pseudonym *Satoshi Nakamoto* published a white paper on the first blockchain ever - **Bitcoin**. 

The protocol of Bitcoin is supposed to be a *public, decentralized and open-source* database. That means that everybody can join the system, there is no central entity -like a bank- that governs the system and the source code of the programm is publicly available. 

![Comparing a centralized and decentralized network](decentralized.png?raw=true "Comparing a centralized and decentralized network")

Since everybody in the network has the same rights and there is no central entity, everybody has its own copy of the database. Note that this means, that also everything that is stored in the blockchain is available for everyone. The common misconception that transactions on the blockchain are anonymous are thereby false. The system is rather transparent.

So let's have a look at how a blockchain works!

# What is a Hash?
Hashes are an important concept for understanding how a BC works. A hash function is a mathematical function / an algorithm that maps data of arbitrary size to data of a fixed size. So whatever we use as input for a hash function, the output will always have the same format. The output of a hash function is called a hash. 

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
So now that you know what a hash is and how they are generated we can look into what a *block* is. A block basically constists of 5 things:
- Two hashes
- A block number
- Block data
- A nonce


I will explain each of those in detail, so don't worry :)

###### Hash
There are two hashes in every block. First there is an 'old' hash that represents the value of the last block before it. The other one is calculated by a combination of the 'old' hash, block number, block data and the nonce as input. Note that this hash will serve as the 'old' hash in the next block.

###### Block number
Since a BC will build a chain of blocks, we need to know in what way they are ordered. This is the block number. It starts with zero and increments by 1 block by block. Ethereum currently reached block number 4,3 million.

###### Block Data
The data part of a block is basically the information we want to store in a block. As you probably know **Ethereum** is one of the most popular blockchains available today. It is used to transfer ETH, a *digital currency*. So if **A**lice would like to send **1ETH** to **B**ob, that information would be stored in the data section of a block.

###### Nonce
*Nonce* stands for *number once used*. The block number and the data we want to store in a block are sort of fixed values. The block number always depends on the previous block and therefore can't be changed. The block data could be changed, but then we would change the information we store in the block. And we don't want to do that. So if we want to change the hash of a block, we need another variable that can get changed. This is the purpose of the nonce. Why we would want to change the hash of a block I'll explain later. For now just remember that the nonce is the part of a block that will decide, how the hash of a block looks like.

# Validating and Signing
Let's get back to **A**lice and **B**ob. As we said, **A**lice wants to send 1ETH to **B**ob and that transaction will be stored in a block. But how do we know if **A**lice even has 1ETH? Somebody needs to **validate** if **A**lice owns in fact 1ETH. That is what **miners** do. They iterate through every block of the blockchain and by processing all of **A**lice's transactions (in- and outgoing), how much ETH she owns.

But why would anyone volunteer and do all that work? Well for every block they *mine*, they are allowed to add a transaction to that block to grant themselves a certain amount of ETH. Also, if you want your transaction to be processed faster, you can pay the miner a transaction fee to prioritize your transaction to be added to the next block.

So miners profit from validating blocks. But how do we make sure they really do their job and not verify false transactions? And who decides which miner gets the reward for a block?  Ethereum uses *Proof of Work* to solve this problem.

The Ethereum network sets requirements to the way a valid hash can look like. So for example, the requirement could be that the hash has to start with four zero's. Therefore the following hash would **not** fulfill the requirements of the blockchain:

```
c89efdaa54c0f20c7adf612882df0950f5a951637e0307cdcb4c672f298b8bc6 //hash with no 4 leading zeros
```

On the other hand, this hash would be accepted by the blockchain:
```
0000a3074287b2b33e975468ae613e023e478112530bc19d4187693c13943445 //hash with 4 leading zeros
```

But how can a miner produce a hash with four leading zeros? Do you remember nonces? We said that the nonce is the only thing in a block a miner can change. And by changing the nonce he changes the hash of that block. The miner will now put effort in finding a nonce that will result in a hash with four leading zeros. There is no formula to calculate such nonce since our hash function is *one-way*. It is only possible to find them through trial and error. Since this problem is quite hard for miners, it proofs that they took a lot of effort to find the nonce. Actually that effort is so high (and expensive) that it is not attractive for the miner to cheat anymore. The process of finding a valid nonce is also called *signing the block*.

This also solves the question, which miner is allowed to mine the block and therefore claim the reward. They basically race and who finds the fitting nonce first and shares it on the network the fastest gets the reward. Every other person in the network can easily test if the block is valid by recalculating the hash.

# The Chain and why it is (almost) impossible to cheat
You now know what a block is and how miner validate a block. Let's have a look how those blocks build a chain and how this chain prevents manipulation. We said that each block has a number to know where in the chain it is and a hash to validate it's content. That being said, here is a picture, how a block chain may look.

![A chain of blocks](blockchain.jpg?raw=true "A chain of blocks")

Let's say two miner want to add a new block to the chain. Thereby they are generating two possible branches of the blockchain. This would look like the following. 

![Miner add blocks](bcminerblock1.jpg?raw=true "Miner add blocks")

As we already said, both miners are now racing to broadcast their block to all other nodes. This is really important because currently both miners submitted a valid block and there can only be one. Otherwhise the blockchain would divide and we would have two branches with different states. Once a miner has broadcasted it's block to other nodes (miners) they will work on his copy of the blockchain. This is the reason, because there is a rule implemented in the blockchain software. The rule states, that miners should always work on the longest branch of the blockchain they know.

Since both miners are broadcasting their branch of the blockchain, there will be miners working on the blockchain of miner **A** and miners working on the blockchain of miner **B**. This will result in the following situation.

![Blockchain Branches](bcminerblocksequel.jpg?raw=true "Blockchain Branches A and B")

In this case the chain of miner **A** was faster in mining new blocks and all miners who receive this broadcasted version of the blockchain will continue to work on it. Miner **B** was *"unlucky"* and his version will be disregarded. He will receive no reward and has to continue to work on the version of miner **A**.

To make you understand why this makes cheating really hard, let's try to cheat! Let's say that **A**lice did send 1 *million* ETH to **B**ob in block #4. Back then she didn't know that ETH will be worth that much money one day. She wishes that this transaction would never have happened. She figures out that if she just mines her *own* block #4 without the transaction and broadcasts it to all other miners, they might continue to work on her branch and she would be rich. Let's have a look at how this would look like.

![Alice cheats](cheating1.jpg?raw=true "Alice cheats")

As you probably already realized, this will not work. **A**lice new BC is not the longest chain available for other miners. They will disregard the attempt to cheat.
**A**lice realizes that she needs to provide the longest chain on the network and still needs to put her block #4 in there. If she would manage to do that, the network would acknowledge her chain and her problem would be solved. 

Gladly **A**lice will most likely not be able to this. As you know, every block needs to fulfill requirements by **PoW** to be accepted. This also means that for every block **A**lice want's to add to her *cheat BC* she needs to calulate the fitting hash. Let's say the original blockchain has 500 blocks right now. That means **A**lice could copy the 3 original blocks and would have to do the **PoW** for 497 blocks to reach the same length than the original chain. But while she is doing this the rest of the network will create new blocks and make the original chain even longer. Thus making it impossible for **A**lice to ever reach a longer, validated chain than the original one. Well, **almost** impossible. If she would have more computing power than the rest of the network combined, she could in theory cheat. This is also called the **51% Attack**, since she would need to own 51% of the network's computing power.



# Wallets and Smart contracts
So **A**lice wants to send some ETH to **B**ob. But how does she or the blockchain know who **B**ob is on the network? If you have an account at a regular bank, you usually get an *IBAN (International Bank Account Number)*, that you can give to people so they know where to send money. 

With the BC it is similar. Once you joined the network you can create as many *wallets* as you like. Wallets are like bank accounts. A wallet can receive funds and the owner of the account can send funds to other wallets. Easy. Just bare in mind that since the blockchain is public, not only you but everyone can see how much money is in your wallet!
Technically, wallets are an *asymmetric crypto system*. Without going into much detail, this means you create two keys: 

-A **public key** which is like your *IBAN*. This is a key you can send to everyone without worrying. 

-A **private key** which is used to unlock your account. You can compare this to the password of your 	bank account. Only you should know this and if anyone else gets that information, well...your money is most likely gone.

Now, there is a second type of account on Ethereum. Those are called **Smart Contracts**. Smart contracts are very similar to wallets. They also have a public key where you can send transactions to. They also can store funds on them and they also can send funds to other accounts. The only difference is, that those accounts are not controlled and managed by a person with the private key, **but by computer code stored in the account**.

The computer code of smart contracts is written in **Solidity**, a programming language especially designed for Ethereum. It has a similar syntax to *JavaScript* and is thereby easy to learn if you have some experience in web development (and even if you don't **:P** ). It's most important feature and big difference to Bitcoin's scripting language is that it is *turing-complete*. *Turing completeness* means that a programming language is able to reproduce / solve every algorithmic problem possible, assuming you have enough memory / computing power.
The computer code stored in a smart contract is executed in the so called **Ethereum Virtual Machine**. The EVM is totally isolated from the environment it runs on. That means if code is executed on a miners pc, the smart contract has no access to eg. the file system of said computer.

Since Solidity is turing-complete, it is also possible to create programms that never terminate. For example one could write a programm, that increments a number by one until infinity. Since that code needs to be executed by miners in order to store the result on the blockchain that is a big problem. They can't let a programm count until infinity, that would literally take **forever ;)** 

```
//Example of a smart contract function that never terminates

pragma solidity ^0.4.0;

contract Simple {
    function infinity(uint _a) {
    	//this loop will be executed infinite times
        while(true) {
        	//increments a by one
        	_a += 1 ;
        }
    }
}
```

If a code never terminates, the miner would'nt be able to push a block to the blockchain. To solve this, smart contracts cost **gas** to execute. That means, that for every computational step a smart contract's inner logic executes, it has to pay a little fee in ETH. If a smart contract runs out of ETH to fund the execution of it's code the EVM stops the execution and returns an error.

That system is really fair. The more step a smart contract takes to execute, the more you have to pay for it to be executed.

# Proof of Work vs. Proof of Stake
Earlier I explained to you that Ethereum currently uses *PoW* to make sure miners do their job right and don't cheat. But the system of *PoW* has a lot of problems. It is really bad for the environment. The computations made to find the right nonces are completly useless after they are done. They don't serve any purpose except for the work you put into it. And still they take a lot of computing power and thereby electricy to produce. 
I couldn't find a better source right now, but [vice](https://motherboard.vice.com/en_us/article/d3zn9a/ethereum-mining-transaction-electricity-consumption-bitcoin) claims that Ethereum currently consumes as much electricity as the country of Cyprus.

###### So what is Proof of Stake?
Proof of Stake is a different approach that will be introduced to Ethereum in the coming release '*Metropolis*'. Instead of using computing power to make cheating unattractive, the miners have to give a certain amount of ETH into escrow of a smart contract called *Casper*. That means, they'll have to invest money before they are able to mine and only get their funds (and rewards) back, if their validating and signing of blocks turns out to be true.

# What are zk-SNARK's?
We earlier found out that everything we post on the blockchain is available to the public. But sometimes we don't want to share every specific detail publicly. Sometimes we want to proof that we did something over the blockchain without telling everybody how we did it. 
Let's say **A**lice works for a company that sells repacked *Magic - The Gathering* (**Robert**, this is for you ;) ) booster packs. They advertise that the cards in those repacks have a minimum value of 5$. 
**B**ob wants to buy some of those booster packs but is scepticle if they tell the truth and it is worth his money. He asks them if they can prove that the value is over 5$. Well they could tell him what cards are in the booster so he can check the price. But that would take the fun out of opening the booster packs. Otherwhise they couldn't prove it.
They would need to provide what is called a *zero-knowledge proof*. That is a proof that doesn't require to share the actual information. **zk-SNARK's** are a variant of zero-knowledge proofs. The acronym stands for *zero-knowledge Succinct Non-interactive ARgument of Knowledge*. zk-Snark's use mathematical formulas to generate a proof without disclosing the actual knowledge.
Let's use a simple example to explain how it could work. I am sure you know those 'Where's Waldo' pictures. 

![Where is Waldo?](wiw.jpg?raw=true "Try to find Waldo!")

Try to find Waldo! Now if I tell you I found Waldo but don't want to tell you where he is, would you believe me? I can prove it to you. 

![There is Waldo!](waldo.jpg?raw=true "There he is!")

Here he is. You can see, that I found him but I didn't tell you where he is so you can go and look for yourself ;)

Sadly, Ethereum currently isn't supporting zk-Snarks. But there is hope! They should be implemented during the Metropolis-Release.
