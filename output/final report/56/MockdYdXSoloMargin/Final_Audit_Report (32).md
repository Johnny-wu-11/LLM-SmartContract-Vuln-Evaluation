# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 6
- Retained Findings: 5
- Filtered Out: 1
- Total Reduction Rate: 16.67%
- False Positive Rate: 16.67%

## Confirmed Findings

1. **Reentrancy Vulnerability**
   - Contract: MIMConvexStrategy
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Ensure state changes are completed before making external calls or use reentrancy guards like OpenZeppelin's ReentrancyGuard.

## Plausible But Unverified Findings

1. **Lack of Access Control**
   - Contract: MIMConvexStrategy
   - Severity: Medium
   - Description: Lack of Access Control
   - Recommendation: Implement role-based access control using OpenZeppelin's AccessControl library to restrict function accessibility.

2. **arbitrary-send-erc20**
   - Contract: MockdYdXSoloMargin
   - Severity: High
   - Confidence: High
   - Line: 71
   - Description: MockdYdXSoloMargin._deposit(Actions.DepositArgs) (contracts/mock/MockdYdXSoloMargin.sol#71-87) uses arbitrary from in transferFrom: IERC20(tokens[args.market]).safeTransferFrom(args.from,address(this),args.amount.value) (contracts/mock/MockdYdXSoloMargin.sol#83)

   - Recommendation: Ensure the 'from' address is verified to prevent unauthorized token transfers.

3. **reentrancy-no-eth**
   - Contract: MockdYdXSoloMargin
   - Severity: Medium
   - Confidence: Medium
   - Line: 89
   - Description: Reentrancy in MockdYdXSoloMargin._withdraw(Actions.WithdrawArgs) (contracts/mock/MockdYdXSoloMargin.sol#89-104):
	External calls:
	- IERC20(tokens[args.market]).safeTransfer(args.to,args.amount.value) (contracts/mock/MockdYdXSoloMargin.sol#100)
	State variables written after the call(s):
	- balances
   - Recommendation: Move state variable updates to occur before external calls or use a mutex pattern to prevent reentrancy.

4. **solc-version**
   - Contract: MockdYdXSoloMargin
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint ^0.6.2 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- NestedCalldataArrayAbiReencodingSizeValidation
	- ABIDecodeTwoDimension
   - Recommendation: Upgrade the Solidity compiler version to at least 0.6.12 to avoid known vulnerabilities.

## Unsupported Or False Positive

1. **reentrancy-benign**
   - Contract: MockdYdXSoloMargin
   - Severity: Low
   - Confidence: Medium
   - Line: 71
   - Description: Reentrancy in MockdYdXSoloMargin._deposit(Actions.DepositArgs) (contracts/mock/MockdYdXSoloMargin.sol#71-87):
	External calls:
	- IERC20(tokens[args.market]).safeTransferFrom(args.from,address(this),args.amount.value) (contracts/mock/MockdYdXSoloMargin.sol#83)
	State variables written after the call
   - Recommendation: No specific recommendation provided.
