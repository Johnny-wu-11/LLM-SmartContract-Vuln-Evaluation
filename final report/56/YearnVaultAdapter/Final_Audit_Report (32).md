# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 10
- Retained Findings: 9
- Filtered Out: 1
- Total Reduction Rate: 10.00%
- False Positive Rate: 10.00%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Unchecked External Calls**
   - Contract: YearnVaultAdapter
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Ensure all external calls are followed by checks on the return values to handle possible failure cases.

2. **Approval of Token**
   - Contract: YearnVaultAdapter
   - Severity: Medium
   - Description: Approval of Token
   - Recommendation: Validate token allowances and ensure approvals are properly scoped to prevent unintended transfers.

3. **Admin Privileges**
   - Contract: YearnVaultAdapter
   - Severity: Medium
   - Description: Admin Privileges
   - Recommendation: Restrict administrative functions to secure addresses and add access control checks.

4. **Reentrancy**
   - Contract: YearnVaultAdapter
   - Severity: Medium
   - Description: Reentrancy
   - Recommendation: Implement a `nonReentrant` modifier using OpenZeppelin's ReentrancyGuard.

5. **Decimal Handling**
   - Contract: YearnVaultAdapter
   - Severity: Medium
   - Description: Decimal Handling
   - Recommendation: Ensure consistent decimal arithmetic using libraries like SafeMath.

6. **unused-return**
   - Contract: YearnVaultAdapter
   - Severity: Medium
   - Confidence: Medium
   - Line: 72
   - Description: YearnVaultAdapter.withdraw(address,uint256) (contracts/v3/alchemix/adapters/YearnVaultAdapter.sol#72-74) ignores return value by vault.withdraw(_tokensToShares(_amount),_recipient) (contracts/v3/alchemix/adapters/YearnVaultAdapter.sol#73)

   - Recommendation: Check the return value of `vault.withdraw` and handle errors or unexpected conditions accordingly.

7. **solc-version**
   - Contract: YearnVaultAdapter
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint ^0.6.12 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCh
   - Recommendation: Upgrade Solidity to a version without these known issues, such as ^0.8.x, for better security.

8. **naming-convention**
   - Contract: YearnVaultAdapter
   - Severity: Informational
   - Confidence: High
   - Line: 62
   - Description: Parameter YearnVaultAdapter.deposit(uint256)._amount (contracts/v3/alchemix/adapters/YearnVaultAdapter.sol#62) is not in mixedCase

   - Recommendation: Rename `_amount` to follow mixedCase as per Solidity naming conventions.

9. **immutable-states**
   - Contract: YearnVaultAdapter
   - Severity: Optimization
   - Confidence: High
   - Line: 30
   - Description: YearnVaultAdapter.decimals (contracts/v3/alchemix/adapters/YearnVaultAdapter.sol#30) should be immutable 

   - Recommendation: Make `decimals` immutable to save gas and ensure it remains constant after deployment.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: YearnVaultAdapter
   - Severity: Low
   - Confidence: Medium
   - Line: 32
   - Description: YearnVaultAdapter.constructor(IyVaultV2,address)._admin (contracts/v3/alchemix/adapters/YearnVaultAdapter.sol#32) lacks a zero-check on :
		- admin = _admin (contracts/v3/alchemix/adapters/YearnVaultAdapter.sol#34)

   - Recommendation: No specific recommendation provided.
