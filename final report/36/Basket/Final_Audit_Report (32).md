# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 18
- Retained Findings: 15
- Filtered Out: 3
- Total Reduction Rate: 16.67%
- False Positive Rate: 16.67%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: Basket
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Use the checks-effects-interactions pattern to prevent reentrancy. Ensure all state changes occur before external calls.

2. **Denial of Service (DoS) - Gas exhaustion**
   - Contract: Basket
   - Severity: Medium
   - Description: Denial of Service (DoS) - Gas exhaustion
   - Recommendation: Optimize loops and external calls to prevent gas exhaustion. Limit iteration counts or split calls across transactions.

3. **Integer Overflow/Underflow**
   - Contract: Basket
   - Severity: Medium
   - Description: Integer Overflow/Underflow
   - Recommendation: Use SafeMath operations or Solidity 0.8+ to automatically check for overflows and underflows.

4. **Timestamp Dependence**
   - Contract: Basket
   - Severity: Medium
   - Description: Timestamp Dependence
   - Recommendation: Avoid using block timestamps for logic that affects contract outcomes. Use block numbers or trusted oracles instead.

5. **Unprotected Function**
   - Contract: Basket
   - Severity: Medium
   - Description: Unprotected Function
   - Recommendation: Add appropriate access control to restrict function access. Use modifiers like onlyOwner where needed.

6. **Lack of Access Control**
   - Contract: Basket
   - Severity: Medium
   - Description: Lack of Access Control
   - Recommendation: Implement role-based access control using OpenZeppelin's AccessControl library or similar patterns.

7. **Pending State Variables Initialization**
   - Contract: Basket
   - Severity: Medium
   - Description: Pending State Variables Initialization
   - Recommendation: Initialize all state variables in the constructor or in the variable declaration to prevent reliance on default values.

8. **Handling Fees Logic**
   - Contract: Basket
   - Severity: Medium
   - Description: Handling Fees Logic
   - Recommendation: Review fee calculations for accuracy and ensure correct order of operations. Consider defensive checks to prevent inaccurate fees.

