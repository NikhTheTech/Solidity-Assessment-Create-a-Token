# MyToken Contract

This Solidity smart contract provides a basic implementation of a token with functionalities for minting and burning tokens. The contract includes public variables for token details and functions to manage token supply and balances.

## Features

- Mint new tokens to a specified address.
- Burn tokens from a specified address, with conditions to ensure sufficient balance.
- Track token details such as name, abbreviation, and total supply.

## Contract Details

- **Token Name**: NikhTheTech
- **Token Abbreviation**: NTT
- **Total Supply**: Public variable to store the total supply of tokens.

## Functions

### `mint(address _cosmos, uint _value)`

This function allows the minting of new tokens. It increases the total supply by the specified value and adds this value to the balance of the specified address.

- **Parameters**:
  - `_cosmos`: The address receiving the minted tokens.
  - `_value`: The number of tokens to mint.

### `burn(address _blackhole, uint _value)`

This function allows tokens to be burned. It deducts the specified value from the total supply and the balance of the specified address. The function includes a conditional check to ensure that the balance of the address is greater than or equal to the amount to be burned.

- **Parameters**:
  - `_blackhole`: The address from which tokens will be burned.
  - `_value`: The number of tokens to burn.

## Solidity Version

This contract is written in Solidity version 0.8.18.

## Requirements

1. The contract includes public variables to store token details.
2. It uses a mapping from addresses to balances.
3. The mint function allows minting tokens, increasing both total supply and the balance of the specified address.
4. The burn function allows burning tokens, with conditions to ensure the sender has a sufficient balance.
5. The burn function includes checks to ensure the sender's balance is adequate for the amount to be burned.

## Usage

To interact with this contract, you can deploy it on an Ethereum-compatible blockchain and use web3.js or ethers.js to call the functions:

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

/*
       REQUIREMENTS
    1. Your contract will have public variables that store the details about your coin (Token Name, Token Abbrv., Total Supply)
    2. Your contract will have a mapping of addresses to balances (address => uint)
    3. You will have a mint function that takes two parameters: an address and a value. 
       The function then increases the total supply by that number and increases the balance 
       of the “sender” address by that amount
    4. Your contract will have a burn function, which works the opposite of the mint function, as it will destroy tokens. 
       It will take an address and value just like the mint functions. It will then deduct the value from the total supply 
       and from the balance of the “sender”.
    5. Lastly, your burn function should have conditionals to make sure the balance of "sender" is greater than or equal 
       to the amount that is supposed to be burned.
*/

contract MyToken {

    // public variables here
    string public Token_Name = "NikhTheTech";
    string public Token_Abbrv = "NTT";
    uint public Total_Supply;

    // mapping variable here
    mapping(address => uint) public balance;

    // mint function
    function mint(address _cosmos, uint _value) public {
        Total_Supply += _value;
        balance[_cosmos] += _value;
    }

    // burn function
     function burn(address _blackhole, uint _value) public {
        if(balance[_blackhole] >= _value){
        Total_Supply -= _value;
        balance[_blackhole] -= _value;
        }
    }
}
