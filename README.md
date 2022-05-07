# zombie_sol  
## Solidity path : Beginner to intermediate Smart contract  
api (cryptoKitties) : https://api.cryptokitties.co/kitties/  
Library :  
- OpenZeppelin is a library of secure and community-vetted smart contracts that you can use in your own DApps. After this lesson, we highly recommend you check out their site to further your learning!  

## Gas notion  

In Solidity, your users have to pay every time they execute a function on your DApp using a currency called gas. Users buy gas with Ether (the currency on Ethereum), so your users have to spend ETH in order to execute functions on your DApp.

How much gas is required to execute a function depends on how complex that function's logic is. Each individual operation has a gas cost based roughly on how much computing resources will be required to perform that operation (e.g. writing to storage is much more expensive than adding two integers). The total gas cost of your function is the sum of the gas costs of all its individual operations.

Because running functions costs real money for your users, code optimization is much more important in Ethereum than in other programming languages. If your code is sloppy, your users are going to have to pay a premium to execute your functions — and this could add up to millions of dollars in unnecessary fees across thousands of users.

32 bits is more than enough to hold the zombie's level and timestamp, so this will save us some gas costs by packing the data more tightly than using a regular uint (256-bits).

## Let's recap  

- We've added a way to update our CryptoKitties contracts  
- We've learned to protect core functions with onlyOwner  
- We've learned about gas and gas optimization  
- We added levels and cooldowns to our zombies  
- We now have functions to update a zombie's name and DNA once the zombie gets above a certain level  
- And finally, we now have a function to return a user's zombie army  

Up until now, we've covered quite a few function modifiers. It can be difficult to try to remember everything, so let's run through a quick review:

We have visibility modifiers that control when and where the function can be called from: private means it's only callable from other functions inside the contract; internal is like private but can also be called by contracts that inherit from this one; external can only be called outside the contract; and finally public can be called anywhere, both internally and externally.

We also have state modifiers, which tell us how the function interacts with the BlockChain: view tells us that by running the function, no data will be saved/changed. pure tells us that not only does the function not save any data to the blockchain, but it also doesn't read any data from the blockchain. Both of these don't cost any gas to call if they're called externally from outside the contract (but they do cost gas if called internally by another function).

Then we have custom modifiers, which we learned about in Lesson 3: onlyOwner and aboveLevel, for example. For these we can define custom logic to determine how they affect a function.

These modifiers can all be stacked together on a function definition as follows:

```function test() external view onlyOwner anotherModifier { /* ... */ }```

## Zombie battle flow  

- You choose one of your zombies, and choose an opponent's zombie to attack.  
- If you're the attacking zombie, you will have a 70% chance of winning. The defending zombie will have a 30% chance of winning.  
- All zombies (attacking and defending) will have a winCount and a lossCount that will increment depending on the outcome of the battle.  
- If the attacking zombie wins, it levels up and spawns a new zombie.  
- If it loses, nothing happens (except its lossCount incrementing).  
- Whether it wins or loses, the attacking zombie's cooldown time will be triggered.  
## web3  

``npm install web3``

*Infura* [https://infura.io/] is a service that maintains a set of Ethereum nodes with a caching layer for fast reads, which you can access for free through their API. Using Infura as a provider, you can reliably send and receive messages to/from the Ethereum blockchain without needing to set up and maintain your own node.  

*Metamask* [https://metamask.io/] is a browser extension for Chrome and Firefox that lets users securely manage their Ethereum accounts and private keys, and use these accounts to interact with websites that are using Web3.js. (If you haven't used it before, you'll definitely want to go and install it — then your browser is Web3 enabled, and you can now interact with any website that communicates with the Ethereum blockchain!).

*Contract Address*  
After you finish writing your smart contract, you will compile it and deploy it to Ethereum. We're going to cover deployment in the next lesson, but since that's quite a different process from writing code, we've decided to go out of order and cover Web3.js first.

*Contract ABI*  
The other thing Web3.js will need to talk to your contract is its ABI.  
ABI stands for Application Binary Interface. Basically it's a representation of your contracts' methods in JSON format that tells Web3.js how to format function calls in a way your contract will understand.  
When you compile your contract to deploy to Ethereum (which we'll cover in Lesson 7), the Solidity compiler will give you the ABI, so you'll need to copy and save this in addition to the contract address.  

*Call*  
call is used for view and pure functions. It only runs on the local node, and won't create a transaction on the blockchain.  
Using Web3.js, you would call a function named myMethod with the parameter 123 as follows:  
``myContract.methods.myMethod(123).call()``

*Send*  
send will create a transaction and change data on the blockchain. You'll need to use send for any functions that aren't view or pure.  
Using Web3.js, you would send a transaction calling a function named myMethod with the parameter 123 as follows:  
``myContract.methods.myMethod(123).send()``  

*What's a Wei?*
A wei is the smallest sub-unit of Ether — there are 10^18 wei in one ether.  
That's a lot of zeroes to count — but luckily Web3.js has a conversion utility that does this for us.
``web3js.utils.toWei("1");`` 