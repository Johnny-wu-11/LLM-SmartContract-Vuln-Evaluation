# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 16
- Retained Findings: 11
- Filtered Out: 5
- Total Reduction Rate: 31.25%
- False Positive Rate: 31.25%

## Confirmed Findings

1. **Unchecked External Call**
   - Contract: Swap
   - Severity: Medium
   - Description: Unchecked External Call
   - Recommendation: Ensure that external calls check return values and handle failures appropriately.

2. **Handling of Allowance**
   - Contract: Swap
   - Severity: Medium
   - Description: Handling of Allowance
   - Recommendation: Validate allowance before executing transfers to prevent misuse.

## Plausible But Unverified Findings

1. **Reentrancy Protection**
   - Contract: Swap
   - Severity: Medium
   - Description: Reentrancy Protection
   - Recommendation: Implement reentrancy guards using mutexes or the checks-effects-interactions pattern.

2. **Gas Limit and Block Gas Limit**
   - Contract: Swap
   - Severity: Medium
   - Description: Gas Limit and Block Gas Limit
   - Recommendation: Explicitly set gas limits for critical operations to avoid hitting block limits.

3. **Minimum Amount Received Check**
   - Contract: Swap
   - Severity: Medium
   - Description: Minimum Amount Received Check
   - Recommendation: Ensure checks guarantee minimum amounts received for transactions to prevent underpayment.

4. **Access Control**
   - Contract: Swap
   - Severity: Medium
   - Description: Access Control
   - Recommendation: Refine access control checks to allow only authorized addresses to execute sensitive operations.

5. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: Swap
   - Severity: HIGH
   - Line: 200
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Implement security mechanisms like TWAP to mitigate flashloan attacks on token values.

6. **arbitrary-send-eth**
   - Contract: Swap
   - Severity: High
   - Confidence: Medium
   - Line: 243
   - Description: Swap.sweepFees(address[]) (contracts/swap/Swap.sol#243-259) sends eth to arbitrary user
	Dangerous calls:
	- feeRecipient.transfer(address(this).balance) (contracts/swap/Swap.sol#257)

   - Recommendation: Replace direct transfers with `call.value()` to handle failures and revert on unsuccessful transfers.

7. **uninitialized-local**
   - Contract: Swap
   - Severity: Medium
   - Confidence: Medium
   - Line: 216
   - Description: Swap.fillZrxQuote(IERC20,address,bytes,uint256).erc20Delta (contracts/swap/Swap.sol#216) is a local variable never initialized

   - Recommendation: Initialize all local variables before use to prevent unexpected computation errors.

8. **low-level-calls**
   - Contract: Swap
   - Severity: Informational
   - Confidence: High
   - Line: 200
   - Description: Low level call in Swap.fillZrxQuote(IERC20,address,bytes,uint256) (contracts/swap/Swap.sol#200-225):
	- (success,None) = zrxTo.call{value: ethAmount}(zrxData) (contracts/swap/Swap.sol#212)

   - Recommendation: Use high-level functions like `transfer()` or `send()` which automatically revert on failure.

9. **reentrancy-unlimited-gas**
   - Contract: Swap
   - Severity: Informational
   - Confidence: Medium
   - Line: 243
   - Description: Reentrancy in Swap.sweepFees(address[]) (contracts/swap/Swap.sol#243-259):
	External calls:
	- feeRecipient.transfer(address(this).balance) (contracts/swap/Swap.sol#257)
	Event emitted after the call(s):
	- FeesSwept(address(0),address(this).balance,feeRecipient) (contracts/swap/Swap.sol#258)

   - Recommendation: Consider introducing reentrancy locks to manage state changes safely post-transfer calls.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: Swap
   - Severity: Low
   - Confidence: Medium
   - Line: 51
   - Description: Swap.constructor(address,address,uint256).feeRecipient_ (contracts/swap/Swap.sol#51) lacks a zero-check on :
		- feeRecipient = feeRecipient_ (contracts/swap/Swap.sol#54)

   - Recommendation: No specific recommendation provided.

2. **calls-loop**
   - Contract: Swap
   - Severity: Low
   - Confidence: Medium
   - Line: 243
   - Description: Swap.sweepFees(address[]) (contracts/swap/Swap.sol#243-259) has external calls inside a loop: balance = IERC20(tokens[i]).balanceOf(address(this)) (contracts/swap/Swap.sol#251)

   - Recommendation: No specific recommendation provided.

3. **reentrancy-benign**
   - Contract: Swap
   - Severity: Low
   - Confidence: Medium
   - Line: 73
   - Description: Reentrancy in Swap.setFeeRecipient(address) (contracts/swap/Swap.sol#73-76):
	External calls:
	- onlyTimelock() (contracts/swap/Swap.sol#73)
		- require(bool,string)(msg.sender == governor().timelock(),Only governor may call this function.) (contracts/governance/EmergencyGovernable.sol#33-36)
	State
   - Recommendation: No specific recommendation provided.

4. **reentrancy-events**
   - Contract: Swap
   - Severity: Low
   - Confidence: Medium
   - Line: 73
   - Description: Reentrancy in Swap.setFeeRecipient(address) (contracts/swap/Swap.sol#73-76):
	External calls:
	- onlyTimelock() (contracts/swap/Swap.sol#73)
		- require(bool,string)(msg.sender == governor().timelock(),Only governor may call this function.) (contracts/governance/EmergencyGovernable.sol#33-36)
	Event
   - Recommendation: No specific recommendation provided.

5. **timestamp**
   - Contract: Swap
   - Severity: Low
   - Confidence: Medium
   - Line: 106
   - Description: Swap.swapByQuote(address,uint256,address,uint256,address,address,bytes,uint256) (contracts/swap/Swap.sol#106-186) uses timestamp for comparisons
	Dangerous comparisons:
	- require(bool,string)(block.timestamp <= deadline,Swap::swapByQuote: Deadline exceeded) (contracts/swap/Swap.sol#116-119)

   - Recommendation: No specific recommendation provided.
