# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 14
- Retained Findings: 9
- Filtered Out: 5
- Total Reduction Rate: 35.71%
- False Positive Rate: 35.71%

## Confirmed Findings

1. **Unrestricted Access to Critical Functions**
   - Contract: TracerPerpetualSwaps
   - Severity: Medium
   - Description: Unrestricted Access to Critical Functions
   - Recommendation: Implement role-based access control to restrict access to critical functions.

2. **Reentrancy Attack Vulnerability**
   - Contract: TracerPerpetualSwaps
   - Severity: Medium
   - Description: Reentrancy Attack Vulnerability
   - Recommendation: Use the Checks-Effects-Interactions pattern to prevent reentrant calls.

3. **Oracle Manipulation Risk**
   - Contract: TracerPerpetualSwaps
   - Severity: Medium
   - Description: Oracle Manipulation Risk
   - Recommendation: Validate oracle data with time-weighted averages or additional off-chain sources.

## Plausible But Unverified Findings

1. **Potential ERC20 Token Withdrawal Misuse**
   - Contract: TracerPerpetualSwaps
   - Severity: Medium
   - Description: Potential ERC20 Token Withdrawal Misuse
   - Recommendation: Verify correct token amounts and recipient addresses during withdrawals.

2. **DoS Attack from External Oracle Dependence**
   - Contract: TracerPerpetualSwaps
   - Severity: Medium
   - Description: DoS Attack from External Oracle Dependence
   - Recommendation: Implement fallback mechanisms to handle oracle failures gracefully.

3. **MWE-209: Wrong Order for Interest or ExchangeRate**
   - Contract: TracerPerpetualSwaps
   - Severity: HIGH
   - Line: 216
   - Description: Update of interest or exchange rate should be executed before calculating new balance, share, stake, loan or fee.
   - Recommendation: Ensure interest and exchange rates are updated before balance calculations.

4. **unchecked-transfer**
   - Contract: TracerPerpetualSwaps
   - Severity: High
   - Confidence: Medium
   - Line: 508
   - Description: TracerPerpetualSwaps.withdrawFees() (contracts/TracerPerpetualSwaps.sol#508-516) ignores return value by IERC20(tracerQuoteToken).transfer(feeReceiver,tempFees) (contracts/TracerPerpetualSwaps.sol#514)

   - Recommendation: Check the return value of the transfer function to ensure successful execution.

5. **reentrancy-no-eth**
   - Contract: TracerPerpetualSwaps
   - Severity: Medium
   - Confidence: Medium
   - Line: 142
   - Description: Reentrancy in TracerPerpetualSwaps.deposit(uint256) (contracts/TracerPerpetualSwaps.sol#142-164):
	External calls:
	- IERC20(tracerQuoteToken).transferFrom(msg.sender,address(this),rawTokenAmount) (contracts/TracerPerpetualSwaps.sol#151)
	State variables written after the call(s):
	- userBalance.pos
   - Recommendation: Reorder state updates to occur before making external calls to prevent reentrancy.

6. **naming-convention**
   - Contract: TracerPerpetualSwaps
   - Severity: Informational
   - Confidence: High
   - Line: 560
   - Description: Parameter TracerPerpetualSwaps.setDeleveragingCliff(uint256)._deleveragingCliff (contracts/TracerPerpetualSwaps.sol#560) is not in mixedCase

   - Recommendation: Rename the parameter to use mixedCase naming for consistency.

## Unsupported Or False Positive

1. **events-access**
   - Contract: TracerPerpetualSwaps
   - Severity: Low
   - Confidence: Medium
   - Line: 522
   - Description: TracerPerpetualSwaps.setLiquidationContract(address) (contracts/TracerPerpetualSwaps.sol#522-525) should emit an event for: 
	- liquidationContract = _liquidationContract (contracts/TracerPerpetualSwaps.sol#524) 

   - Recommendation: No specific recommendation provided.

2. **events-maths**
   - Contract: TracerPerpetualSwaps
   - Severity: Low
   - Confidence: Medium
   - Line: 568
   - Description: TracerPerpetualSwaps.setInsurancePoolSwitchStage(uint256) (contracts/TracerPerpetualSwaps.sol#568-570) should emit an event for: 
	- insurancePoolSwitchStage = _insurancePoolSwitchStage (contracts/TracerPerpetualSwaps.sol#569) 

   - Recommendation: No specific recommendation provided.

3. **missing-zero-check**
   - Contract: TracerPerpetualSwaps
   - Severity: Low
   - Confidence: Medium
   - Line: 100
   - Description: TracerPerpetualSwaps.constructor(bytes32,address,uint256,address,uint256,uint256,uint256,address,uint256,uint256,uint256)._feeReceiver (contracts/TracerPerpetualSwaps.sol#100) lacks a zero-check on :
		- feeReceiver = _feeReceiver (contracts/TracerPerpetualSwaps.sol#113)

   - Recommendation: No specific recommendation provided.

4. **reentrancy-benign**
   - Contract: TracerPerpetualSwaps
   - Severity: Low
   - Confidence: Medium
   - Line: 142
   - Description: Reentrancy in TracerPerpetualSwaps.deposit(uint256) (contracts/TracerPerpetualSwaps.sol#142-164):
	External calls:
	- IERC20(tracerQuoteToken).transferFrom(msg.sender,address(this),rawTokenAmount) (contracts/TracerPerpetualSwaps.sol#151)
	State variables written after the call(s):
	- _updateAccountL
   - Recommendation: No specific recommendation provided.

5. **reentrancy-events**
   - Contract: TracerPerpetualSwaps
   - Severity: Low
   - Confidence: Medium
   - Line: 142
   - Description: Reentrancy in TracerPerpetualSwaps.deposit(uint256) (contracts/TracerPerpetualSwaps.sol#142-164):
	External calls:
	- IERC20(tracerQuoteToken).transferFrom(msg.sender,address(this),rawTokenAmount) (contracts/TracerPerpetualSwaps.sol#151)
	Event emitted after the call(s):
	- Deposit(msg.sender,amount
   - Recommendation: No specific recommendation provided.
