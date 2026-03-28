# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 4
- Retained Findings: 4
- Filtered Out: 0
- Total Reduction Rate: 0.00%
- False Positive Rate: 0.00%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Unrestricted Minting and Burning**
   - Contract: ERC20Mock
   - Severity: Medium
   - Description: Unrestricted Minting and Burning
   - Recommendation: Implement access control checks on minting and burning functions to restrict their usage to authorized addresses.

2. **solc-version**
   - Contract: ERC20Mock
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint ^0.6.12 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCh
   - Recommendation: Upgrade Solidity compiler to a version without the listed known severe issues, such as 0.8.x.

3. **missing-inheritance**
   - Contract: ERC20Mock
   - Severity: Informational
   - Confidence: High
   - Line: 10
   - Description: ERC20Mock (contracts/v3/alchemix/mocks/ERC20Mock.sol#10-23) should inherit from IVaultToken (contracts/v3/interfaces/IVaultToken.sol#5-8)

   - Recommendation: Add IVaultToken as a base contract to ERC20Mock to ensure compliance with the interface.

4. **naming-convention**
   - Contract: ERC20Mock
   - Severity: Informational
   - Confidence: High
   - Line: 16
   - Description: Parameter ERC20Mock.mint(address,uint256)._amount (contracts/v3/alchemix/mocks/ERC20Mock.sol#16) is not in mixedCase

   - Recommendation: Rename the parameter _amount to follow mixedCase naming convention, such as amount.

## Unsupported Or False Positive

None
