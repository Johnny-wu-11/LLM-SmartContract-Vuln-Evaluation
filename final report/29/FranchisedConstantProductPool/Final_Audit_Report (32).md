# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 21
- Retained Findings: 17
- Filtered Out: 4
- Total Reduction Rate: 19.05%
- False Positive Rate: 19.05%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Ensure that state changes occur before external calls to prevent reentrancy. Consider using a reentrancy guard modifier.

2. **Unchecked External Calls**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Check the return value of all external calls and handle failure cases where necessary.

3. **Denial of Service (DoS)**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Validate user-supplied data and limit the size of computations to mitigate potential DoS vectors.

4. **Gas Limit and Block Timestamp Dependence**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Description: Gas Limit and Block Timestamp Dependence
   - Recommendation: Avoid relying on block timestamps for critical logic, and do not assume a specific gas scenario.

5. **Integer Overflow/Underflow**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Description: Integer Overflow/Underflow
   - Recommendation: Use SafeMath libraries to perform arithmetic operations safely, checking for overflows and underflows.

6. **Lack of Access Control**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Description: Lack of Access Control
   - Recommendation: Implement access control checks using modifiers to restrict function access to authorized accounts.

7. **Frontrunning Vulnerability**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Description: Frontrunning Vulnerability
   - Recommendation: Consider implementing mechanisms like commit-reveal schemes to mitigate frontrunning risks.

8. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: FranchisedConstantProductPool
   - Severity: HIGH
   - Line: 272
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Ensure LP token values are accurately calculated by using tamper-proof oracles and checks against manipulation.

9. **weak-prng**
   - Contract: FranchisedConstantProductPool
   - Severity: High
   - Confidence: Medium
   - Line: 281
   - Description: FranchisedConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/franchised/FranchisedConstantProductPool.sol#281-309) uses a weak PRNG: "blockTimestamp = uint32(block.timestamp % 2 ** 32) (contracts/pool/franchised/FranchisedConstantProductPool.sol#294)" 

   - Recommendation: Replace weak PRNG with a cryptographically secure randomness source for critical operations.

