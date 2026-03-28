# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 16
- Retained Findings: 13
- Filtered Out: 3
- Total Reduction Rate: 18.75%
- False Positive Rate: 18.75%

## Confirmed Findings

1. **Unchecked External Calls**
   - Contract: HybridPool
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Verify the success of all external calls and handle potential failures gracefully.

2. **Unprotected Function**
   - Contract: HybridPool
   - Severity: Medium
   - Description: Unprotected Function
   - Recommendation: Implement appropriate access control using modifiers to ensure only authorized users can call the function.

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: HybridPool
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Use the Checks-Effects-Interactions pattern to prevent reentrancy issues.

2. **Denial of Service (DoS)**
   - Contract: HybridPool
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Ensure that loops and external calls cannot be exploited to exhaust gas or block execution.

3. **Frontrunning**
   - Contract: HybridPool
   - Severity: Medium
   - Description: Frontrunning
   - Recommendation: Consider implementing commit-reveal schemes or transaction time locks to mitigate frontrunning.

4. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: HybridPool
   - Severity: HIGH
   - Line: 272
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Ensure calculations are based on time-weighted averages or other anti-manipulation mechanisms.

5. **divide-before-multiply**
   - Contract: HybridPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 352
   - Description: FranchisedHybridPool._computeLiquidityFromAdjustedBalances(uint256,uint256) (contracts/pool/franchised/FranchisedHybridPool.sol#352-369) performs a multiplication on the result of a division:
	- dP = (((D * D) / xp0) * D) / xp1 / 4 (contracts/pool/franchised/FranchisedHybridPool.sol#361)
	- D = (((N
   - Recommendation: Refactor the computation to minimize precision loss by multiplying first before dividing.

6. **reentrancy-no-eth**
   - Contract: HybridPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 143
   - Description: Reentrancy in HybridPool.burnSingle(bytes) (contracts/pool/HybridPool.sol#143-176):
	External calls:
	- fee = _handleFee(token0,amount0) (contracts/pool/HybridPool.sol#158)
		- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMinimal.withdraw.selector,token,address(this),to,amount,0)) (co
   - Recommendation: Lock the contract state during external calls, or use reentrancy guards to prevent reentrant calls.

7. **dead-code**
   - Contract: HybridPool
   - Severity: Informational
   - Confidence: Medium
   - Line: 404
   - Description: FranchisedHybridPool._getYD(uint256,uint256) (contracts/pool/franchised/FranchisedHybridPool.sol#404-422) is never used and should be removed

   - Recommendation: Remove unused code to reduce potential surface area for bugs and simplify maintenance.

8. **solc-version**
   - Contract: HybridPool
   - Severity: Informational
   - Confidence: High
   - Line: 3
   - Description: Version constraint >=0.8.0 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCh
   - Recommendation: Consider specifying a precise compiler version and apply patches for known issues.

9. **low-level-calls**
   - Contract: HybridPool
   - Severity: Informational
   - Confidence: High
   - Line: 282
   - Description: Low level call in FranchisedHybridPool.__balance(address) (contracts/pool/franchised/FranchisedHybridPool.sol#282-286):
	- (None,___balance) = bento.staticcall(abi.encodeWithSelector(IBentoBoxMinimal.balanceOf.selector,token,address(this))) (contracts/pool/franchised/FranchisedHybridPool.sol#284)

   - Recommendation: Avoid low-level calls unless absolutely necessary, and handle potential failures robustly.

10. **naming-convention**
   - Contract: HybridPool
   - Severity: Informational
   - Confidence: High
   - Line: 282
   - Description: Function FranchisedHybridPool.__balance(address) (contracts/pool/franchised/FranchisedHybridPool.sol#282-286) is not in mixedCase

   - Recommendation: Rename the function to follow naming conventions, e.g., `__balance` to `_balance`.

11. **unused-state**
   - Contract: HybridPool
   - Severity: Informational
   - Confidence: High
   - Line: 23
   - Description: FranchisedHybridPool.PRECISION (contracts/pool/franchised/FranchisedHybridPool.sol#23) is never used in FranchisedHybridPool (contracts/pool/franchised/FranchisedHybridPool.sol#15-470)

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: HybridPool
   - Severity: Low
   - Confidence: Medium
   - Line: 60
   - Description: FranchisedHybridPool.constructor(bytes,address)._masterDeployer (contracts/pool/franchised/FranchisedHybridPool.sol#60) lacks a zero-check on :
		- (None,_barFee) = _masterDeployer.staticcall(abi.encodeWithSelector(IMasterDeployer.barFee.selector)) (contracts/pool/franchised/FranchisedHybridPool.sol
   - Recommendation: No specific recommendation provided.

2. **reentrancy-benign**
   - Contract: HybridPool
   - Severity: Low
   - Confidence: Medium
   - Line: 122
   - Description: Reentrancy in FranchisedHybridPool.burn(bytes) (contracts/pool/franchised/FranchisedHybridPool.sol#122-146):
	External calls:
	- _transfer(token0,amount0,recipient,unwrapBento) (contracts/pool/franchised/FranchisedHybridPool.sol#133)
		- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMi
   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: HybridPool
   - Severity: Low
   - Confidence: Medium
   - Line: 122
   - Description: Reentrancy in FranchisedHybridPool.burn(bytes) (contracts/pool/franchised/FranchisedHybridPool.sol#122-146):
	External calls:
	- _transfer(token0,amount0,recipient,unwrapBento) (contracts/pool/franchised/FranchisedHybridPool.sol#133)
		- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMi
   - Recommendation: No specific recommendation provided.
