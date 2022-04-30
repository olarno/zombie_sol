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
