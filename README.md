# Transient-Storage-Example
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract TransientStorageExample {
    // Transient storage (tstore/tload) - gas efficient temporary storage
    function temporaryCalculation(uint256 input) public returns (uint256) {
        uint256 tempResult;
        assembly {
            tstore(0, input)                    // Store in transient slot 0
            tempResult := mul(tload(0), 2)      // Read and calculate
            tstore(0, 0)                        // Clear transient storage
        }
        return tempResult;
    }
}
