# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 7
- Retained Findings: 6
- Filtered Out: 1
- Total Reduction Rate: 14.29%
- False Positive Rate: 14.29%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **solc-version**
   - Contract: Synth
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Version constraint 0.8.3 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationChan
   - Remediation: Upgrade the Solidity compiler to a version unaffected by these issues to mitigate potential vulnerabilities.

2. **naming-convention**
   - Contract: Synth
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Synth.TOKEN (contracts/Synth.sol#11) is not in mixedCase

   - Remediation: Rename the variable Synth.TOKEN to use mixedCase to adhere to standard naming conventions.

3. **naming-convention**
   - Contract: Synth
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Synth.TOKEN (contracts/Synth.sol#11) is not in mixedCase

   - Remediation: Rename the variable Synth.TOKEN to use mixedCase to adhere to standard naming conventions.

4. **constable-states**
   - Contract: Synth
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Synth.decimals (contracts/Synth.sol#16) should be constant 

   - Remediation: Declare the Synth.decimals variable as constant to potentially save gas and improve readability.

5. **immutable-states**
   - Contract: Synth
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Synth.FACTORY (contracts/Synth.sol#10) should be immutable 

   - Remediation: Declare the Synth.FACTORY variable as immutable for optimization since its value is set once during deployment and never changes.

6. **immutable-states**
   - Contract: Synth
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Synth.FACTORY (contracts/Synth.sol#10) should be immutable 

   - Remediation: Declare the Synth.FACTORY variable as immutable for optimization since its value is set once during deployment and never changes.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: Synth
   - Function: constructor(address)
   - Severity: Low
   - Confidence: Medium
   - Description: Synth.constructor(address)._token (contracts/Synth.sol#29) lacks a zero-check on :
		- TOKEN = _token (contracts/Synth.sol#30)

