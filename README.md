# Project Title

For this project, write a smart contract that implements the require(), assert() and revert() statements.

## Description

The purpose of this smart contract is to demonstrate the use of error handling mechanisms in Solidity, specifically require(), assert(), and revert(). This contract includes functions to set a value, double the value, and reset the value, incorporating these error handling statements to ensure proper functionality and security.

## Getting Started



### Executing program


// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Bank {
    mapping(address => uint256) private balances;
    address[] private accounts;
    
    // Event for making deposits
    event Deposit(address indexed account, uint256 amount);
    
    // Event for making withdrawals
    event Withdrawal(address indexed account, uint256 amount);

    // Function to deposit 
    function deposit() external payable {
        require(msg.value > 0, "Deposit amount must be greater than zero");
        
        // If this is a new account, add it to the accounts array
        if (balances[msg.sender] == 0) {
            accounts.push(msg.sender);
        }
        
        balances[msg.sender] += msg.value;
        emit Deposit(msg.sender, msg.value);
    }
    
    // Function to withdraw
    function withdraw(uint256 amount) external {
        require(amount > 0, "Withdrawal amount must be greater than zero");
        require(balances[msg.sender] >= amount, "Insufficient balance");
        
        balances[msg.sender] -= amount;
        payable(msg.sender).transfer(amount);
        emit Withdrawal(msg.sender, amount);
    }
    
    // Function to check the balance 
    function checkBalance() external view returns (uint256) {
        return balances[msg.sender];
    }

    // Function to demonstrate assert
    function checkInvariant() external view {
        // This is a hypothetical invariant check, which should always hold true
        uint256 totalBalance = address(this).balance;
        
        // Iterating through all accounts to calculate the sum of balances
        uint256 sumBalances = 0;
        for (uint i = 0; i < accounts.length; i++) {
            sumBalances += balances[accounts[i]];
        }
        
        // The total balance of the contract should equal the sum of all individual balances
        assert(totalBalance == sumBalances); // This condition should always be true
    }

    // Function to demonstrate revert
    function demoRevert(uint256 amount) external pure {
        if (amount == 0) {
            revert("Amount cannot be zero");
        }
       
    }
}


## Help

High Gas Consumption: Writing complex logic in a single transaction can lead to high gas costs, potentially causing the transaction to fail.

## Authors

Contributors names and contact info

Muskan Sikka 
muskansikka1234@gmail.com


## License

This project is licensed under the SPDX-License-Identifier:MIT
