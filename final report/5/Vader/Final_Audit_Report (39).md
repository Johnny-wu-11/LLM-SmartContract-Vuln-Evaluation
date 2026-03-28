# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 27
- Retained Findings: 16
- Filtered Out: 11
- Total Reduction Rate: 40.74%
- False Positive Rate: 40.74%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **tautology**
   - Contract: Vader
   - Function: _transfer(address,address,uint256)
   - Severity: Medium
   - Confidence: High
   - Description: Vader._transfer(address,address,uint256) (contracts/Vader.sol#122-134) contains a tautology or contradiction:
	- _fee >= 0 && _fee <= amount (contracts/Vader.sol#127)

   - Remediation: Remove the tautological check '_fee >= 0' if '_fee' is an unsigned integer, as it is always true. Verify logical correctness if '_fee' can never exceed 'amount'.

2. **boolean-equal**
   - Contract: Vader
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Vader.init(address,address,address) (contracts/Vader.sol#74-81) compares to a boolean constant:
	-require(bool)(inited == false) (contracts/Vader.sol#75)

   - Remediation: Replace 'require(bool)(inited == false)' with '!inited' for simplicity and readability.

3. **solc-version**
   - Contract: Vader
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Version constraint 0.8.3 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationChan
   - Remediation: Upgrade the Solidity compiler version to at least 0.8.4 to avoid known vulnerabilities.

4. **naming-convention**
   - Contract: Vader
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Vader.USDV (contracts/Vader.sol#34) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to 'usdv' to follow mixedCase naming conventions.

5. **naming-convention**
   - Contract: Vader
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Vader.USDV (contracts/Vader.sol#34) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to 'usdv' to follow mixedCase naming conventions.

6. **naming-convention**
   - Contract: Vader
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Variable Vader.USDV (contracts/Vader.sol#34) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to 'usdv' to follow mixedCase naming conventions.

7. **naming-convention**
   - Contract: Vader
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Vader.USDV (contracts/Vader.sol#34) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to 'usdv' to follow mixedCase naming conventions.

8. **naming-convention**
   - Contract: Vader
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Variable Vader.USDV (contracts/Vader.sol#34) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to 'usdv' to follow mixedCase naming conventions.

9. **naming-convention**
   - Contract: Vader
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: Variable Vader.USDV (contracts/Vader.sol#34) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to 'usdv' to follow mixedCase naming conventions.

10. **naming-convention**
   - Contract: Vader
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Vader.USDV (contracts/Vader.sol#34) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to 'usdv' to follow mixedCase naming conventions.

11. **naming-convention**
   - Contract: Vader
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable Vader.USDV (contracts/Vader.sol#34) is not in mixedCase

   - Remediation: Rename the variable 'USDV' to 'usdv' to follow mixedCase naming conventions.

12. **immutable-states**
   - Contract: Vader
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Vader._1m (contracts/Vader.sol#24) should be immutable 


13. **immutable-states**
   - Contract: Vader
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Vader.burnAddress (contracts/Vader.sol#36) should be immutable 


14. **immutable-states**
   - Contract: Vader
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Vader.decimals (contracts/Vader.sol#14) should be immutable 


15. **immutable-states**
   - Contract: Vader
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Vader.maxSupply (contracts/Vader.sol#27) should be immutable 


16. **immutable-states**
   - Contract: Vader
   - Function: Unknown
   - Severity: Optimization
   - Confidence: High
   - Description: Vader.baseline (contracts/Vader.sol#25) should be immutable 


## Unsupported Or False Positive

1. **events-access**
   - Contract: Vader
   - Function: changeDAO(address)
   - Severity: Low
   - Confidence: Medium
   - Description: Vader.changeDAO(address) (contracts/Vader.sol#193-196) should emit an event for: 
	- DAO = newDAO (contracts/Vader.sol#195)


2. **events-maths**
   - Contract: Vader
   - Function: setParams(uint256,uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Vader.setParams(uint256,uint256) (contracts/Vader.sol#179-182) should emit an event for: 
	- secondsPerEra = newEra (contracts/Vader.sol#180)
	- emissionCurve = newCurve (contracts/Vader.sol#181)


3. **missing-zero-check**
   - Contract: Vader
   - Function: setRewardAddress(address)
   - Severity: Low
   - Confidence: Medium
   - Description: Vader.init(address,address,address)._utils (contracts/Vader.sol#74) lacks a zero-check on :
		- UTILS = _utils (contracts/Vader.sol#79)


4. **missing-zero-check**
   - Contract: Vader
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: Vader.init(address,address,address)._utils (contracts/Vader.sol#74) lacks a zero-check on :
		- UTILS = _utils (contracts/Vader.sol#79)


5. **missing-zero-check**
   - Contract: Vader
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: Vader.init(address,address,address)._utils (contracts/Vader.sol#74) lacks a zero-check on :
		- UTILS = _utils (contracts/Vader.sol#79)


6. **missing-zero-check**
   - Contract: Vader
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: Vader.init(address,address,address)._utils (contracts/Vader.sol#74) lacks a zero-check on :
		- UTILS = _utils (contracts/Vader.sol#79)


7. **reentrancy-benign**
   - Contract: Vader
   - Function: upgrade(uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in Vader.redeemToMember(address) (contracts/Vader.sol#237-244):
	External calls:
	- iERC20(USDV).burn(_amount) (contracts/Vader.sol#240)
	State variables written after the call(s):
	- _mint(member,redeemAmount) (contracts/Vader.sol#242)
		- _balances[account] += amount (contracts/Vader.so
   - Remediation: Use the checks-effects-interactions pattern to manage state changes securely before external calls.

8. **reentrancy-benign**
   - Contract: Vader
   - Function: redeemToMember(address)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in Vader.redeemToMember(address) (contracts/Vader.sol#237-244):
	External calls:
	- iERC20(USDV).burn(_amount) (contracts/Vader.sol#240)
	State variables written after the call(s):
	- _mint(member,redeemAmount) (contracts/Vader.sol#242)
		- _balances[account] += amount (contracts/Vader.so
   - Remediation: Use the checks-effects-interactions pattern to manage state changes securely before external calls.

9. **reentrancy-events**
   - Contract: Vader
   - Function: redeemToMember(address)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in Vader.upgrade(uint256) (contracts/Vader.sol#228-231):
	External calls:
	- require(bool)(iERC20(VETHER).transferFrom(msg.sender,burnAddress,amount)) (contracts/Vader.sol#229)
	Event emitted after the call(s):
	- Transfer(address(0),account,amount) (contracts/Vader.sol#143)
		- _mint(msg
   - Remediation: Change the placement of events to before the state-changing external calls.

10. **reentrancy-events**
   - Contract: Vader
   - Function: upgrade(uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in Vader.upgrade(uint256) (contracts/Vader.sol#228-231):
	External calls:
	- require(bool)(iERC20(VETHER).transferFrom(msg.sender,burnAddress,amount)) (contracts/Vader.sol#229)
	Event emitted after the call(s):
	- Transfer(address(0),account,amount) (contracts/Vader.sol#143)
		- _mint(msg
   - Remediation: Change the placement of events to before the state-changing external calls.

11. **timestamp**
   - Contract: Vader
   - Function: _checkEmission()
   - Severity: Low
   - Confidence: Medium
   - Description: Vader._checkEmission() (contracts/Vader.sol#204-214) uses timestamp for comparisons
	Dangerous comparisons:
	- (block.timestamp >= nextEraTime) && emitting (contracts/Vader.sol#205)

