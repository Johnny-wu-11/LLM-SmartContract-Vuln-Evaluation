# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 15
- Retained Findings: 10
- Filtered Out: 5
- Total Reduction Rate: 33.33%
- False Positive Rate: 33.33%

## Confirmed Findings

1. **Unbounded Minting**
   - Contract: MockERC20
   - Severity: Medium
   - Description: Unbounded Minting
   - Recommendation: Implement a cap on minting operations to prevent unlimited token creation.

2. **Lack of Access Control for `burnFrom`**
   - Contract: MockERC20
   - Severity: Medium
   - Description: Lack of Access Control for `burnFrom`
   - Recommendation: Add authorization checks to ensure only approved addresses can call `burnFrom`.

3. **Denial of Service via `transferOwnership`**
   - Contract: MockERC20
   - Severity: Medium
   - Description: Denial of Service via `transferOwnership`
   - Recommendation: Ensure that the new owner address is valid and perform checks to avoid denial of service.

## Plausible But Unverified Findings

1. **Integer Overflow/Underflow**
   - Contract: MockERC20
   - Severity: Medium
   - Description: Integer Overflow/Underflow
   - Recommendation: Use SafeMath library to handle arithmetic operations securely.

2. **Reentrancy Vulnerability**
   - Contract: MockERC20
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Utilize the checks-effects-interactions pattern to prevent reentrancy issues.

3. **Lack of Input Validation**
   - Contract: MockERC20
   - Severity: Medium
   - Description: Lack of Input Validation
   - Recommendation: Ensure all functions validate input parameters thoroughly before use.

4. **dead-code**
   - Contract: MockERC20
   - Severity: Informational
   - Confidence: Medium
   - Line: 64
   - Description: MockERC20._push(address,uint256) (contracts/mock/MockERC20.sol#64-66) is never used and should be removed

   - Recommendation: Remove any code that is not used to improve readability and maintainability.

5. **solc-version**
   - Contract: MockERC20
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint 0.6.12 contains known severe issues...
   - Recommendation: Upgrade the Solidity compiler version to the latest stable release to mitigate known bugs.

6. **naming-convention**
   - Contract: MockERC20
   - Severity: Informational
   - Confidence: High
   - Line: 17
   - Description: Modifier MockERC20._onlyOwner_() (contracts/mock/MockERC20.sol#17-20) is not in mixedCase

   - Recommendation: Rename modifiers and variables to use mixedCase for consistency with Solidity naming conventions.

7. **immutable-states**
   - Contract: MockERC20
   - Severity: Optimization
   - Confidence: High
   - Line: 8
   - Description: MockERC20._decimals (contracts/mock/MockERC20.sol#8) should be immutable 

   - Recommendation: Declare `_decimals` as immutable to optimize storage and gas usage.

## Unsupported Or False Positive

1. **shadowing-local**
   - Contract: MockERC20
   - Severity: Low
   - Confidence: High
   - Line: 37
   - Description: MockERC20.constructor(string,string,uint8).decimals (contracts/mock/MockERC20.sol#37) shadows:
	- MockERC20.decimals() (contracts/mock/MockERC20.sol#53-55) (function)

   - Recommendation: No specific recommendation provided.

2. **events-access**
   - Contract: MockERC20
   - Severity: Low
   - Confidence: Medium
   - Line: 139
   - Description: MockERC20.transferOwnership(address) (contracts/mock/MockERC20.sol#139-141) should emit an event for: 
	- _owner = newOwner (contracts/mock/MockERC20.sol#140) 

   - Recommendation: No specific recommendation provided.

3. **missing-zero-check**
   - Contract: MockERC20
   - Severity: Low
   - Confidence: Medium
   - Line: 139
   - Description: MockERC20.transferOwnership(address).newOwner (contracts/mock/MockERC20.sol#139) lacks a zero-check on :
		- _owner = newOwner (contracts/mock/MockERC20.sol#140)

   - Recommendation: No specific recommendation provided.

4. **reentrancy-benign**
   - Contract: MockERC20
   - Severity: Low
   - Confidence: Medium
   - Line: 43
   - Description: Reentrancy in MockFlamIncomeVault.deposit(uint256) (contracts/mock/MockFlamIncome.sol#43-56):
	External calls:
	- token.safeTransferFrom(msg.sender,address(this),_amount) (contracts/mock/MockFlamIncome.sol#46)
	State variables written after the call(s):
	- _mint(msg.sender,shares) (contracts/mock/Mo
   - Recommendation: No specific recommendation provided.

5. **reentrancy-events**
   - Contract: MockERC20
   - Severity: Low
   - Confidence: Medium
   - Line: 30
   - Description: Reentrancy in MockPickleJar.deposit(uint256) (contracts/mock/MockPickleJar.sol#30-34):
	External calls:
	- t3crv.transferFrom(msg.sender,address(this),_amount) (contracts/mock/MockPickleJar.sol#31)
	Event emitted after the call(s):
	- Transfer(address(0),dst,amt) (contracts/mock/MockERC20.sol#75)
		
   - Recommendation: No specific recommendation provided.
