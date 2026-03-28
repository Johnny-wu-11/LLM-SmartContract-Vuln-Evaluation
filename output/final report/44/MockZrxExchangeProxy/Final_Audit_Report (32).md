# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 8
- Retained Findings: 8
- Filtered Out: 0
- Total Reduction Rate: 0.00%
- False Positive Rate: 0.00%

## Confirmed Findings

1. **Malicious Functions detected.**
   - Contract: MockZrxExchangeProxy
   - Severity: Medium
   - Description: Malicious Functions detected.
   - Recommendation: Review the functions for any unauthorized operations or logic that might lead to exploits.

2. **Lack of Access Control.**
   - Contract: MockZrxExchangeProxy
   - Severity: Medium
   - Description: Lack of Access Control.
   - Recommendation: Implement access modifiers like 'onlyOwner' to restrict critical function executions.

3. **Reentrancy Vulnerability.**
   - Contract: MockZrxExchangeProxy
   - Severity: Medium
   - Description: Reentrancy Vulnerability.
   - Recommendation: Use modifiers like 'nonReentrant' or checks-effects-interactions pattern to prevent reentrancy.

## Plausible But Unverified Findings

1. **Transfer of Tokens Without Checking Success.**
   - Contract: MockZrxExchangeProxy
   - Severity: Medium
   - Description: Transfer of Tokens Without Checking Success.
   - Recommendation: Ensure that token transfers check the return value to confirm the success of the operation.

2. **Lack of Input Validation.**
   - Contract: MockZrxExchangeProxy
   - Severity: Medium
   - Description: Lack of Input Validation.
   - Recommendation: Add validation for function inputs to prevent invalid data from being processed.

3. **Fallback and Receive Functions are insecure.**
   - Contract: MockZrxExchangeProxy
   - Severity: Medium
   - Description: Fallback and Receive Functions are insecure.
   - Recommendation: Use a fallback function that limits access or reverts unless specific criteria are met.

4. **unchecked-transfer**
   - Contract: MockZrxExchangeProxy
   - Severity: High
   - Confidence: Medium
   - Line: 37
   - Description: MockZrxExchangeProxy.sellToUniswap2(address[],uint256,uint256,bool) (contracts/test/MockZrxExchangeProxy.sol#37-41) ignores return value by IERC20(_1[1]).transfer(msg.sender,1000000000000000000000) (contracts/test/MockZrxExchangeProxy.sol#40)

   - Recommendation: Check the return value of 'IERC20.transfer' to ensure successful execution and prevent silent failures.

5. **naming-convention**
   - Contract: MockZrxExchangeProxy
   - Severity: Informational
   - Confidence: High
   - Line: 53
   - Description: Parameter MockZrxExchangeProxy.sellToUniswap4(address[],uint256,uint256,bool)._2 (contracts/test/MockZrxExchangeProxy.sol#53) is not in mixedCase

   - Recommendation: Rename parameters to follow mixedCase to improve code readability and maintain consistency.

## Unsupported Or False Positive

None
