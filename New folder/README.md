# function-and-errors

FUNCTIONS AND ERRORS
This assessment tackles the require, assert and the revert in Module 1 of Avalanche in Metacraters.

# DESCRIPTION
Require is a term for a requirement that must be fulfilled for the function to proceed. If the condition evaluates to false, the function will rerun with all state alterations made during the execution undone. Assert: This verb is used to look for circumstances that don't have to be evaluated as false. It is usually used to look for internal problems or static circumstances. To reverse the current transaction and display an optional error message, use the "Revert" command.

# GETTING STARTED
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a functionanderrors.sol extension (e.g., functionanderrors.sol). Copy and paste the following code into the file:

// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;

//import "hardhat/console.sol";

contract Bmcdo {
    address payable public owner;
    uint256 public balance;

    event Deposit(uint256 amount);
    event Withdraw(uint256 amount);

    constructor(uint initBalance) payable {
        owner = payable(msg.sender);
        balance = initBalance;
    }

    function getBalance() public view returns(uint256){
        return balance;
    }

    function deposit(uint256 _amount) public payable {
        uint _previousBalance = balance;

        // make sure this is the owner
        require(msg.sender == owner, "You are not the owner of this account");

        // perform transaction
        balance += _amount;

        // assert transaction completed successfully
        assert(balance == _previousBalance + _amount);

        // emit the event
        emit Deposit(_amount);
    }

    // custom error
    error InsufficientBalance(uint256 balance, uint256 withdrawAmount);

    function withdraw(uint256 _withdrawAmount) public {
        require(msg.sender == owner, "You are not the owner of this account");
        uint _previousBalance = balance;
        if (balance < _withdrawAmount) {
            revert InsufficientBalance({
                balance: balance,
                withdrawAmount: _withdrawAmount
            });
        }

        // withdraw the given amount
        balance -= _withdrawAmount;

        // assert the balance is correct
        assert(balance == (_previousBalance - _withdrawAmount));

        // emit the event
        emit Withdraw(_withdrawAmount);
    }
}


# AUTHOR
Alcantara, John Benedict G. Bsit 3.1
