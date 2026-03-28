# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 17
- Retained Findings: 14
- Filtered Out: 3
- Total Reduction Rate: 17.65%
- False Positive Rate: 17.65%

## Confirmed Findings

1. **Access Control**
   - Contract: IndexPool
   - Severity: Medium
   - Description: Access Control
   - Recommendation: Implement role-based access control on all sensitive functions to ensure only authorized addresses can execute them.

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: IndexPool
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Use a reentrancy guard to prevent multiple invocations of vulnerable functions within the same transaction.

2. **Unchecked External Call**
   - Contract: IndexPool
   - Severity: Medium
   - Description: Unchecked External Call
   - Recommendation: Check the success of external calls and handle any errors or revert if the call fails.

3. **Denial of Service (DoS)**
   - Contract: IndexPool
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Limit gas consumption and optimize operations in critical functions to avoid potential DoS attacks.

4. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: IndexPool
   - Severity: HIGH
   - Line: 258
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Implement validation and sanity checks on token price calculations to prevent manipulation.

5. **divide-before-multiply**
   - Contract: IndexPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 245
   - Description: FranchisedIndexPool._compute(uint256,uint256) performs a multiplication on the result of a division.
   - Recommendation: Reorder operations to multiply before dividing where possible to minimize precision loss.

6. **reentrancy-no-eth**
   - Contract: IndexPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 120
   - Description: Reentrancy in IndexPool.burn(bytes).
   - Recommendation: Deploy a checks-effects-interactions pattern to prevent state changes after external calls.

7. **uninitialized-local**
   - Contract: IndexPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 298
   - Description: IndexPool._powApprox(uint256,uint256,uint256).negative is a local variable never initialized.
   - Recommendation: Ensure all local variables are initialized before use to prevent unexpected behavior.

8. **write-after-write**
   - Contract: IndexPool
   - Severity: Medium
   - Confidence: High
   - Line: 255
   - Description: IndexPool._compute(uint256,uint256).output is written in both output = wholePow and output = _mul(wholePow,partialResult).
   - Recommendation: Refactor the function to avoid overwriting variables within a single execution path.

9. **costly-loop**
   - Contract: IndexPool
   - Severity: Informational
   - Confidence: Medium
   - Line: 61
   - Description: FranchisedIndexPool.constructor(bytes,address) has costly operations inside a loop.
   - Recommendation: Consider caching immutable data outside the loop to reduce processing time.

10. **solc-version**
   - Contract: IndexPool
   - Severity: Informational
   - Confidence: High
   - Line: 3
   - Description: Version constraint >=0.8.0 contains known severe issues.
   - Recommendation: Upgrade to a newer, patched version of Solidity that addresses these issues.

11. **low-level-calls**
   - Contract: IndexPool
   - Severity: Informational
   - Confidence: High
   - Line: 217
   - Description: Low level call in FranchisedIndexPool.updateBarFee() (contracts/pool/franchised/FranchisedIndexPool.sol#217-220):
	- (None,_barFee) = masterDeployer.staticcall(abi.encodeWithSelector(IMasterDeployer.barFee.selector)) (contracts/pool/franchised/FranchisedIndexPool.sol#218)

   - Recommendation: No specific recommendation provided.

12. **cache-array-length**
   - Contract: IndexPool
   - Severity: Optimization
   - Confidence: High
   - Line: 104
   - Description: Loop condition i < tokens.length (contracts/pool/franchised/FranchisedIndexPool.sol#104) should use cached array length instead of referencing `length` member of the storage array.
 
   - Recommendation: No specific recommendation provided.

13. **immutable-states**
   - Contract: IndexPool
   - Severity: Optimization
   - Confidence: High
   - Line: 40
   - Description: IndexPool.totalWeight (contracts/pool/IndexPool.sol#40) should be immutable 

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: IndexPool
   - Severity: Low
   - Confidence: Medium
   - Line: 61
   - Description: FranchisedIndexPool.constructor lacks a zero-check on _masterDeployer.
   - Recommendation: No specific recommendation provided.

2. **calls-loop**
   - Contract: IndexPool
   - Severity: Low
   - Confidence: Medium
   - Line: 332
   - Description: FranchisedIndexPool._transfer has external calls inside a loop.
   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: IndexPool
   - Severity: Low
   - Confidence: Medium
   - Line: 149
   - Description: Reentrancy in FranchisedIndexPool.burnSingle.
   - Recommendation: No specific recommendation provided.
