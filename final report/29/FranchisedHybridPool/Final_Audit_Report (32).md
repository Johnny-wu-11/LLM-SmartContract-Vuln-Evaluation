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
   - Contract: FranchisedHybridPool
   - Severity: Medium
   - Description: Access Control
   - Recommendation: Implement role-based access control using OpenZeppelin's AccessControl library to enforce permissions for sensitive functions.

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: FranchisedHybridPool
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Consider using ReentrancyGuard from OpenZeppelin to prevent reentrant calls to sensitive functions.

2. **Unchecked External Calls**
   - Contract: FranchisedHybridPool
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Check the return value of all external calls and use pattern like Checks-Effects-Interactions to mitigate risks.

3. **Denial of Service (DoS)**
   - Contract: FranchisedHybridPool
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Ensure that all loop iterations and external calls can handle large data inputs and have gas limits.

4. **Integer Overflow/Underflow**
   - Contract: FranchisedHybridPool
   - Severity: Medium
   - Description: Integer Overflow/Underflow
   - Recommendation: Use SafeMath library to perform arithmetic operations securely and prevent overflow/underflow.

5. **Potential Front-Running**
   - Contract: FranchisedHybridPool
   - Severity: Medium
   - Description: Potential Front-Running
   - Recommendation: Implement mechanisms such as commit-reveal schemes or nonce-based systems to mitigate front-running.

6. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: FranchisedHybridPool
   - Severity: HIGH
   - Line: 187
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Use chainlink oracles to fetch token prices securely and make sure calculations are resistant to manipulation.

7. **divide-before-multiply**
   - Contract: FranchisedHybridPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 352
   - Description: FranchisedHybridPool._computeLiquidityFromAdjustedBalances(uint256,uint256) (contracts/pool/franchised/FranchisedHybridPool.sol#352-369) performs a multiplication on the result of a division:
	- dP = (((D * D) / xp0) * D) / xp1 / 4 (contracts/pool/franchised/FranchisedHybridPool.sol#361)
	- D = (((N
   - Recommendation: Refactor to multiply before dividing to maintain precision and reduce rounding errors.

8. **reentrancy-no-eth**
   - Contract: FranchisedHybridPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 150
   - Description: Reentrancy in FranchisedHybridPool.burnSingle(bytes) (contracts/pool/franchised/FranchisedHybridPool.sol#150-184):
	External calls:
	- fee = _handleFee(token0,amount0) (contracts/pool/franchised/FranchisedHybridPool.sol#166)
		- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMinimal.wit
   - Recommendation: Enforce the Checks-Effects-Interactions pattern by updating balance before making external calls.

9. **dead-code**
   - Contract: FranchisedHybridPool
   - Severity: Informational
   - Confidence: Medium
   - Line: 404
   - Description: FranchisedHybridPool._getYD(uint256,uint256) (contracts/pool/franchised/FranchisedHybridPool.sol#404-422) is never used and should be removed

   - Recommendation: Remove the unused function to improve code readability and maintainability.

10. **solc-version**
   - Contract: FranchisedHybridPool
   - Severity: Informational
   - Confidence: High
   - Line: 3
   - Description: Version constraint >=0.8.0 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCh
   - Recommendation: Upgrade the Solidity compiler to the latest stable version to avoid known bugs and security issues.

11. **low-level-calls**
   - Contract: FranchisedHybridPool
   - Severity: Informational
   - Confidence: High
   - Line: 282
   - Description: Low level call in FranchisedHybridPool.__balance(address) (contracts/pool/franchised/FranchisedHybridPool.sol#282-286):
	- (None,___balance) = bento.staticcall(abi.encodeWithSelector(IBentoBoxMinimal.balanceOf.selector,token,address(this))) (contracts/pool/franchised/FranchisedHybridPool.sol#284)

   - Recommendation: No specific recommendation provided.

12. **naming-convention**
   - Contract: FranchisedHybridPool
   - Severity: Informational
   - Confidence: High
   - Line: 282
   - Description: Function FranchisedHybridPool.__balance(address) (contracts/pool/franchised/FranchisedHybridPool.sol#282-286) is not in mixedCase

   - Recommendation: No specific recommendation provided.

13. **unused-state**
   - Contract: FranchisedHybridPool
   - Severity: Informational
   - Confidence: High
   - Line: 23
   - Description: FranchisedHybridPool.PRECISION (contracts/pool/franchised/FranchisedHybridPool.sol#23) is never used in FranchisedHybridPool (contracts/pool/franchised/FranchisedHybridPool.sol#15-470)

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: FranchisedHybridPool
   - Severity: Low
   - Confidence: Medium
   - Line: 60
   - Description: FranchisedHybridPool.constructor(bytes,address)._masterDeployer (contracts/pool/franchised/FranchisedHybridPool.sol#60) lacks a zero-check on :
		- (None,_barFee) = _masterDeployer.staticcall(abi.encodeWithSelector(IMasterDeployer.barFee.selector)) (contracts/pool/franchised/FranchisedHybridPool.sol
   - Recommendation: No specific recommendation provided.

2. **reentrancy-benign**
   - Contract: FranchisedHybridPool
   - Severity: Low
   - Confidence: Medium
   - Line: 122
   - Description: Reentrancy in FranchisedHybridPool.burn(bytes) (contracts/pool/franchised/FranchisedHybridPool.sol#122-146):
	External calls:
	- _transfer(token0,amount0,recipient,unwrapBento) (contracts/pool/franchised/FranchisedHybridPool.sol#133)
		- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMi
   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: FranchisedHybridPool
   - Severity: Low
   - Confidence: Medium
   - Line: 122
   - Description: Reentrancy in FranchisedHybridPool.burn(bytes) (contracts/pool/franchised/FranchisedHybridPool.sol#122-146):
	External calls:
	- _transfer(token0,amount0,recipient,unwrapBento) (contracts/pool/franchised/FranchisedHybridPool.sol#133)
		- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMi
   - Recommendation: No specific recommendation provided.
