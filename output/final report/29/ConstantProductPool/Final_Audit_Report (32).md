# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 21
- Retained Findings: 17
- Filtered Out: 4
- Total Reduction Rate: 19.05%
- False Positive Rate: 19.05%

## Confirmed Findings

1. **Unprotected Functions**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Description: Unprotected Functions
   - Recommendation: Protect the functions with appropriate access control checks like 'onlyOwner' to limit the callers.

## Plausible But Unverified Findings

1. **Reentrancy Vulnerability**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Description: Reentrancy Vulnerability
   - Recommendation: Use ReentrancyGuard or the checks-effects-interactions pattern to prevent reentrancy attacks.

2. **Unchecked External Calls**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Description: Unchecked External Calls
   - Recommendation: Ensure external calls are checked for success, using require or assert to handle failures.

3. **Denial of Service (DoS)**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Validate and check conditions that could be manipulated to cause gas limit issues.

4. **Potential Integer Overflow/Underflow**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Description: Potential Integer Overflow/Underflow
   - Recommendation: Use SafeMath for all arithmetic operations to prevent overflow and underflow vulnerabilities.

5. **Price Manipulation**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Description: Price Manipulation
   - Recommendation: Consider using an oracle-based approach for price feeds to mitigate manipulation risks.

6. **Lack of Input Validation**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Description: Lack of Input Validation
   - Recommendation: Add require statements to validate function inputs and ensure they meet expected criteria.

7. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: ConstantProductPool
   - Severity: HIGH
   - Line: 272
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Ensure LP token value calculations are based on trusted price feeds to avoid manipulation.

8. **weak-prng**
   - Contract: ConstantProductPool
   - Severity: High
   - Confidence: Medium
   - Line: 281
   - Description: FranchisedConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) uses a weak PRNG
   - Recommendation: Replace weak PRNG with a secure randomness source, such as Chainlink VRF.

9. **divide-before-multiply**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 281
   - Description: Performs a multiplication on the result of a division
   - Recommendation: Reorder operations to multiply before division to preserve precision.

10. **incorrect-equality**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Confidence: High
   - Line: 90
   - Description: Uses a dangerous strict equality
   - Recommendation: Consider using a less strict condition or add additional context checks.

