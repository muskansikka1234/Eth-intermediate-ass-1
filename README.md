# Project Title

For this project, write a smart contract that implements the require(), assert() and revert() statements.

## Description

The purpose of this smart contract is to demonstrate the use of error handling mechanisms in Solidity, specifically require(), assert(), and revert(). This contract includes functions to set a value, double the value, and reset the value, incorporating these error handling statements to ensure proper functionality and security.

## Getting Started



### Executing program


// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract ErrorHandling {

    uint256 public value;

    // Modifier to check if the caller is a specific address
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    // Use of require()
    function setValue(uint256 _value) public {
        require(_value > 0, "Value must be greater than zero");
        value = _value;
    }

    // Use of assert()
    function doubleValue() public view returns (uint256) {
        uint256 doubledValue = value * 2;
        assert(doubledValue > value);
        return doubledValue;
    }

    // Use of revert()
    function resetValue() public {
        if (msg.sender != owner) {
            revert("Caller is not the owner");
        }
        value = 0;
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
