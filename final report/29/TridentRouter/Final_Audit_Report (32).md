# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 16
- Retained Findings: 13
- Filtered Out: 3
- Total Reduction Rate: 18.75%
- False Positive Rate: 18.75%

## Confirmed Findings

1. **Unchecked External Calls**
   - Contract: TridentRouter
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Add checks for the success of external calls and handle failures gracefully.

2. **Denial of Service (DoS)**
   - Contract: TridentRouter
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Implement gas limits and checks on inputs to prevent potential DoS vectors.

3. **Reentrancy Attacks**
   - Contract: TridentRouter
   - Severity: Medium
   - Description: Reentrancy Attacks
   - Recommendation: Use the Checks-Effects-Interactions pattern to secure against reentrancy.

4. **Unprotected Functions**
   - Contract: TridentRouter
   - Severity: Medium
   - Description: Unprotected Functions
   - Recommendation: Add access control modifiers to restrict function execution to authorized users.

## Plausible But Unverified Findings

1. **Slippage Assumptions**
   - Contract: TridentRouter
   - Severity: Medium
   - Description: Slippage Assumptions
   - Recommendation: Ensure slippage is calculated and handled accurately to protect user funds.

2. **Timestamp Dependence**
   - Contract: TridentRouter
   - Severity: Medium
   - Description: Timestamp Dependence
   - Recommendation: Avoid reliance on block timestamps for critical logic; consider using block.number.

3. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: TridentRouter
   - Severity: HIGH
   - Line: 196
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Improve validation in the price calculation to guard against manipulation.

4. **reentrancy-eth**
   - Contract: TridentRouter
   - Severity: High
   - Confidence: Medium
   - Line: 270
   - Description: Reentrancy in TridentRouter.tridentMintCallback(bytes) (contracts/TridentRouter.sol#270-283):
	External calls:
	- _depositFromUserToBentoBox(tokenInput[i].token,cachedMsgSender,msg.sender,tokenInput[i].amount) (contracts/TridentRouter.sol#276)
		- bento.deposit{value: underlyingAmount}(address(0),ad
   - Recommendation: Reorder code to follow the Checks-Effects-Interactions pattern to mitigate reentrancy.

5. **reentrancy-no-eth**
   - Contract: TridentRouter
   - Severity: Medium
   - Confidence: Medium
   - Line: 57
   - Description: Reentrancy in TridentRouter.exactInput(ITridentRouter.ExactInputParams) (contracts/TridentRouter.sol#57-72):
	External calls:
	- bento.transfer(params.tokenIn,msg.sender,params.path[0].pool,params.amountIn) (contracts/TridentRouter.sol#59)
	- amountOut = IPool(params.path[i].pool).swap(params.path[i
   - Recommendation: Secure against reentrancy by updating state variables before external calls.

6. **unused-return**
   - Contract: TridentRouter
   - Severity: Medium
   - Confidence: Medium
   - Line: 136
   - Description: TridentRouter.complexPath(ITridentRouter.ComplexPathParams) (contracts/TridentRouter.sol#136-166) ignores return value by IPool(params.initialPath[i].pool).swap(params.initialPath[i].data) (contracts/TridentRouter.sol#146)

   - Recommendation: Handle return values of external calls to ensure they succeed as expected.

7. **costly-loop**
   - Contract: TridentRouter
   - Severity: Informational
   - Confidence: Medium
   - Line: 79
   - Description: TridentRouter.exactInputLazy(uint256,ITridentRouter.Path[]) (contracts/TridentRouter.sol#79-96) has costly operations inside a loop:
	- cachedMsgSender = msg.sender (contracts/TridentRouter.sol#86)

   - Recommendation: Move constant operations outside the loop to optimize gas usage.

8. **solc-version**
   - Contract: TridentRouter
   - Severity: Informational
   - Confidence: High
   - Line: 3
   - Description: Version constraint >=0.8.0 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCh
   - Recommendation: Upgrade the Solidity compiler version to the latest stable release.

9. **missing-inheritance**
   - Contract: TridentRouter
   - Severity: Informational
   - Confidence: High
   - Line: 14
   - Description: TridentRouter (contracts/TridentRouter.sol#14-359) should inherit from ITridentCallee (contracts/interfaces/ITridentCallee.sol#6-10)

   - Recommendation: Ensure that the contract properly inherits interfaces to maintain expected behavior.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: TridentRouter
   - Severity: Low
   - Confidence: Medium
   - Line: 195
   - Description: TridentRouter.addLiquidityLazy(address,uint256,bytes).pool (contracts/TridentRouter.sol#195) lacks a zero-check on :
		- cachedPool = pool (contracts/TridentRouter.sol#201)

   - Recommendation: No specific recommendation provided.

2. **calls-loop**
   - Contract: TridentRouter
   - Severity: Low
   - Confidence: Medium
   - Line: 335
   - Description: TridentRouter._depositFromUserToBentoBox(address,address,address,uint256) (contracts/TridentRouter.sol#335-351) has external calls inside a loop: bento.deposit(token,sender,recipient,0,amount) (contracts/TridentRouter.sol#350)
	Calls stack containing the loop:
		TridentRouter.tridentMintCallback(byt
   - Recommendation: No specific recommendation provided.

3. **reentrancy-benign**
   - Contract: TridentRouter
   - Severity: Low
   - Confidence: Medium
   - Line: 194
   - Description: Reentrancy in TridentRouter.addLiquidityLazy(address,uint256,bytes) (contracts/TridentRouter.sol#194-207):
	External calls:
	- liquidity = IPool(pool).mint(data) (contracts/TridentRouter.sol#203)
	State variables written after the call(s):
	- cachedMsgSender = address(1) (contracts/TridentRouter.sol
   - Recommendation: No specific recommendation provided.
