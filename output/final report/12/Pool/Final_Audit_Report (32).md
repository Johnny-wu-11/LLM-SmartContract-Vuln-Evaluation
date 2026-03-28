# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 9
- Retained Findings: 8
- Filtered Out: 1
- Total Reduction Rate: 11.11%
- False Positive Rate: 11.11%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: Pool
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Implement reentrancy guards on critical functions using OpenZeppelin's ReentrancyGuard.

2. **Integer Overflow/Underflow**
   - Contract: Pool
   - Severity: Medium
   - Description: Integer Overflow/Underflow
   - Recommendation: Use SafeMath library to perform arithmetic operations to prevent overflows and underflows.

3. **Access Control**
   - Contract: Pool
   - Severity: Medium
   - Description: Access Control
   - Recommendation: Ensure that all critical functions have appropriate access modifiers, such as onlyOwner.

4. **Timestamp Dependence**
   - Contract: Pool
   - Severity: Medium
   - Description: Timestamp Dependence
   - Recommendation: Avoid relying directly on block timestamps for critical logic; use block numbers instead if possible.

5. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: Pool
   - Severity: HIGH
   - Line: 165
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Implement checks to ensure accurate LP token pricing and consider using price oracles.

6. **divide-before-multiply**
   - Contract: Pool
   - Severity: Medium
   - Confidence: Medium
   - Line: 231
   - Description: Pool._mintInternal(address,bool,uint256,uint256) (contracts/yieldspace/Pool.sol#231-298) performs a multiplication on the result of a division:
	- tokensMinted = (supply * (fyTokenToBuy + fyTokenIn)) / (_realFYTokenCached - fyTokenToBuy) (contracts/yieldspace/Pool.sol#269)
	- baseIn = baseToSell + (
   - Recommendation: Reorder the operations to perform multiplication before division to maintain precision.

7. **uninitialized-local**
   - Contract: Pool
   - Severity: Medium
   - Confidence: Medium
   - Line: 253
   - Description: Pool._mintInternal(address,bool,uint256,uint256).baseToSell (contracts/yieldspace/Pool.sol#253) is a local variable never initialized

   - Recommendation: Ensure all local variables are initialized before use to avoid unexpected behavior.

8. **solc-version**
   - Contract: Pool
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint >=0.8.0 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCh
   - Recommendation: Upgrade to the latest stable Solidity version to mitigate known issues.

## Unsupported Or False Positive

1. **reentrancy-events**
   - Contract: Pool
   - Severity: Low
   - Confidence: Medium
   - Line: 329
   - Description: Reentrancy in Pool._burnInternal(address,bool,uint256,uint256) (contracts/yieldspace/Pool.sol#329-377):
	External calls:
	- base.safeTransfer(to,tokenOut) (contracts/yieldspace/Pool.sol#372)
	- IERC20(address(fyToken)).safeTransfer(to,fyTokenOut) (contracts/yieldspace/Pool.sol#373)
	Event emitted af
   - Recommendation: No specific recommendation provided.
