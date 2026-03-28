# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 10
- Retained Findings: 7
- Filtered Out: 3
- Total Reduction Rate: 30.00%
- False Positive Rate: 30.00%

## Confirmed Findings

1. **Require Statements**
   - Contract: Factory
   - Severity: Medium
   - Description: Require Statements
   - Recommendation: Ensure that all require statements have clear and specific conditions and revert messages. Improve condition checks to prevent unintended code execution.

## Plausible But Unverified Findings

1. **Proposal Array Access**
   - Contract: Factory
   - Severity: Medium
   - Description: Proposal Array Access
   - Recommendation: Implement boundary checks before accessing array elements to prevent out-of-bounds errors. Validate inputs to ensure they fall within expected ranges.

2. **Reentrancy**
   - Contract: Factory
   - Severity: Medium
   - Description: Reentrancy
   - Recommendation: Use checks-effects-interactions pattern to prevent reentrancy issues. Consider using reentrancy guards via OpenZeppelin's ReentrancyGuard.

3. **Constructor Parameters**
   - Contract: Factory
   - Severity: Medium
   - Description: Constructor Parameters
   - Recommendation: Validate constructor parameters thoroughly to ensure contract initialization is secure. Avoid using externally controlled inputs without checks.

4. **reentrancy-no-eth**
   - Contract: Factory
   - Severity: Medium
   - Confidence: Medium
   - Line: 93
   - Description: Reentrancy in Factory.createBasket(uint256) (contracts/Factory.sol#93-116):
	External calls:
	- newAuction.initialize(address(newBasket),address(this)) (contracts/Factory.sol#100)
	- newBasket.initialize(bProposal,newAuction) (contracts/Factory.sol#101)
	- token.safeTransferFrom(msg.sender,address(t
   - Recommendation: Analyze and order external calls in the function carefully. Implement reentrancy guards and ensure no state changes occur after external calls.

5. **solc-version**
   - Contract: Factory
   - Severity: Informational
   - Confidence: High
   - Line: 1
   - Description: Version constraint =0.8.7 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- VerbatimInvalidDeduplication
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesA
   - Recommendation: Upgrade to the latest stable version of Solidity to mitigate potential known issues. Regularly review and apply compiler updates.

6. **immutable-states**
   - Contract: Factory
   - Severity: Optimization
   - Confidence: High
   - Line: 27
   - Description: Factory.basketImpl (contracts/Factory.sol#27) should be immutable 

   - Recommendation: Declare basketImpl as immutable to optimize gas efficiency. Use the appropriate syntax to set its value during contract deployment.

## Unsupported Or False Positive

1. **shadowing-local**
   - Contract: Factory
   - Severity: Low
   - Confidence: High
   - Line: 77
   - Description: Factory.proposeBasketLicense(uint256,string,string,address[],uint256[]).proposal (contracts/Factory.sol#77-85) shadows:
	- Factory.proposal(uint256) (contracts/Factory.sol#35-37) (function)
	- IFactory.proposal(uint256) (contracts/interfaces/IFactory.sol#23) (function)

   - Recommendation: No specific recommendation provided.

2. **events-maths**
   - Contract: Factory
   - Severity: Low
   - Confidence: Medium
   - Line: 39
   - Description: Factory.setMinLicenseFee(uint256) (contracts/Factory.sol#39-41) should emit an event for: 
	- minLicenseFee = newMinLicenseFee (contracts/Factory.sol#40) 

   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: Factory
   - Severity: Low
   - Confidence: Medium
   - Line: 93
   - Description: Reentrancy in Factory.createBasket(uint256) (contracts/Factory.sol#93-116):
	External calls:
	- newAuction.initialize(address(newBasket),address(this)) (contracts/Factory.sol#100)
	- newBasket.initialize(bProposal,newAuction) (contracts/Factory.sol#101)
	- token.safeTransferFrom(msg.sender,address(t
   - Recommendation: No specific recommendation provided.
