# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 5
- Retained Findings: 5
- Filtered Out: 0
- Total Reduction Rate: 0.00%
- False Positive Rate: 0.00%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability in `redeem` Function**
   - Contract: MockDerc20
   - Severity: Medium
   - Description: Reentrancy Vulnerability in `redeem` Function
   - Recommendation: Implement a locking mechanism using a modifier to prevent reentrant calls or use the checks-effects-interactions pattern.

2. **Unprotected Access to `mint` and `redeem` Functions**
   - Contract: MockDerc20
   - Severity: Medium
   - Description: Unprotected Access to `mint` and `redeem` Functions
   - Recommendation: Add access control checks, such as onlyOwner modifiers, to restrict function usage to authorized entities.

3. **solc-version**
   - Contract: MockDerc20
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint 0.6.12 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Upgrade to a newer Solidity version that addresses these bugs to enhance code security.

4. **naming-convention**
   - Contract: MockDerc20
   - Severity: Informational
   - Confidence: High
   - Line: 34
   - Description: Parameter MockDErc20.redeem(address,uint256)._amount (contracts/mock/MockDErc20.sol#34) is not in mixedCase

   - Recommendation: Rename the parameter `_amount` to follow the mixedCase convention for increased code readability.

5. **immutable-states**
   - Contract: MockDerc20
   - Severity: Optimization
   - Confidence: High
   - Line: 14
   - Description: MockDErc20.underlying (contracts/mock/MockDErc20.sol#14) should be immutable 

   - Recommendation: Declare `underlying` as immutable so that its value is set once and cannot be altered, optimizing gas usage.

## Unsupported Or False Positive

None