11. **reentrancy-no-eth**
   - Contract: ConstantProductPool
   - Severity: Medium
   - Confidence: Medium
   - Line: 196
   - Description: Reentrancy in ConstantProductPool.swap(bytes) (contracts/pool/ConstantProductPool.sol#196-220):
	External calls:
	- _transfer(tokenOut,amountOut,recipient,unwrapBento) (contracts/pool/ConstantProductPool.sol#217)
		- (success,None) = bento.call(abi.encodeWithSelector(0x97da6d30,token,address(this),to,0,shares)) (contracts/pool/ConstantProductPool.sol#347)
		- (success_scope_0,None) = bento.call(abi.encodeWithSelector(0xf18d03cc,token,address(this),to,shares)) (contracts/pool/ConstantProductPool.sol#351)
	State variables written after the call(s):
	- _update(balance0,balance1,_reserve0,_reserve1,_blockTimestampLast) (contracts/pool/ConstantProductPool.sol#218)
		- blockTimestampLast = blockTimestamp (contracts/pool/ConstantProductPool.sol#306)
	ConstantProductPool.blockTimestampLast (contracts/pool/ConstantProductPool.sol#42) can be used in cross function reentrancies:
	- ConstantProductPool._getReserves() (contracts/pool/ConstantProductPool.sol#258-270)
	- ConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/ConstantProductPool.sol#281-309)
	- ConstantProductPool.constructor(bytes,address) (contracts/pool/ConstantProductPool.sol#54-81)
	- _update(balance0,balance1,_reserve0,_reserve1,_blockTimestampLast) (contracts/pool/ConstantProductPool.sol#218)
		- reserve0 = uint112(balance0) (contracts/pool/ConstantProductPool.sol#291)
		- reserve0 = uint112(balance0) (contracts/pool/ConstantProductPool.sol#304)
	ConstantProductPool.reserve0 (contracts/pool/ConstantProductPool.sol#40) can be used in cross function reentrancies:
	- ConstantProductPool._getReserves() (contracts/pool/ConstantProductPool.sol#258-270)
	- ConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/ConstantProductPool.sol#281-309)
	- _update(balance0,balance1,_reserve0,_reserve1,_blockTimestampLast) (contracts/pool/ConstantProductPool.sol#218)
		- reserve1 = uint112(balance1) (contracts/pool/ConstantProductPool.sol#292)
		- reserve1 = uint112(balance1) (contracts/pool/ConstantProductPool.sol#305)
	ConstantProductPool.reserve1 (contracts/pool/ConstantProductPool.sol#41) can be used in cross function reentrancies:
	- ConstantProductPool._getReserves() (contracts/pool/ConstantProductPool.sol#258-270)
	- ConstantProductPool._update(uint256,uint256,uint112,uint112,uint32) (contracts/pool/ConstantProductPool.sol#281-309)
	- ConstantProductPool.swap(bytes) (contracts/pool/ConstantProductPool.sol#196-220)

   - Recommendation: No specific recommendation provided.

12. **solc-version**
   - Contract: ConstantProductPool
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

13. **low-level-calls**
   - Contract: ConstantProductPool
   - Severity: Informational
   - Confidence: High
   - Line: 339
   - Description: Low level call in FranchisedConstantProductPool._transfer(address,uint256,address,bool) (contracts/pool/franchised/FranchisedConstantProductPool.sol#339-352):
	- (success,None) = bento.call(abi.encodeWithSelector(IBentoBoxMinimal.withdraw.selector,token,address(this),to,0,shares)) (contracts/pool/franchised/FranchisedConstantProductPool.sol#346)
	- (success_scope_0,None) = bento.call(abi.encodeWithSelector(IBentoBoxMinimal.transfer.selector,token,address(this),to,shares)) (contracts/pool/franchised/FranchisedConstantProductPool.sol#349)

   - Recommendation: No specific recommendation provided.

14. **naming-convention**
   - Contract: ConstantProductPool
   - Severity: Informational
   - Confidence: High
   - Line: 27
   - Description: Variable ConstantProductPool.MAX_FEE_MINUS_SWAP_FEE (contracts/pool/ConstantProductPool.sol#27) is not in mixedCase

   - Recommendation: No specific recommendation provided.

15. **too-many-digits**
   - Contract: ConstantProductPool
   - Severity: Informational
   - Confidence: Medium
   - Line: 15
   - Description: FranchisedConstantProductPool.slitherConstructorConstantVariables() (contracts/pool/franchised/FranchisedConstantProductPool.sol#15-398) uses literals with too many digits:
	- MAX_FEE_SQUARE = 100000000 (contracts/pool/franchised/FranchisedConstantProductPool.sol#24)

   - Recommendation: No specific recommendation provided.

16. **unused-state**
   - Contract: ConstantProductPool
   - Severity: Informational
   - Confidence: High
   - Line: 24
   - Description: FranchisedConstantProductPool.MAX_FEE_SQUARE (contracts/pool/franchised/FranchisedConstantProductPool.sol#24) is never used in FranchisedConstantProductPool (contracts/pool/franchised/FranchisedConstantProductPool.sol#15-398)

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: ConstantProductPool
   - Severity: Low
   - Confidence: Medium
   - Line: 54
   - Description: Lacks a zero-check on _masterDeployer
   - Recommendation: No specific recommendation provided.

2. **reentrancy-benign**
   - Contract: ConstantProductPool
   - Severity: Low
   - Confidence: Medium
   - Line: 223
   - Description: Reentrancy in flashSwap affects external calls
   - Recommendation: No specific recommendation provided.

3. **reentrancy-events**
   - Contract: ConstantProductPool
   - Severity: Low
   - Confidence: Medium
   - Line: 123
   - Description: Reentrancy in burn affects external calls
   - Recommendation: No specific recommendation provided.

4. **timestamp**
   - Contract: ConstantProductPool
   - Severity: Low
   - Confidence: Medium
   - Line: 85
   - Description: Uses timestamp for comparisons
   - Recommendation: No specific recommendation provided.
