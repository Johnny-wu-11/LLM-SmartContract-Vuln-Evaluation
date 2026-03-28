# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 19
- Retained Findings: 16
- Filtered Out: 3
- Total Reduction Rate: 15.79%
- False Positive Rate: 15.79%

## Confirmed Findings

1. **Reentrancy Vulnerability**
   - Contract: Transmuter
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Use the checks-effects-interactions pattern to mitigate reentrancy attacks. Ensure that state changes occur before calling external contracts.

2. **Access Control**
   - Contract: Transmuter
   - Severity: Medium
   - Description: Access Control
   - Recommendation: Implement role-based access control using OpenZeppelin's AccessControl library to restrict function access to authorized roles only.

3. **Pending Governance**
   - Contract: Transmuter
   - Severity: Medium
   - Description: Pending Governance
   - Recommendation: Introduce a time-lock mechanism for governance actions to prevent immediate implementation without sufficient notice.

## Plausible But Unverified Findings

1. **Integer Underflow/Overflow**
   - Contract: Transmuter
   - Severity: Medium
   - Description: Integer Underflow/Overflow
   - Recommendation: Use SafeMath library to prevent integer underflows and overflows, or switch to Solidity 0.8.x where overflow checks are built-in.

2. **Gas Limit and Loops**
   - Contract: Transmuter
   - Severity: Medium
   - Description: Gas Limit and Loops
   - Recommendation: Ensure loops are limited in iterations or fees are adjusted to prevent gas exhaustion. Consider breaking complex loops into smaller transactions.

3. **Zero Address Handling**
   - Contract: Transmuter
   - Severity: Medium
   - Description: Zero Address Handling
   - Recommendation: Add checks for zero address inputs and revert transactions when such an address is detected to prevent unexpected behavior.

4. **Potential for Forced Transmute Abuse**
   - Contract: Transmuter
   - Severity: Medium
   - Description: Potential for Forced Transmute Abuse
   - Recommendation: Implement validation checks and require user confirmations before executing sensitive operations to prevent manipulation.

5. **arbitrary-send-erc20**
   - Contract: Transmuter
   - Severity: High
   - Confidence: High
   - Line: 363
   - Description: Transmuter.distribute(address,uint256) (contracts/v3/alchemix/Transmuter.sol#363-366) uses arbitrary from in transferFrom: IERC20Burnable(Token).safeTransferFrom(origin,address(this),amount) (contracts/v3/alchemix/Transmuter.sol#364)

   - Recommendation: Verify the origin parameter to ensure it matches the expected sender or implement an allowance-based mechanism to restrict unauthorized transfers.

6. **divide-before-multiply**
   - Contract: Transmuter
   - Severity: Medium
   - Confidence: Medium
   - Line: 421
   - Description: Transmuter.getMultipleUserInfo(uint256,uint256) (contracts/v3/alchemix/Transmuter.sol#421-443) performs a multiplication on the result of a division:
	- _toDistribute = buffer.mul(block.number.sub(lastDepositBlock)).div(TRANSMUTATION_PERIOD) (contracts/v3/alchemix/Transmuter.sol#431)
	- _theUserData
   - Recommendation: Reorder arithmetic operations to multiply before dividing to maintain precision, where applicable.

7. **reentrancy-no-eth**
   - Contract: Transmuter
   - Severity: Medium
   - Confidence: Medium
   - Line: 242
   - Description: Reentrancy in Transmuter.transmute() (contracts/v3/alchemix/Transmuter.sol#242-273):
	External calls:
	- IERC20Burnable(AlToken).burn(pendingz) (contracts/v3/alchemix/Transmuter.sol#263)
	State variables written after the call(s):
	- increaseAllocations(diff) (contracts/v3/alchemix/Transmuter.sol#26
   - Recommendation: Apply the checks-effects-interactions pattern and ensure that sensitive state changes occur before any external call.

8. **uninitialized-local**
   - Contract: Transmuter
   - Severity: Medium
   - Confidence: Medium
   - Line: 245
   - Description: Transmuter.transmute().diff (contracts/v3/alchemix/Transmuter.sol#245) is a local variable never initialized

   - Recommendation: Initialize local variables before use to avoid undefined behavior and ensure predictable execution.

9. **solc-version**
   - Contract: Transmuter
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint 0.6.12 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Upgrade the Solidity compiler to the latest stable version to benefit from security enhancements and bug fixes.

10. **missing-inheritance**
   - Contract: Transmuter
   - Severity: Informational
   - Confidence: High
   - Line: 47
   - Description: Transmuter (contracts/v3/alchemix/Transmuter.sol#47-493) should inherit from ITransmuter (contracts/v3/alchemix/interfaces/ITransmuter.sol#4-7)

   - Recommendation: Ensure the contract inherits from ITransmuter to align with the expected interface and guarantee consistent behavior.

11. **naming-convention**
   - Contract: Transmuter
   - Severity: Informational
   - Confidence: High
   - Line: 490
   - Description: Parameter Transmuter.setWhitelist(address,bool)._state (contracts/v3/alchemix/Transmuter.sol#490) is not in mixedCase

   - Recommendation: No specific recommendation provided.

12. **constable-states**
   - Contract: Transmuter
   - Severity: Optimization
   - Confidence: High
   - Line: 72
   - Description: Transmuter.pointMultiplier (contracts/v3/alchemix/Transmuter.sol#72) should be constant 

   - Recommendation: No specific recommendation provided.

13. **immutable-states**
   - Contract: Transmuter
   - Severity: Optimization
   - Confidence: High
   - Line: 56
   - Description: Transmuter.Token (contracts/v3/alchemix/Transmuter.sol#56) should be immutable 

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **events-maths**
   - Contract: Transmuter
   - Severity: Low
   - Confidence: Medium
   - Line: 213
   - Description: Transmuter.unstake(uint256) (contracts/v3/alchemix/Transmuter.sol#213-220) should emit an event for: 
	- totalSupplyAltokens = totalSupplyAltokens.sub(amount) (contracts/v3/alchemix/Transmuter.sol#218) 

   - Recommendation: No specific recommendation provided.

2. **missing-zero-check**
   - Contract: Transmuter
   - Severity: Low
   - Confidence: Medium
   - Line: 98
   - Description: Transmuter.constructor(address,address,address)._Token (contracts/v3/alchemix/Transmuter.sol#98) lacks a zero-check on :
		- Token = _Token (contracts/v3/alchemix/Transmuter.sol#102)

   - Recommendation: No specific recommendation provided.

3. **reentrancy-benign**
   - Contract: Transmuter
   - Severity: Low
   - Confidence: Medium
   - Line: 282
   - Description: Reentrancy in Transmuter.forceTransmute(address) (contracts/v3/alchemix/Transmuter.sol#282-327):
	External calls:
	- IERC20Burnable(AlToken).burn(pendingz) (contracts/v3/alchemix/Transmuter.sol#310)
	State variables written after the call(s):
	- realisedTokens[toTransmute] = realisedTokens[toTransmu
   - Recommendation: No specific recommendation provided.
