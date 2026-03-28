# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 7
- Retained Findings: 5
- Filtered Out: 2
- Total Reduction Rate: 28.57%
- False Positive Rate: 28.57%

## Confirmed Findings

1. **Reentrancy**
   - Contract: MIMConvexStrategy
   - Severity: Medium
   - Description: Reentrancy
   - Recommendation: Consider using reentrancy guards or the checks-effects-interactions pattern to prevent reentrancy attacks.

## Plausible But Unverified Findings

1. **Unchecked External Call**
   - Contract: MIMConvexStrategy
   - Severity: Medium
   - Description: Unchecked External Call
   - Recommendation: Validate the return value of external calls and revert if the call fails to ensure reliable execution.

2. **Denial of Service**
   - Contract: MIMConvexStrategy
   - Severity: Medium
   - Description: Denial of Service
   - Recommendation: Ensure that loops involving external calls have a fixed maximum iteration count to prevent out-of-gas errors.

3. **unused-return**
   - Contract: MIMConvexStrategy
   - Severity: Medium
   - Confidence: Medium
   - Line: 154
   - Description: MIMConvexStrategy._withdraw(uint256) (contracts/v3/strategies/MIMConvexStrategy.sol#154-156) ignores return value by convexVault.withdraw(pid,_amount) (contracts/v3/strategies/MIMConvexStrategy.sol#155)

   - Recommendation: Check the return value of convexVault.withdraw and handle failures appropriately to avoid unexpected behavior.

4. **solc-version**
   - Contract: MIMConvexStrategy
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint 0.6.12 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Upgrade to a more recent stable version of Solidity to mitigate known issues and improve security.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: MIMConvexStrategy
   - Severity: Low
   - Confidence: Medium
   - Line: 60
   - Description: MIMConvexStrategy.constructor(string,address,address,address,address,address,address,uint256,IConvexVault,IStableSwap2Pool,address,address,address)._token (contracts/v3/strategies/MIMConvexStrategy.sol#60) lacks a zero-check on :
		- mimCvxDepositLP = _token (contracts/v3/strategies/MIMConvexStrateg
   - Recommendation: No specific recommendation provided.

2. **calls-loop**
   - Contract: MIMConvexStrategy
   - Severity: Low
   - Confidence: Medium
   - Line: 125
   - Description: MIMConvexStrategy._harvest(uint256,uint256) (contracts/v3/strategies/MIMConvexStrategy.sol#125-148) has external calls inside a loop: _extraRewardBalance = IERC20(_rewardToken).balanceOf(address(this)) (contracts/v3/strategies/MIMConvexStrategy.sol#135)
	Calls stack containing the loop:
		BaseStrate
   - Recommendation: No specific recommendation provided.
