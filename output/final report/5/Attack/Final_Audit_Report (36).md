# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 13
- Retained Findings: 11
- Filtered Out: 2
- Total Reduction Rate: 15.38%
- False Positive Rate: 15.38%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **unused-return**
   - Contract: Attack
   - Function: attackUSDV(uint256)
   - Severity: Medium
   - Confidence: Medium
   - Description: Attack.attackUSDV(uint256) (contracts/Attack.sol#28-34) ignores return value by iERC20(VADER).transferTo(address(this),amount) (contracts/Attack.sol#31)

   - Remediation: Check the return value of iERC20(VADER).transferTo and handle any failures appropriately.

2. **unused-return**
   - Contract: Attack
   - Function: attackUSDV(uint256)
   - Severity: Medium
   - Confidence: Medium
   - Description: Attack.attackUSDV(uint256) (contracts/Attack.sol#28-34) ignores return value by iERC20(USDV).approve(USDV,amount) (contracts/Attack.sol#30)

   - Remediation: Verify the return value of iERC20(USDV).approve and ensure appropriate action is taken if it fails.

3. **unused-return**
   - Contract: Attack
   - Function: attackUSDV(uint256)
   - Severity: Medium
   - Confidence: Medium
   - Description: Attack.attackUSDV(uint256) (contracts/Attack.sol#28-34) ignores return value by iUSDV(USDV).redeem(amount) (contracts/Attack.sol#33)

   - Remediation: Handle the return value of iUSDV(USDV).redeem to check for successful execution.

4. **unused-return**
   - Contract: Attack
   - Function: attackUSDV(uint256)
   - Severity: Medium
   - Confidence: Medium
   - Description: Attack.attackUSDV(uint256) (contracts/Attack.sol#28-34) ignores return value by iERC20(VADER).approve(USDV,amount) (contracts/Attack.sol#29)

   - Remediation: Include a check for the return value of iERC20(VADER).approve and handle any issues if it fails.

5. **unused-return**
   - Contract: Attack
   - Function: attackUSDV(uint256)
   - Severity: Medium
   - Confidence: Medium
   - Description: Attack.attackUSDV(uint256) (contracts/Attack.sol#28-34) ignores return value by iUSDV(USDV).convert(amount) (contracts/Attack.sol#32)

   - Remediation: Add logic to confirm the success of iUSDV(USDV).convert by checking its return value.

6. **boolean-equal**
   - Contract: Attack
   - Function: init(address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Attack.init(address,address) (contracts/Attack.sol#20-25) compares to a boolean constant:
	-require(bool)(inited == false) (contracts/Attack.sol#21)

   - Remediation: Use the ! operator instead of comparing directly to false for improved readability.

7. **solc-version**
   - Contract: Attack
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Version constraint 0.8.3 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationChan
   - Remediation: Upgrade to the latest stable version of Solidity to avoid known compiler issues.

8. **naming-convention**
   - Contract: Attack
   - Function: init(address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter Attack.init(address,address)._USDV (contracts/Attack.sol#20) is not in mixedCase

   - Remediation: Rename parameter _USDV to use mixedCase, such as usdV, to follow naming conventions.

9. **naming-convention**
   - Contract: Attack
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Attack.USDV (contracts/Attack.sol#14) is not in mixedCase

   - Remediation: Change variable USDV to usdV to comply with mixedCase naming conventions.

10. **naming-convention**
   - Contract: Attack
   - Function: init(address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter Attack.init(address,address)._vader (contracts/Attack.sol#20) is not in mixedCase

   - Remediation: Update parameter _vader to a mixedCase naming style, like vader, to improve readability.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: Attack
   - Function: init(address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: Attack.init(address,address)._USDV (contracts/Attack.sol#20) lacks a zero-check on :
		- USDV = _USDV (contracts/Attack.sol#24)


2. **missing-zero-check**
   - Contract: Attack
   - Function: init(address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: Attack.init(address,address)._vader (contracts/Attack.sol#20) lacks a zero-check on :
		- VADER = _vader (contracts/Attack.sol#23)

