# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 13
- Retained Findings: 11
- Filtered Out: 2
- Total Reduction Rate: 15.38%
- False Positive Rate: 15.38%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Integer Overflow/Underflow Risk**
   - Contract: MockPickleJar
   - Severity: Medium
   - Description: Integer Overflow/Underflow Risk
   - Recommendation: Use SafeMath library to handle arithmetic operations securely and prevent overflow or underflow.

2. **Denial of Service (DoS) Risk**
   - Contract: MockPickleJar
   - Severity: Medium
   - Description: Denial of Service (DoS) Risk
   - Recommendation: Implement proper input validation and error handling to restrict possible DoS attack vectors.

3. **Lack of Access Control**
   - Contract: MockPickleJar
   - Severity: Medium
   - Description: Lack of Access Control
   - Recommendation: Implement role-based access control using OpenZeppelin's Ownable or AccessControl to secure critical functions.

4. **Potential Reentrancy Attack**
   - Contract: MockPickleJar
   - Severity: Medium
   - Description: Potential Reentrancy Attack
   - Recommendation: Use the Checks-Effects-Interactions pattern and consider using ReentrancyGuard from OpenZeppelin to prevent reentrancy.

5. **unchecked-transfer**
   - Contract: MockPickleJar
   - Severity: High
   - Confidence: Medium
   - Line: 30
   - Description: MockPickleJar.deposit(uint256) (contracts/mock/MockPickleJar.sol#30-34) ignores return value by t3crv.transferFrom(msg.sender,address(this),_amount) (contracts/mock/MockPickleJar.sol#31)

   - Recommendation: Check the return value of the transferFrom call to ensure the transfer was successful and handle failures appropriately.

6. **solc-version**
   - Contract: MockPickleJar
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint 0.6.12 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Upgrade to a more recent Solidity version that does not have known severe issues.

7. **missing-inheritance**
   - Contract: MockPickleJar
   - Severity: Informational
   - Confidence: High
   - Line: 10
   - Description: MockPickleJar (contracts/mock/MockPickleJar.sol#10-49) should inherit from PickleJar (contracts/interfaces/PickleJar.sol#5-14)

   - Recommendation: Ensure MockPickleJar correctly inherits from PickleJar to maintain its intended interface and behavior.

8. **naming-convention**
   - Contract: MockPickleJar
   - Severity: Informational
   - Confidence: High
   - Line: 30
   - Description: Parameter MockPickleJar.deposit(uint256)._amount (contracts/mock/MockPickleJar.sol#30) is not in mixedCase

   - Recommendation: Rename the parameter _amount to use mixedCase to adhere to naming conventions.

9. **too-many-digits**
   - Contract: MockPickleJar
   - Severity: Informational
   - Confidence: Medium
   - Line: 40
   - Description: MockPickleJar.withdraw(uint256) (contracts/mock/MockPickleJar.sol#40-44) uses literals with too many digits:
	- r = _shares * getRatio() / 1000000000000000000 (contracts/mock/MockPickleJar.sol#41)

   - Recommendation: Consider defining large constants separately to improve readability and maintainability.

10. **constable-states**
   - Contract: MockPickleJar
   - Severity: Optimization
   - Confidence: High
   - Line: 12
   - Description: MockPickleJar.lpToken (contracts/mock/MockPickleJar.sol#12) should be constant 

   - Recommendation: Declare the lpToken variable as constant to save gas by preventing storage reads at runtime.

11. **immutable-states**
   - Contract: MockPickleJar
   - Severity: Optimization
   - Confidence: High
   - Line: 11
   - Description: MockPickleJar.t3crv (contracts/mock/MockPickleJar.sol#11) should be immutable 

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **reentrancy-benign**
   - Contract: MockPickleJar
   - Severity: Low
   - Confidence: Medium
   - Line: 30
   - Description: Reentrancy in MockPickleJar.deposit(uint256) (contracts/mock/MockPickleJar.sol#30-34):
	External calls:
	- t3crv.transferFrom(msg.sender,address(this),_amount) (contracts/mock/MockPickleJar.sol#31)
	State variables written after the call(s):
	- _mint(msg.sender,shares) (contracts/mock/MockPickleJar.
   - Recommendation: No specific recommendation provided.

2. **reentrancy-events**
   - Contract: MockPickleJar
   - Severity: Low
   - Confidence: Medium
   - Line: 30
   - Description: Reentrancy in MockPickleJar.deposit(uint256) (contracts/mock/MockPickleJar.sol#30-34):
	External calls:
	- t3crv.transferFrom(msg.sender,address(this),_amount) (contracts/mock/MockPickleJar.sol#31)
	Event emitted after the call(s):
	- Transfer(address(0),dst,amt) (contracts/mock/MockERC20.sol#75)
		
   - Recommendation: No specific recommendation provided.
