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

1. **boolean-equal**
   - Contract: Factory
   - Function: init(address)
   - Severity: Informational
   - Confidence: High
   - Description: Factory.init(address) (contracts/Factory.sol#27-31) compares to a boolean constant:
	-require(bool)(inited == false) (contracts/Factory.sol#28)

   - Remediation: Ensure the boolean comparison uses explicit equality checks with constants, or refactor logic for clarity.

2. **solc-version**
   - Contract: Factory
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Version constraint 0.8.3 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationChan
   - Remediation: Upgrade the Solidity compiler to a version without these known issues for improved security.

3. **naming-convention**
   - Contract: Factory
   - Function: init(address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter Factory.init(address)._pool (contracts/Factory.sol#27) is not in mixedCase

   - Remediation: Rename the parameter '_pool' to use mixedCase, such as 'poolAddress'.

4. **naming-convention**
   - Contract: Factory
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Factory.VADER (contracts/Factory.sol#10) is not in mixedCase

   - Remediation: Rename the variable 'VADER' to use mixedCase, such as 'vader'.

5. **naming-convention**
   - Contract: Factory
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Factory.POOLS (contracts/Factory.sol#12) is not in mixedCase

   - Remediation: Rename the variable 'POOLS' to use mixedCase, such as 'pools'.

6. **naming-convention**
   - Contract: Factory
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Factory.USDV (contracts/Factory.sol#11) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to use mixedCase, such as 'usdv'.

7. **constable-states**
   - Contract: Factory
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Factory.USDV (contracts/Factory.sol#11) should be constant 

   - Remediation: Declare the 'USDV' variable as constant to improve gas efficiency.

8. **constable-states**
   - Contract: Factory
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Factory.VADER (contracts/Factory.sol#10) should be constant 

   - Remediation: Declare the 'VADER' variable as constant to save on gas costs.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: Factory
   - Function: init(address)
   - Severity: Low
   - Confidence: Medium
   - Description: Factory.init(address)._pool (contracts/Factory.sol#27) lacks a zero-check on :
		- POOLS = _pool (contracts/Factory.sol#30)

