# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 13
- Retained Findings: 9
- Filtered Out: 4
- Total Reduction Rate: 30.77%
- False Positive Rate: 30.77%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: Visor
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Add checks-effects-interactions pattern and reentrancy guards to protect external call functions.

2. **Gas Limit in Rage Quit**
   - Contract: Visor
   - Severity: Medium
   - Description: Gas Limit in Rage Quit
   - Recommendation: Explicitly define and document gas limits for critical functions and ensure they are sufficient for all expected operations.

3. **Unchecked External Calls**
   - Contract: Visor
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Check the return values of all external calls and handle potential errors gracefully.

4. **Access Control**
   - Contract: Visor
   - Severity: Medium
   - Description: Access Control
   - Recommendation: Ensure proper access control is implemented using modifiers or require statements to restrict function access.

5. **Timestamp Dependence**
   - Contract: Visor
   - Severity: Medium
   - Description: Timestamp Dependence
   - Recommendation: Avoid using block timestamps for critical logic; consider using block numbers or other stable values.

6. **MWE-203: Approval Not Revoked**
   - Contract: Visor
   - Severity: HIGH
   - Line: 495
   - Description: Approval is not revoked or reset after the code functionality finishes.
   - Recommendation: Revoke or reset token approvals immediately after they are no longer needed to minimize security risks.

7. **unchecked-transfer**
   - Contract: Visor
   - Severity: High
   - Confidence: Medium
   - Line: 583
   - Description: Visor.timeLockERC20(address,address,uint256,uint256) (contracts/visor/Visor.sol#583-612) ignores return value by IERC20(token).transferFrom(msg.sender,address(this),amount) (contracts/visor/Visor.sol#610)

   - Recommendation: Ensure that the return value of the IERC20 transferFrom function is checked and handled properly.

8. **naming-convention**
   - Contract: Visor
   - Severity: Informational
   - Confidence: High
   - Line: 400
   - Description: Parameter Visor.setURI(string)._uri (contracts/visor/Visor.sol#400) is not in mixedCase

   - Recommendation: Rename variables to follow the mixedCase naming convention to enhance code readability and consistency.

9. **too-many-digits**
   - Contract: Visor
   - Severity: Informational
   - Confidence: Medium
   - Line: 27
   - Description: Visor.slitherConstructorConstantVariables() (contracts/visor/Visor.sol#27-641) uses literals with too many digits:
	- RAGEQUIT_GAS = 500000 (contracts/visor/Visor.sol#50)

   - Recommendation: Consider reducing the literal size or document the rationale behind choosing such large values for understanding.

## Unsupported Or False Positive

1. **calls-loop**
   - Contract: Visor
   - Severity: Low
   - Confidence: Medium
   - Line: 212
   - Description: Visor.checkBalances() (contracts/visor/Visor.sol#212-223) has external calls inside a loop: IERC20(_lockData.token).balanceOf(address(this)) < _lockData.balance (contracts/visor/Visor.sol#219)

   - Recommendation: No specific recommendation provided.

2. **reentrancy-benign**
   - Contract: Visor
   - Severity: Low
   - Confidence: Medium
   - Line: 364
   - Description: Reentrancy in Visor.rageQuit(address,address) (contracts/visor/Visor.sol#364-398):
	External calls:
	- IRageQuit(delegate).rageQuit{gas: RAGEQUIT_GAS}() (contracts/visor/Visor.sol#382-389)
	State variables written after the call(s):
	- delete _locks[lockID] (contracts/visor/Visor.sol#394)

   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: Visor
   - Severity: Low
   - Confidence: Medium
   - Line: 619
   - Description: Reentrancy in Visor.timeUnlockERC20(address,address,uint256,uint256) (contracts/visor/Visor.sol#619-639):
	External calls:
	- TransferHelper.safeTransfer(token,recipient,amount) (contracts/visor/Visor.sol#637)
	Event emitted after the call(s):
	- TimeUnlockERC20(recipient,token,amount,expires) (cont
   - Recommendation: No specific recommendation provided.

4. **timestamp**
   - Contract: Visor
   - Severity: Low
   - Confidence: Medium
   - Line: 495
   - Description: Visor.transferERC721(address,address,uint256) (contracts/visor/Visor.sol#495-516) uses timestamp for comparisons
	Dangerous comparisons:
	- require(bool,string)(timelockERC721s[timelockERC721Keys[nftContract][i]].expires <= block.timestamp,NFT locked and not expired) (contracts/visor/Visor.sol#506-5
   - Recommendation: No specific recommendation provided.
