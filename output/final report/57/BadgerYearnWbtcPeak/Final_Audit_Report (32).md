# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 5
- Retained Findings: 4
- Filtered Out: 1
- Total Reduction Rate: 20.00%
- False Positive Rate: 20.00%

## Confirmed Findings

1. **Reentrancy Vulnerability**
   - Contract: BadgerYearnWbtcPeak
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Use the checks-effects-interactions pattern to prevent reentrancy. Ensure state changes occur before external calls and consider using a reentrancy guard.

## Plausible But Unverified Findings

1. **Access Control**
   - Contract: BadgerYearnWbtcPeak
   - Severity: Medium
   - Description: Access Control
   - Recommendation: Review access modifiers to ensure only authorized accounts can call sensitive functions. Consider adding role-based checks or ownership requirements.

2. **Potential Denial of Service (DoS)**
   - Contract: BadgerYearnWbtcPeak
   - Severity: Medium
   - Description: Potential Denial of Service (DoS)
   - Recommendation: Ensure loops have a constant or small execution time bound. Verify that computations cannot be forced into a worst-case scenario by external inputs.

3. **solc-version**
   - Contract: BadgerYearnWbtcPeak
   - Severity: Informational
   - Confidence: High
   - Line: 3
   - Description: Version constraint 0.6.11 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Upgrade the Solidity compiler version to at least 0.6.12 to avoid known vulnerabilities.

## Unsupported Or False Positive

1. **reentrancy-events**
   - Contract: BadgerYearnWbtcPeak
   - Severity: Low
   - Confidence: Medium
   - Line: 44
   - Description: Reentrancy in BadgerYearnWbtcPeak.mint(uint256,bytes32[]) (contracts/peaks/BadgerYearnWbtcPeak.sol#44-55):
	External calls:
	- outAmount = core.mint(_byvWbtcToBtc(inAmount),msg.sender,merkleProof) (contracts/peaks/BadgerYearnWbtcPeak.sol#52)
	- byvWBTC.safeTransferFrom(msg.sender,address(this),inAmo
   - Recommendation: No specific recommendation provided.
