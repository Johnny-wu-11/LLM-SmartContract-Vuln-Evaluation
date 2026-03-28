# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 17
- Retained Findings: 14
- Filtered Out: 3
- Total Reduction Rate: 17.65%
- False Positive Rate: 17.65%

## Confirmed Findings

1. **Reentrancy Vulnerability**
   - Contract: Auction
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Implement a reentrancy guard or use checks-effects-interactions pattern to prevent reentrant calls.

2. **Potential Denial of Service**
   - Contract: Auction
   - Severity: Medium
   - Description: Potential Denial of Service
   - Recommendation: Ensure that external calls do not block execution or control flow. Consider using gas limits or splitting operations.

## Plausible But Unverified Findings

1. **Lack of Access Control**
   - Contract: Auction
   - Severity: Medium
   - Description: Lack of Access Control
   - Recommendation: Incorporate role-based access control to restrict function access to authorized accounts only.

2. **Integer Overflow/Underflow**
   - Contract: Auction
   - Severity: Medium
   - Description: Integer Overflow/Underflow
   - Recommendation: Ensure arithmetic operations are safe by using SafeMath libraries or Solidity 0.8.0 and above.

3. **Bond Amount Calculation**
   - Contract: Auction
   - Severity: Medium
   - Description: Bond Amount Calculation
   - Recommendation: Validate bond calculations to avoid precision errors and ensure correct bond amounts are used.

4. **Timestamp Dependence**
   - Contract: Auction
   - Severity: Medium
   - Description: Timestamp Dependence
   - Recommendation: Use block numbers instead of timestamps for time-dependent logic to avoid manipulation.

5. **Bounty Management**
   - Contract: Auction
   - Severity: Medium
   - Description: Bounty Management
   - Recommendation: Verify bounty calculations and transfers to ensure correctness and that funds are safeguarded.

6. **arbitrary-send-erc20**
   - Contract: Auction
   - Severity: High
   - Confidence: High
   - Line: 69
   - Description: Auction.settleAuction(uint256[],address[],uint256[],address[],uint256[]) (contracts/Auction.sol#69-109) uses arbitrary from in transferFrom: IERC20(outputTokens[i_scope_0]).safeTransferFrom(address(basket),msg.sender,outputWeights[i_scope_0]) (contracts/Auction.sol#86)

   - Recommendation: Ensure that only authorized addresses can initiate token transfers and validate input addresses.

7. **unchecked-transfer**
   - Contract: Auction
   - Severity: High
   - Confidence: Medium
   - Line: 140
   - Description: Auction.withdrawBounty(uint256[]) (contracts/Auction.sol#140-151) ignores return value by IERC20(bounty.token).transfer(msg.sender,bounty.amount) (contracts/Auction.sol#146)

   - Recommendation: Check the return value of the transfer function to ensure successful token transfers.

8. **reentrancy-no-eth**
   - Contract: Auction
   - Severity: Medium
   - Confidence: Medium
   - Line: 54
   - Description: Reentrancy in Auction.bondForRebalance() (contracts/Auction.sol#54-67):
	External calls:
	- basketToken.safeTransferFrom(msg.sender,address(this),bondAmount) (contracts/Auction.sol#62)
	State variables written after the call(s):
	- hasBonded = true (contracts/Auction.sol#63)
	Auction.hasBonded (cont
   - Recommendation: Apply reentrancy protection or finalize state changes before external calls are made.

9. **unused-return**
   - Contract: Auction
   - Severity: Medium
   - Confidence: Medium
   - Line: 69
   - Description: Auction.settleAuction(uint256[],address[],uint256[],address[],uint256[]) (contracts/Auction.sol#69-109) ignores return value by basket.updateIBRatio(newRatio) (contracts/Auction.sol#104)

   - Recommendation: Check and handle the return value of updateIBRatio to ensure it executes successfully.

10. **boolean-equal**
   - Contract: Auction
   - Severity: Informational
   - Confidence: High
   - Line: 34
   - Description: Auction.startAuction() (contracts/Auction.sol#34-41) compares to a boolean constant:
	-require(bool,string)(auctionOngoing == false,ongoing auction) (contracts/Auction.sol#35)

   - Recommendation: Simplify boolean comparison by using `!auctionOngoing` instead of `auctionOngoing == false`.

11. **solc-version**
   - Contract: Auction
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

12. **unused-state**
   - Contract: Auction
   - Severity: Informational
   - Confidence: High
   - Line: 14
   - Description: Auction.BLOCK_DECREMENT (contracts/Auction.sol#14) is never used in Auction (contracts/Auction.sol#9-153)

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **calls-loop**
   - Contract: Auction
   - Severity: Low
   - Confidence: Medium
   - Line: 69
   - Description: Auction.settleAuction(uint256[],address[],uint256[],address[],uint256[]) (contracts/Auction.sol#69-109) has external calls inside a loop: tokensNeeded = basketAsERC20.totalSupply() * pendingWeights[i_scope_1] * newRatio / BASE / BASE (contracts/Auction.sol#97)

   - Recommendation: No specific recommendation provided.

2. **reentrancy-benign**
   - Contract: Auction
   - Severity: Low
   - Confidence: Medium
   - Line: 111
   - Description: Reentrancy in Auction.bondBurn() (contracts/Auction.sol#111-124):
	External calls:
	- basket.auctionBurn(bondAmount) (contracts/Auction.sol#116)
	- basket.deleteNewIndex() (contracts/Auction.sol#119)
	State variables written after the call(s):
	- auctionBonder = address(0) (contracts/Auction.sol#123
   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: Auction
   - Severity: Low
   - Confidence: Medium
   - Line: 126
   - Description: Reentrancy in Auction.addBounty(IERC20,uint256) (contracts/Auction.sol#126-138):
	External calls:
	- token.safeTransferFrom(msg.sender,address(this),amount) (contracts/Auction.sol#128)
	Event emitted after the call(s):
	- BountyAdded(token,amount,id) (contracts/Auction.sol#136)

   - Recommendation: No specific recommendation provided.
