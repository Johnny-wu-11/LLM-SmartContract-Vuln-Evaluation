# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 20
- Retained Findings: 17
- Filtered Out: 3
- Total Reduction Rate: 15.00%
- False Positive Rate: 15.00%

## Confirmed Findings

1. **Governance Functions**
   - Contract: MetaVault
   - Severity: Medium
   - Description: Governance Functions
   - Recommendation: Ensure that access to governance functions is strictly controlled with proper role-based access control checks.

2. **Reentrancy Vulnerability**
   - Contract: MetaVault
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Use reentrancy guards such as OpenZeppelin's ReentrancyGuard to prevent nested calls to functions.

3. **Denial of Service (DoS)**
   - Contract: MetaVault
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Audit all loops and external calls to ensure they are limited or aggregated to prevent resource exhaustion.

4. **Integer Overflow/Underflow**
   - Contract: MetaVault
   - Severity: Medium
   - Description: Integer Overflow/Underflow
   - Recommendation: Use SafeMath or Solidity version 0.8.x or higher which incorporates safe arithmetic by default.

5. **Bad Randomness**
   - Contract: MetaVault
   - Severity: Medium
   - Description: Bad Randomness
   - Recommendation: Avoid relying on block variables for randomness; consider using Chainlink VRF for provably fair random numbers.

## Plausible But Unverified Findings

1. **Unchecked External Calls**
   - Contract: MetaVault
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Check the return values of all external calls and handle failures appropriately.

2. **Frontrunning**
   - Contract: MetaVault
   - Severity: Medium
   - Description: Frontrunning
   - Recommendation: Implement commit-reveal schemes or other cryptographic techniques to mitigate price manipulation risks.

3. **Timestamp Dependence**
   - Contract: MetaVault
   - Severity: Medium
   - Description: Timestamp Dependence
   - Recommendation: Avoid using block.timestamp for critical logic. Consider block.number for more predictable future conditions.

4. **unchecked-transfer**
   - Contract: MetaVault
   - Severity: High
   - Confidence: Medium
   - Line: 572
   - Description: MetaVault.unstake(uint256) ignores return value by IERC20(address(this)).transfer(msg.sender,_amount)
   - Recommendation: Check the return value of ERC20 transfer calls to handle failure scenarios and revert if necessary.

5. **divide-before-multiply**
   - Contract: MetaVault
   - Severity: Medium
   - Confidence: Medium
   - Line: 591
   - Description: MetaVault.withdraw performs a multiplication on the result of a division
   - Recommendation: Reorder operations to multiply before division to avoid loss of precision.

6. **incorrect-equality**
   - Contract: MetaVault
   - Severity: Medium
   - Confidence: High
   - Line: 523
   - Description: MetaVault.updateReward uses a dangerous strict equality
   - Recommendation: Consider using a greater-than condition or handle the zero state separately.

7. **reentrancy-no-eth**
   - Contract: MetaVault
   - Severity: Medium
   - Confidence: Medium
   - Line: 300
   - Description: Reentrancy in MetaVault.claimInsurance
   - Recommendation: Use checks-effects-interactions pattern and apply reentrancy guard to prevent vulnerabilities.

8. **unused-return**
   - Contract: MetaVault
   - Severity: Medium
   - Confidence: Medium
   - Line: 664
   - Description: MetaVault.earnExtra ignores return value by converter.convert()
   - Recommendation: Validate and check all return values of important functions to ensure correct execution.

9. **solc-version**
   - Contract: MetaVault
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint 0.6.12 contains known severe issues
   - Recommendation: Upgrade to the latest stable version of Solidity to avoid known bugs and security issues.

10. **naming-convention**
   - Contract: MetaVault
   - Severity: Informational
   - Confidence: High
   - Line: 138
   - Description: Parameter not in mixedCase
   - Recommendation: Rename parameters and variables to use mixedCase as per the Solidity naming conventions.

11. **too-many-digits**
   - Contract: MetaVault
   - Severity: Informational
   - Confidence: Medium
   - Line: 25
   - Description: MetaVault.slitherConstructorVariables() (contracts/legacy/MetaVault.sol#25-673) uses literals with too many digits:
	- totalDepositCap = 10000000000000000000000000 (contracts/legacy/MetaVault.sol#39)

   - Recommendation: No specific recommendation provided.

12. **immutable-states**
   - Contract: MetaVault
   - Severity: Optimization
   - Confidence: High
   - Line: 32
   - Description: MetaVault.token3CRV (contracts/legacy/MetaVault.sol#32) should be immutable 

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **events-maths**
   - Contract: MetaVault
   - Severity: Low
   - Confidence: Medium
   - Line: 138
   - Description: MetaVault.setMin should emit an event
   - Recommendation: No specific recommendation provided.

2. **missing-zero-check**
   - Contract: MetaVault
   - Severity: Low
   - Confidence: Medium
   - Line: 156
   - Description: MetaVault.setController lacks a zero-check
   - Recommendation: No specific recommendation provided.

3. **calls-loop**
   - Contract: MetaVault
   - Severity: Low
   - Confidence: Medium
   - Line: 422
   - Description: External calls inside a loop in MetaVault.depositAll
   - Recommendation: No specific recommendation provided.
