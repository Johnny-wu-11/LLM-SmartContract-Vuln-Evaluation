# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 5
- Retained Findings: 3
- Filtered Out: 2
- Total Reduction Rate: 40.00%
- False Positive Rate: 40.00%

## Confirmed Findings

1. **Potential Denial of Service**
   - Contract: EmergencyGovernable
   - Severity: Medium
   - Description: Potential Denial of Service
   - Recommendation: Review and optimize loops or external calls that can be used to disrupt availability. Consider adding conditions to manage resource-intensive operations.

## Plausible But Unverified Findings

1. **Incorrect Interface Function Signatures**
   - Contract: EmergencyGovernable
   - Severity: Medium
   - Description: Incorrect Interface Function Signatures
   - Recommendation: Verify that all interface function signatures match their implementations. Adjust any mismatches to ensure compatibility.

2. **Reentrancy Consideration**
   - Contract: EmergencyGovernable
   - Severity: Medium
   - Description: Reentrancy Consideration
   - Recommendation: Implement reentrancy guards such as the 'checks-effects-interactions' pattern or the 'ReentrancyGuard' modifier to prevent state changes during external calls.

## Unsupported Or False Positive

1. **reentrancy-benign**
   - Contract: EmergencyGovernable
   - Severity: Low
   - Confidence: Medium
   - Line: 73
   - Description: Reentrancy in Swap.setFeeRecipient(address) (contracts/swap/Swap.sol#73-76):
	External calls:
	- onlyTimelock() (contracts/swap/Swap.sol#73)
		- require(bool,string)(msg.sender == governor().timelock(),Only governor may call this function.) (contracts/governance/EmergencyGovernable.sol#33-36)
	State
   - Recommendation: No specific recommendation provided.

2. **reentrancy-events**
   - Contract: EmergencyGovernable
   - Severity: Low
   - Confidence: Medium
   - Line: 73
   - Description: Reentrancy in Swap.setFeeRecipient(address) (contracts/swap/Swap.sol#73-76):
	External calls:
	- onlyTimelock() (contracts/swap/Swap.sol#73)
		- require(bool,string)(msg.sender == governor().timelock(),Only governor may call this function.) (contracts/governance/EmergencyGovernable.sol#33-36)
	Event
   - Recommendation: No specific recommendation provided.