9. **divide-before-multiply**
   - Contract: Basket
   - Severity: Medium
   - Confidence: Medium
   - Line: 110
   - Description: Basket.handleFees() (contracts/Basket.sol#110-129) performs a multiplication on the result of a division:
	- feePct = timeDiff * licenseFee / ONE_YEAR (contracts/Basket.sol#117)
	- fee = startSupply * feePct / (BASE - feePct) (contracts/Basket.sol#118)

   - Recommendation: Rearrange calculations to multiply before division to minimize precision loss. Confirm variables do not unintentionally become zero.

10. **incorrect-equality**
   - Contract: Basket
   - Severity: Medium
   - Confidence: High
   - Line: 110
   - Description: Basket.handleFees() (contracts/Basket.sol#110-129) uses a dangerous strict equality:
	- lastFee == 0 (contracts/Basket.sol#111)

   - Recommendation: Replace strict equality checks with safe alternatives or add assertions to handle differing conditions robustly.

11. **reentrancy-no-eth**
   - Contract: Basket
   - Severity: Medium
   - Confidence: Medium
   - Line: 170
   - Description: Reentrancy in Basket.publishNewIndex(address[],uint256[]) (contracts/Basket.sol#170-194):
	External calls:
	- auction.killAuction() (contracts/Basket.sol#182)
	State variables written after the call(s):
	- pendingWeights.tokens = _tokens (contracts/Basket.sol#184)
	Basket.pendingWeights (contracts/Basket.sol#29) can be used in cross function reentrancies:
	- Basket.deleteNewIndex() (contracts/Basket.sol#207-214)
	- Basket.getPendingWeights() (contracts/Basket.sol#49-51)
	- Basket.pendingWeights (contracts/Basket.sol#29)
	- Basket.publishNewIndex(address[],uint256[]) (contracts/Basket.sol#170-194)
	- Basket.setNewWeights() (contracts/Basket.sol#196-204)
	- pendingWeights.weights = _weights (contracts/Basket.sol#185)
	Basket.pendingWeights (contracts/Basket.sol#29) can be used in cross function reentrancies:
	- Basket.deleteNewIndex() (contracts/Basket.sol#207-214)
	- Basket.getPendingWeights() (contracts/Basket.sol#49-51)
	- Basket.pendingWeights (contracts/Basket.sol#29)
	- Basket.publishNewIndex(address[],uint256[]) (contracts/Basket.sol#170-194)
	- Basket.setNewWeights() (contracts/Basket.sol#196-204)
	- pendingWeights.block = block.number (contracts/Basket.sol#186)
	Basket.pendingWeights (contracts/Basket.sol#29) can be used in cross function reentrancies:
	- Basket.deleteNewIndex() (contracts/Basket.sol#207-214)
	- Basket.getPendingWeights() (contracts/Basket.sol#49-51)
	- Basket.pendingWeights (contracts/Basket.sol#29)
	- Basket.publishNewIndex(address[],uint256[]) (contracts/Basket.sol#170-194)
	- Basket.setNewWeights() (contracts/Basket.sol#196-204)

   - Recommendation: No specific recommendation provided.

12. **unused-return**
   - Contract: Basket
   - Severity: Medium
   - Confidence: Medium
   - Line: 224
   - Description: Basket.approveUnderlying(address) (contracts/Basket.sol#224-228) ignores return value by IERC20(tokens[i]).approve(spender,type()(uint256).max) (contracts/Basket.sol#226)

   - Recommendation: No specific recommendation provided.

13. **boolean-equal**
   - Contract: Basket
   - Severity: Informational
   - Confidence: High
   - Line: 207
   - Description: Basket.deleteNewIndex() (contracts/Basket.sol#207-214) compares to a boolean constant:
	-require(bool)(auction.auctionOngoing() == false) (contracts/Basket.sol#209)

   - Recommendation: No specific recommendation provided.

14. **solc-version**
   - Contract: Basket
   - Severity: Informational
   - Confidence: High
   - Line: 1
   - Description: Version constraint =0.8.7 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- VerbatimInvalidDeduplication
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationChangeInInternalOverride
	- NestedCalldataArrayAbiReencodingSizeValidation
	- SignedImmutables.
It is used by:
	- =0.8.7 (contracts/Auction.sol#1)
	- =0.8.7 (contracts/Basket.sol#1)
	- =0.8.7 (contracts/Factory.sol#1)
	- =0.8.7 (contracts/interfaces/IAuction.sol#1)
	- =0.8.7 (contracts/interfaces/IBasket.sol#1)
	- =0.8.7 (contracts/interfaces/IFactory.sol#1)
	- =0.8.7 (contracts/test/TestToken.sol#1)

   - Recommendation: No specific recommendation provided.

15. **naming-convention**
   - Contract: Basket
   - Severity: Informational
   - Confidence: High
   - Line: 170
   - Description: Parameter Basket.publishNewIndex(address[],uint256[])._weights (contracts/Basket.sol#170) is not in mixedCase

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **calls-loop**
   - Contract: Basket
   - Severity: Low
   - Confidence: Medium
   - Line: 224
   - Description: Basket.approveUnderlying(address) (contracts/Basket.sol#224-228) has external calls inside a loop: IERC20(tokens[i]).approve(spender,type()(uint256).max) (contracts/Basket.sol#226)
	Calls stack containing the loop:
		Basket.setNewWeights()

   - Recommendation: No specific recommendation provided.

2. **reentrancy-events**
   - Contract: Basket
   - Severity: Low
   - Confidence: Medium
   - Line: 170
   - Description: Reentrancy in Basket.publishNewIndex(address[],uint256[]) (contracts/Basket.sol#170-194):
	External calls:
	- auction.startAuction() (contracts/Basket.sol#176)
	Event emitted after the call(s):
	- PublishedNewIndex(publisher) (contracts/Basket.sol#178)

   - Recommendation: No specific recommendation provided.

3. **timestamp**
   - Contract: Basket
   - Severity: Low
   - Confidence: Medium
   - Line: 110
   - Description: Basket.handleFees() (contracts/Basket.sol#110-129) uses timestamp for comparisons
	Dangerous comparisons:
	- lastFee == 0 (contracts/Basket.sol#111)

   - Recommendation: No specific recommendation provided.