10. **divide-before-multiply**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 281
   - Description: FranchisedConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/franchised/FranchisedConstantProductPool.sol#281-309) performs a multiplication on the result of a division:
	- price0 = (uint256(_reserve1) << PRECISION) / _reserve0 (contracts/pool/franchised/FranchisedCo
   - Recommendation: Reorder operations to perform multiplication before division to maintain precision and accuracy.

11. **incorrect-equality**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Confidence: High
   - Line: 90
   - Description: FranchisedConstantProductPool.mint(bytes) (contracts/pool/franchised/FranchisedConstantProductPool.sol#90-118) uses a dangerous strict equality:
	- _totalSupply == 0 (contracts/pool/franchised/FranchisedConstantProductPool.sol#106)

   - Recommendation: No specific recommendation provided.

12. **reentrancy-no-eth**
   - Contract: FranchisedConstantProductPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 223
   - Description: Reentrancy in FranchisedConstantProductPool.flashSwap(bytes) (contracts/pool/franchised/FranchisedConstantProductPool.sol#223-250):
	External calls:
	- _transfer(token0,amountOut,recipient,unwrapBento) (contracts/pool/franchised/FranchisedConstantProductPool.sol#242)
		- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMinimal.withdraw.selector,token,address(this),to,0,shares)) (contracts/pool/franchised/FranchisedConstantProductPool.sol#346)
		- (success_scope_0,None) = bento.call(abi.encodeWithSelector(IBentoBoxMinimal.transfer.selector,token,address(this),to,shares)) (contracts/pool/franchised/FranchisedConstantProductPool.sol#349)
	- ITridentCallee(msg.sender).tridentSwapCallback(context) (contracts/pool/franchised/FranchisedConstantProductPool.sol#243)
	State variables written after the call(s):
	- _update(balance0_scope_0,balance1_scope_1,_reserve0,_reserve1,_blockTimestampLast) (contracts/pool/franchised/FranchisedConstantProductPool.sol#246)
		- blockTimestampLast = blockTimestamp (contracts/pool/franchised/FranchisedConstantProductPool.sol#306)
	FranchisedConstantProductPool.blockTimestampLast (contracts/pool/franchised/FranchisedConstantProductPool.sol#42) can be used in cross function reentrancies:
	- FranchisedConstantProductPool._getReserves() (contracts/pool/franchised/FranchisedConstantProductPool.sol#258-270)
	- FranchisedConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/franchised/FranchisedConstantProductPool.sol#281-309)
	- FranchisedConstantProductPool.constructor(bytes,address) (contracts/pool/franchised/FranchisedConstantProductPool.sol#54-86)
	- _update(balance0_scope_0,balance1_scope_1,_reserve0,_reserve1,_blockTimestampLast) (contracts/pool/franchised/FranchisedConstantProductPool.sol#246)
		- reserve0 = uint112(balance0) (contracts/pool/franchised/FranchisedConstantProductPool.sol#291)
		- reserve0 = uint112(balance0) (contracts/pool/franchised/FranchisedConstantProductPool.sol#304)
	FranchisedConstantProductPool.reserve0 (contracts/pool/franchised/FranchisedConstantProductPool.sol#40) can be used in cross function reentrancies:
	- FranchisedConstantProductPool._getReserves() (contracts/pool/franchised/FranchisedConstantProductPool.sol#258-270)
	- FranchisedConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/franchised/FranchisedConstantProductPool.sol#281-309)
	- _update(balance0_scope_0,balance1_scope_1,_reserve0,_reserve1,_blockTimestampLast) (contracts/pool/franchised/FranchisedConstantProductPool.sol#246)
		- reserve1 = uint112(balance1) (contracts/pool/franchised/FranchisedConstantProductPool.sol#292)
		- reserve1 = uint112(balance1) (contracts/pool/franchised/FranchisedConstantProductPool.sol#305)
	FranchisedConstantProductPool.reserve1 (contracts/pool/franchised/FranchisedConstantProductPool.sol#41) can be used in cross function reentrancies:
	- FranchisedConstantProductPool._getReserves() (contracts/pool/franchised/FranchisedConstantProductPool.sol#258-270)
	- FranchisedConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/franchised/FranchisedConstantProductPool.sol#281-309)
	- FranchisedConstantProductPool.swap(bytes) (contracts/pool/franchised/FranchisedConstantProductPool.sol#196-220)

   - Recommendation: No specific recommendation provided.

13. **solc-version**
   - Contract: FranchisedConstantProductPool
   - Severity: Informational
   - Confidence: High
   - Line: 3
   - Description: Version constraint >=0.8.0 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationChangeInInternalOverride
	- NestedCalldataArrayAbiReencodingSizeValidation
	- SignedImmutables
	- ABIDecodeTwoDimensionalArrayMemory
	- KeccakCaching.
It is used by:
	- >=0.8.0 (contracts/TridentRouter.sol#3)
	- >=0.8.0 (contracts/deployer/MasterDeployer.sol#3)
	- >=0.8.0 (contracts/interfaces/IBentoBoxMinimal.sol#3)
	- >=0.8.0 (contracts/interfaces/IMasterDeployer.sol#3)
	- >=0.8.0 (contracts/interfaces/IPoolFactory.sol#3)
	- >=0.8.0 (contracts/interfaces/ITridentCallee.sol#3)
	- >=0.8.0 (contracts/interfaces/ITridentRouter.sol#3)
	- >=0.8.0 (contracts/interfaces/IWhiteListManager.sol#3)
	- >=0.8.0 (contracts/libraries/MathUtils.sol#3)
	- >=0.8.0 (contracts/libraries/TridentMath.sol#3)
	- >=0.8.0 (contracts/pool/ConstantProductPool.sol#3)
	- >=0.8.0 (contracts/pool/ConstantProductPoolFactory.sol#3)
	- >=0.8.0 (contracts/pool/HybridPool.sol#3)
	- >=0.8.0 (contracts/pool/HybridPoolFactory.sol#3)
	- >=0.8.0 (contracts/pool/IndexPool.sol#3)
	- >=0.8.0 (contracts/pool/IndexPoolFactory.sol#3)
	- >=0.8.0 (contracts/pool/PoolDeployer.sol#3)
	- >=0.8.0 (contracts/pool/TridentERC20.sol#3)
	- >=0.8.0 (contracts/pool/franchised/FranchisedConstantProductPool.sol#3)
	- >=0.8.0 (contracts/pool/franchised/FranchisedHybridPool.sol#3)
	- >=0.8.0 (contracts/pool/franchised/FranchisedIndexPool.sol#3)
	- >=0.8.0 (contracts/pool/franchised/TridentFranchisedERC20.sol#3)
	- >=0.8.0 (contracts/pool/franchised/WhiteListManager.sol#3)
	- >=0.8.0 (contracts/utils/TridentHelper.sol#3)
	- >=0.8.0 (contracts/utils/TridentOwnable.sol#3)
	- >=0.8.0 (contracts/workInProgress/IMigrator.sol#3)
	- >=0.8.0 (contracts/workInProgress/Migrator.sol#3)

   - Recommendation: No specific recommendation provided.

14. **low-level-calls**
   - Contract: FranchisedConstantProductPool
   - Severity: Informational
   - Confidence: High
   - Line: 339
   - Description: Low level call in FranchisedConstantProductPool._transfer(address,uint256,address,bool) (contracts/pool/franchised/FranchisedConstantProductPool.sol#339-352):
	- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMinimal.withdraw.selector,token,address(this),to,0,shares)) (contracts/pool/franchised/FranchisedConstantProductPool.sol#346)
	- (success_scope_0,None) = bento.call(abi.encodeWithSelector(IBentoBoxMinimal.transfer.selector,token,address(this),to,shares)) (contracts/pool/franchised/FranchisedConstantProductPool.sol#349)

   - Recommendation: No specific recommendation provided.

15. **naming-convention**
   - Contract: FranchisedConstantProductPool
   - Severity: Informational
   - Confidence: High
   - Line: 27
   - Description: Variable FranchisedConstantProductPool.MAX_FEE_MINUS_SWAP_FEE (contracts/pool/franchised/FranchisedConstantProductPool.sol#27) is not in mixedCase

   - Recommendation: No specific recommendation provided.

16. **too-many-digits**
   - Contract: FranchisedConstantProductPool
   - Severity: Informational
   - Confidence: Medium
   - Line: 15
   - Description: FranchisedConstantProductPool.slitherConstructorConstantVariables() (contracts/pool/franchised/FranchisedConstantProductPool.sol#15-398) uses literals with too many digits:
	- MAX_FEE_SQUARE = 100000000 (contracts/pool/franchised/FranchisedConstantProductPool.sol#24)

   - Recommendation: No specific recommendation provided.

17. **unused-state**
   - Contract: FranchisedConstantProductPool
   - Severity: Informational
   - Confidence: High
   - Line: 24
   - Description: FranchisedConstantProductPool.MAX_FEE_SQUARE (contracts/pool/franchised/FranchisedConstantProductPool.sol#24) is never used in FranchisedConstantProductPool (contracts/pool/franchised/FranchisedConstantProductPool.sol#15-398)

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: FranchisedConstantProductPool
   - Severity: Low
   - Confidence: Medium
   - Line: 54
   - Description: FranchisedConstantProductPool.constructor(bytes,address)._masterDeployer (contracts/pool/franchised/FranchisedConstantProductPool.sol#54) lacks a zero-check on :
		- (None,_barFee) = _masterDeployer.staticcall(abi.encodeWithSelector(IMasterDeployer.barFee.selector)) (contracts/pool/franchised/Franch
   - Recommendation: No specific recommendation provided.

2. **reentrancy-benign**
   - Contract: FranchisedConstantProductPool
   - Severity: Low
   - Confidence: Medium
   - Line: 223
   - Description: Reentrancy in FranchisedConstantProductPool.flashSwap(bytes) (contracts/pool/franchised/FranchisedConstantProductPool.sol#223-250):
	External calls:
	- _transfer(token0,amountOut,recipient,unwrapBento) (contracts/pool/franchised/FranchisedConstantProductPool.sol#242)
		- (success,None) = bento.call(
   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: FranchisedConstantProductPool
   - Severity: Low
   - Confidence: Medium
   - Line: 196
   - Description: Reentrancy in FranchisedConstantProductPool.swap(bytes) (contracts/pool/franchised/FranchisedConstantProductPool.sol#196-220):
	External calls:
	- _transfer(tokenOut,amountOut,recipient,unwrapBento) (contracts/pool/franchised/FranchisedConstantProductPool.sol#217)
		- (success,None) = bento.call(abi
   - Recommendation: No specific recommendation provided.

4. **timestamp**
   - Contract: FranchisedConstantProductPool
   - Severity: Low
   - Confidence: Medium
   - Line: 281
   - Description: FranchisedConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/franchised/FranchisedConstantProductPool.sol#281-309) uses timestamp for comparisons
	Dangerous comparisons:
	- require(bool,string)(balance0 <= type()(uint112).max && balance1 <= type()(uint112).max,OVERFL
   - Recommendation: No specific recommendation provided.
