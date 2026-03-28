# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 7
- Retained Findings: 7
- Filtered Out: 0
- Total Reduction Rate: 0.00%
- False Positive Rate: 0.00%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: Sett
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Add a reentrancy guard to prevent recursive calls from exploiting state changes.

2. **Unchecked External Call**
   - Contract: Sett
   - Severity: Medium
   - Description: Unchecked External Call
   - Recommendation: Check the return value of external calls to ensure they succeed and handle any failures.

3. **Potential Integer Overflow/Underflow**
   - Contract: Sett
   - Severity: Medium
   - Description: Potential Integer Overflow/Underflow
   - Recommendation: Use SafeMath library functions to perform arithmetic operations to prevent overflows and underflows.

4. **unchecked-transfer**
   - Contract: Sett
   - Severity: High
   - Confidence: Medium
   - Line: 16
   - Description: Sett.deposit(uint256) (contracts/mocks/Sett.sol#16-19) ignores return value by token.transferFrom(msg.sender,address(this),_amount) (contracts/mocks/Sett.sol#17)

   - Recommendation: Check the return value of token transfers to ensure they are successful and handle any transfer failures.

5. **solc-version**
   - Contract: Sett
   - Severity: Informational
   - Confidence: High
   - Line: 3
   - Description: Version constraint 0.6.11 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Update the compiler version to the latest stable version to avoid known issues and vulnerabilities.

6. **naming-convention**
   - Contract: Sett
   - Severity: Informational
   - Confidence: High
   - Line: 21
   - Description: Parameter Sett.withdraw(uint256)._shares (contracts/mocks/Sett.sol#21) is not in mixedCase

   - Recommendation: Rename the parameter _shares to follow mixedCase naming conventions for better readability.

7. **immutable-states**
   - Contract: Sett
   - Severity: Optimization
   - Confidence: High
   - Line: 10
   - Description: Sett.token (contracts/mocks/Sett.sol#10) should be immutable 

   - Recommendation: Declare the token state variable as immutable to reduce gas costs by preventing reassignment.

## Unsupported Or False Positive

None
