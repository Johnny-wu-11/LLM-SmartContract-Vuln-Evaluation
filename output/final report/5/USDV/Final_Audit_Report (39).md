# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 31
- Retained Findings: 19
- Filtered Out: 12
- Total Reduction Rate: 38.71%
- False Positive Rate: 38.71%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **unchecked-transfer**
   - Contract: USDV
   - Function: _checkIncentives()
   - Severity: High
   - Confidence: Medium
   - Description: USDV._checkIncentives() (contracts/USDV.sol#146-161) ignores return value by iERC20(VADER).transfer(VAULT,iERC20(VADER).balanceOf(address(this))) (contracts/USDV.sol#158)

   - Remediation: Verify the return value of the transfer to ensure it completes successfully and handle any errors.

2. **unchecked-transfer**
   - Contract: USDV
   - Function: _checkIncentives()
   - Severity: High
   - Confidence: Medium
   - Description: USDV._checkIncentives() (contracts/USDV.sol#146-161) ignores return value by iERC20(VADER).transfer(VAULT,iERC20(VADER).balanceOf(address(this))) (contracts/USDV.sol#158)

   - Remediation: Verify the return value of the transfer to ensure it completes successfully and handle any errors.

3. **reentrancy-no-eth**
   - Contract: USDV
   - Function: convertForMember(address,uint256)
   - Severity: Medium
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER
   - Remediation: Use a state-changing operation before external calls to apply the checks-effects-interactions pattern.

4. **reentrancy-no-eth**
   - Contract: USDV
   - Function: _checkIncentives()
   - Severity: Medium
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER
   - Remediation: Use a state-changing operation before external calls to apply the checks-effects-interactions pattern.

5. **reentrancy-no-eth**
   - Contract: USDV
   - Function: redeemForMember(address,uint256)
   - Severity: Medium
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER
   - Remediation: Use a state-changing operation before external calls to apply the checks-effects-interactions pattern.

6. **reentrancy-no-eth**
   - Contract: USDV
   - Function: _checkIncentives()
   - Severity: Medium
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER
   - Remediation: Use a state-changing operation before external calls to apply the checks-effects-interactions pattern.

7. **tx-origin**
   - Contract: USDV
   - Function: isMature()
   - Severity: Medium
   - Confidence: Medium
   - Description: USDV.isMature() (contracts/USDV.sol#40-44) uses tx.origin for authorization: lastBlock[tx.origin] + blockDelay <= block.number (contracts/USDV.sol#41)

   - Remediation: Replace tx.origin with msg.sender to prevent potential phishing attacks.

8. **boolean-equal**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: USDV.init(address,address,address) (contracts/USDV.sol#54-61) compares to a boolean constant:
	-require(bool)(inited == false) (contracts/USDV.sol#55)

   - Remediation: Use !inited instead of inited == false for a cleaner and more idiomatic check.

9. **solc-version**
   - Contract: USDV
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Version constraint 0.8.3 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationChan
   - Remediation: Upgrade the Solidity compiler version to the latest stable release to patch known vulnerabilities.

10. **naming-convention**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter USDV.init(address,address,address)._vader (contracts/USDV.sol#54) is not in mixedCase

   - Remediation: Rename the parameter _vader to follow mixedCase naming convention for better readability.

11. **naming-convention**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter USDV.init(address,address,address)._vader (contracts/USDV.sol#54) is not in mixedCase

   - Remediation: Rename the parameter _vader to follow mixedCase naming convention for better readability.

12. **naming-convention**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter USDV.init(address,address,address)._vader (contracts/USDV.sol#54) is not in mixedCase

   - Remediation: Rename the parameter _vader to follow mixedCase naming convention for better readability.

13. **naming-convention**
   - Contract: iUSDV
   - Function: ROUTER()
   - Severity: Informational
   - Confidence: High
   - Description: Function iUSDV.ROUTER() (contracts/interfaces/iUSDV.sol#5) is not in mixedCase


14. **naming-convention**
   - Contract: iUSDV
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Contract iUSDV (contracts/interfaces/iUSDV.sol#4-14) is not in CapWords


15. **naming-convention**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter USDV.init(address,address,address)._vader (contracts/USDV.sol#54) is not in mixedCase

   - Remediation: Rename the parameter _vader to follow mixedCase naming convention for better readability.

16. **naming-convention**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter USDV.init(address,address,address)._vader (contracts/USDV.sol#54) is not in mixedCase

   - Remediation: Rename the parameter _vader to follow mixedCase naming convention for better readability.

17. **naming-convention**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter USDV.init(address,address,address)._vader (contracts/USDV.sol#54) is not in mixedCase

   - Remediation: Rename the parameter _vader to follow mixedCase naming convention for better readability.

18. **naming-convention**
   - Contract: USDV
   - Function: DAO()
   - Severity: Informational
   - Confidence: High
   - Description: Parameter USDV.init(address,address,address)._vader (contracts/USDV.sol#54) is not in mixedCase

   - Remediation: Rename the parameter _vader to follow mixedCase naming convention for better readability.

19. **immutable-states**
   - Contract: USDV
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: USDV.decimals (contracts/USDV.sol#13) should be immutable 


## Unsupported Or False Positive

1. **events-maths**
   - Contract: USDV
   - Function: setParams(uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: USDV.setParams(uint256) (contracts/USDV.sol#140-142) should emit an event for: 
	- blockDelay = newDelay (contracts/USDV.sol#141) 


2. **missing-zero-check**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: USDV.init(address,address,address)._vault (contracts/USDV.sol#54) lacks a zero-check on :
		- VAULT = _vault (contracts/USDV.sol#58)


3. **missing-zero-check**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: USDV.init(address,address,address)._vault (contracts/USDV.sol#54) lacks a zero-check on :
		- VAULT = _vault (contracts/USDV.sol#58)


4. **missing-zero-check**
   - Contract: USDV
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: USDV.init(address,address,address)._vault (contracts/USDV.sol#54) lacks a zero-check on :
		- VAULT = _vault (contracts/USDV.sol#58)


5. **reentrancy-benign**
   - Contract: USDV
   - Function: _convert(address,uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in USDV.transferFrom(address,address,uint256) (contracts/USDV.sol#88-92):
	External calls:
	- _transfer(sender,recipient,amount) (contracts/USDV.sol#89)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
		- iERC20(VADER).transfer(ROUTER,iERC20(VADER).balanceOf(address(this)) / 2) (c

6. **reentrancy-benign**
   - Contract: USDV
   - Function: transferFrom(address,address,uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in USDV.transferFrom(address,address,uint256) (contracts/USDV.sol#88-92):
	External calls:
	- _transfer(sender,recipient,amount) (contracts/USDV.sol#89)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
		- iERC20(VADER).transfer(ROUTER,iERC20(VADER).balanceOf(address(this)) / 2) (c

7. **reentrancy-events**
   - Contract: USDV
   - Function: _checkIncentives()
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER

8. **reentrancy-events**
   - Contract: USDV
   - Function: convertForMember(address,uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER

9. **reentrancy-events**
   - Contract: USDV
   - Function: transferFrom(address,address,uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER

10. **reentrancy-events**
   - Contract: USDV
   - Function: _checkIncentives()
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER

11. **reentrancy-events**
   - Contract: USDV
   - Function: _convert(address,uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in USDV._checkIncentives() (contracts/USDV.sol#146-161):
	External calls:
	- _convert(address(this),_USDVShare) (contracts/USDV.sol#152)
		- iERC20(VADER).burn(amount) (contracts/USDV.sol#177)
	- _transfer(address(this),ROUTER,balanceOf(address(this)) / 2) (contracts/USDV.sol#154)
		- iER

12. **timestamp**
   - Contract: USDV
   - Function: _checkIncentives()
   - Severity: Low
   - Confidence: Medium
   - Description: USDV._checkIncentives() (contracts/USDV.sol#146-161) uses timestamp for comparisons
	Dangerous comparisons:
	- block.timestamp >= nextEraTime && emitting() (contracts/USDV.sol#147)

