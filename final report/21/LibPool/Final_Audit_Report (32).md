# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 8
- Retained Findings: 7
- Filtered Out: 1
- Total Reduction Rate: 12.50%
- False Positive Rate: 12.50%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: LibPool
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Implement reentrancy guards on all functions that could allow reentrancy to ensure only one call can execute at a time.

2. **Access Control**
   - Contract: LibPool
   - Severity: Medium
   - Description: Access Control
   - Recommendation: Ensure that function access is restricted to appropriate roles using `require` statements or modifiers.

3. **Potential Denial of Service**
   - Contract: LibPool
   - Severity: Medium
   - Description: Potential Denial of Service
   - Recommendation: Optimize loops that depend on external input to avoid excessive execution times and implement gas limit checks.

4. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: LibPool
   - Severity: HIGH
   - Line: 21
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Incorporate robust price oracles that can resist manipulation or delay updates to prevent external influence on calculations.

5. **uninitialized-local**
   - Contract: LibPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 88
   - Description: LibPool.payOffDebtAll(IERC20).totalAccruedDebt (contracts/libraries/LibPool.sol#88) is a local variable never initialized

   - Recommendation: Initialize local variables before use to prevent unintended behavior or calculation errors.

6. **solc-version**
   - Contract: LibPool
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint ^0.7.4 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Upgrade the Solidity compiler version to the latest stable release to avoid known bugs and vulnerabilities.

7. **naming-convention**
   - Contract: LibPool
   - Severity: Informational
   - Confidence: High
   - Line: 70
   - Description: Parameter LibPool.stake(PoolStorage.Base,uint256,address)._receiver (contracts/libraries/LibPool.sol#70) is not in mixedCase

   - Recommendation: Refactor parameter names to use mixedCase to enhance readability and adhere to Solidity naming conventions.

## Unsupported Or False Positive

1. **reentrancy-events**
   - Contract: LibPool
   - Severity: Low
   - Confidence: Medium
   - Line: 249
   - Description: Reentrancy in SherX.harvestFor(address,ILock) (contracts/facets/SherX.sol#249-257):
	External calls:
	- doYield(_token,_user,_user,0) (contracts/facets/SherX.sol#254)
		- ps.lockToken.mint(_receiver,lock) (contracts/libraries/LibPool.sol#81)
		- LibPool.stake(psSherX,withdrawable_amount,from) (contr
   - Recommendation: No specific recommendation provided.
