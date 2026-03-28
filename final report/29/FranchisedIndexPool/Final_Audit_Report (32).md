# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 17
- Retained Findings: 14
- Filtered Out: 3
- Total Reduction Rate: 17.65%
- False Positive Rate: 17.65%

## Confirmed Findings

1. **Incorrect Access Control**
   - Contract: FranchisedIndexPool
   - Severity: Medium
   - Description: Incorrect Access Control
   - Recommendation: Ensure that appropriate access control checks are in place for all functions. Consider using modifiers to restrict access based on roles.

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: FranchisedIndexPool
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Implement the Checks-Effects-Interactions pattern by checking state changes before making external calls. Consider using reentrancy guards.

2. **Unchecked External Calls**
   - Contract: FranchisedIndexPool
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Check the return value of external call results and handle errors appropriately. Consider using try/catch blocks where possible.

3. **Denial of Service (DoS)**
   - Contract: FranchisedIndexPool
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Refactor the contract to avoid heavy computation that could lead to gas limit exhaustion, and optimize loops with external calls.

4. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: FranchisedIndexPool
   - Severity: HIGH
   - Line: 258
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Add checks against flashloan attack patterns by ensuring token price integrity. Consider using price oracles for validation.

5. **divide-before-multiply**
   - Contract: FranchisedIndexPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 245
   - Description: FranchisedIndexPool._compute(uint256,uint256) (contracts/pool/franchised/FranchisedIndexPool.sol#245-256) performs a multiplication on the result of a division...
   - Recommendation: Reorder the mathematical operations to perform multiplication before division to minimize precision loss.

6. **reentrancy-no-eth**
   - Contract: FranchisedIndexPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 123
   - Description: Reentrancy in FranchisedIndexPool.burn(bytes) (contracts/pool/franchised/FranchisedIndexPool.sol#123-145):...
   - Recommendation: Use a reentrancy guard on functions that involve state changes and external calls to prevent reentrancy attacks.

7. **uninitialized-local**
   - Contract: FranchisedIndexPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 291
   - Description: FranchisedIndexPool._powApprox(uint256,uint256,uint256).negative (contracts/pool/franchised/FranchisedIndexPool.sol#291) is a local variable never initialized...
   - Recommendation: Initialize all local variables before usage to avoid unexpected behavior or undefined values in computations.

8. **write-after-write**
   - Contract: FranchisedIndexPool
   - Severity: Medium
   - Confidence: High
   - Line: 245
   - Description: FranchisedIndexPool._compute(uint256,uint256).output (contracts/pool/franchised/FranchisedIndexPool.sol#245) is written in both...
   - Recommendation: Refactor code to consolidate writes and ensure the latest value is properly updated without unnecessary operations.

9. **costly-loop**
   - Contract: FranchisedIndexPool
   - Severity: Informational
   - Confidence: Medium
   - Line: 61
   - Description: FranchisedIndexPool.constructor(bytes,address) (contracts/pool/franchised/FranchisedIndexPool.sol#61-95) has costly operations inside a loop...
   - Recommendation: Optimize the loop to minimize gas costs, potentially by offloading complex calculations outside of the loop.

10. **solc-version**
   - Contract: FranchisedIndexPool
   - Severity: Informational
   - Confidence: High
   - Line: 3
   - Description: Version constraint >=0.8.0 contains known severe issues...
   - Recommendation: Consider upgrading the Solidity compiler to the latest stable version and review for any critical bug fixes.

11. **low-level-calls**
   - Contract: FranchisedIndexPool
   - Severity: Informational
   - Confidence: High
   - Line: 217
   - Description: Low level call in FranchisedIndexPool.updateBarFee() (contracts/pool/franchised/FranchisedIndexPool.sol#217-220):
	- (None,_barFee) = masterDeployer.staticcall(abi.encodeWithSelector(IMasterDeployer.barFee.selector)) (contracts/pool/franchised/FranchisedIndexPool.sol#218)

   - Recommendation: No specific recommendation provided.

12. **cache-array-length**
   - Contract: FranchisedIndexPool
   - Severity: Optimization
   - Confidence: High
   - Line: 104
   - Description: Loop condition i < tokens.length (contracts/pool/franchised/FranchisedIndexPool.sol#104) should use cached array length instead of referencing `length` member of the storage array.
 
   - Recommendation: No specific recommendation provided.

13. **immutable-states**
   - Contract: FranchisedIndexPool
   - Severity: Optimization
   - Confidence: High
   - Line: 40
   - Description: FranchisedIndexPool.totalWeight (contracts/pool/franchised/FranchisedIndexPool.sol#40) should be immutable 

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: FranchisedIndexPool
   - Severity: Low
   - Confidence: Medium
   - Line: 61
   - Description: FranchisedIndexPool.constructor(bytes,address)._masterDeployer (contracts/pool/franchised/FranchisedIndexPool.sol#61) lacks a zero-check on...
   - Recommendation: No specific recommendation provided.

2. **calls-loop**
   - Contract: FranchisedIndexPool
   - Severity: Low
   - Confidence: Medium
   - Line: 332
   - Description: FranchisedIndexPool._transfer(address,uint256,address,bool) (contracts/pool/franchised/FranchisedIndexPool.sol#332-345) has external calls inside a loop...
   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: FranchisedIndexPool
   - Severity: Low
   - Confidence: Medium
   - Line: 149
   - Description: Reentrancy in FranchisedIndexPool.burnSingle(bytes) (contracts/pool/franchised/FranchisedIndexPool.sol#149-164)...
   - Recommendation: No specific recommendation provided.
