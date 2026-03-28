# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 20
- Retained Findings: 15
- Filtered Out: 5
- Total Reduction Rate: 25.00%
- False Positive Rate: 25.00%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **Access Control: ROOT Role**
   - Contract: FYToken
   - Severity: Medium
   - Description: Access Control: ROOT Role
   - Recommendation: Ensure that only authorized addresses can assign ROOT roles by implementing role-based access control with clear permissions.

2. **Maturity Checks: Timestamps**
   - Contract: FYToken
   - Severity: Medium
   - Description: Maturity Checks: Timestamps
   - Recommendation: Verify that maturity timestamps are properly validated and ensure usage of block.timestamp to prevent manipulation.

3. **Flash Loan Implementation: Fee Absent**
   - Contract: FYToken
   - Severity: Medium
   - Description: Flash Loan Implementation: Fee Absent
   - Recommendation: Implement mandatory fees on flash loans to prevent arbitrage abuses and ensure adequate compensation.

4. **Flash Loan Implementation: Repayment Failures**
   - Contract: FYToken
   - Severity: Medium
   - Description: Flash Loan Implementation: Repayment Failures
   - Recommendation: Check the repayment amount before finalizing a flash loan to ensure the loan balance is repaid fully.

5. **Oracle Dependency**
   - Contract: FYToken
   - Severity: Medium
   - Description: Oracle Dependency
   - Recommendation: Use multiple oracles to verify data consistency and handle failures gracefully by implementing fallback mechanisms.

6. **Burning and Minting Logic**
   - Contract: FYToken
   - Severity: Medium
   - Description: Burning and Minting Logic
   - Recommendation: Ensure there are adequate checks in place for burning and minting operations to prevent unauthorized token creation or destruction.

7. **Overflow Checks**
   - Contract: FYToken
   - Severity: Medium
   - Description: Overflow Checks
   - Recommendation: Implement SafeMath library to prevent overflow and underflow in arithmetic operations.

8. **Review Access Control**
   - Contract: FYToken
   - Severity: Medium
   - Description: Review Access Control
   - Recommendation: Reassess all access control checks to ensure only authorized users can perform critical operations.

9. **Enhance Oracle Security**
   - Contract: FYToken
   - Severity: Medium
   - Description: Enhance Oracle Security
   - Recommendation: Strengthen oracle security by using signed price feeds and implementing validation against potential outliers.

10. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: FYToken
   - Severity: HIGH
   - Line: 167
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Implement safe price calculation checks and ensure oracle data is used for secure and reliable pricing.

11. **reentrancy-no-eth**
   - Contract: FYToken
   - Severity: Medium
   - Confidence: Medium
   - Line: 219
   - Description: Reentrancy in FYToken.flashLoan(IERC3156FlashBorrower,address,uint256,bytes) (contracts/FYToken.sol#219-229):
	External calls:
	- require(bool,string)(receiver.onFlashLoan(msg.sender,token,amount,0,data) == FLASH_LOAN_RETURN,Non-compliant borrower) (contracts/FYToken.sol#226)
	State variables written after the call(s):
	- _burn(address(receiver),amount) (contracts/FYToken.sol#227)
		- _balanceOf[src] = _balanceOf[src] - wad (contracts/utils/token/ERC20.sol#190)
	ERC20._balanceOf (contracts/utils/token/ERC20.sol#30) can be used in cross function reentrancies:
	- ERC20._burn(address,uint256) (contracts/utils/token/ERC20.sol#187-196)
	- FYToken._burn(address,uint256) (contracts/FYToken.sol#167-180)
	- ERC20._mint(address,uint256) (contracts/utils/token/ERC20.sol#167-173)
	- ERC20._transfer(address,address,uint256) (contracts/utils/token/ERC20.sol#115-123)
	- ERC20.balanceOf(address) (contracts/utils/token/ERC20.sol#55-57)
	- _burn(address(receiver),amount) (contracts/FYToken.sol#227)
		- _totalSupply = _totalSupply - wad (contracts/utils/token/ERC20.sol#191)
	ERC20._totalSupply (contracts/utils/token/ERC20.sol#29) can be used in cross function reentrancies:
	- ERC20._burn(address,uint256) (contracts/utils/token/ERC20.sol#187-196)
	- ERC20._mint(address,uint256) (contracts/utils/token/ERC20.sol#167-173)
	- FYToken.maxFlashLoan(address) (contracts/FYToken.sol#187-193)
	- ERC20.totalSupply() (contracts/utils/token/ERC20.sol#48-50)

   - Recommendation: No specific recommendation provided.

12. **unused-return**
   - Contract: FYToken
   - Severity: Medium
   - Confidence: Medium
   - Line: 135
   - Description: FYToken.redeem(address,uint256) (contracts/FYToken.sol#135-145) ignores return value by join.exit(to,redeemed.u128()) (contracts/FYToken.sol#142)

   - Recommendation: No specific recommendation provided.

13. **solc-version**
   - Contract: FYToken
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint 0.8.1 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
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
	- 0.8.1 (contracts/Cauldron.sol#2)
	- 0.8.1 (contracts/FYToken.sol#2)
	- 0.8.1 (contracts/FYTokenFactory.sol#2)
	- 0.8.1 (contracts/Join.sol#2)
	- 0.8.1 (contracts/JoinFactory.sol#2)
	- 0.8.1 (contracts/Ladle.sol#2)
	- 0.8.1 (contracts/LadleStorage.sol#2)
	- 0.8.1 (contracts/Wand.sol#2)
	- 0.8.1 (contracts/Witch.sol#2)
	- 0.8.1 (contracts/constants/Constants.sol#2)
	- 0.8.1 (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#2)
	- 0.8.1 (contracts/oracles/composite/CompositeMultiOracle.sol#2)
	- 0.8.1 (contracts/oracles/compound/CTokenMultiOracle.sol#2)
	- 0.8.1 (contracts/oracles/compound/CompoundMultiOracle.sol#2)
	- 0.8.1 (contracts/utils/token/ERC20Rewards.sol#2)
	- 0.8.1 (contracts/yieldspace/Math64x64.sol#6)
	- 0.8.1 (contracts/yieldspace/Pool.sol#2)
	- 0.8.1 (contracts/yieldspace/PoolFactory.sol#2)
	- 0.8.1 (contracts/yieldspace/Strategy.sol#2)
	- 0.8.1 (contracts/yieldspace/YieldMath.sol#2)

   - Recommendation: No specific recommendation provided.

14. **too-many-digits**
   - Contract: FYToken
   - Severity: Informational
   - Confidence: Medium
   - Line: 19
   - Description: FYToken.slitherConstructorConstantVariables() (contracts/FYToken.sol#19-230) uses literals with too many digits:
	- ROOT = 0x00000000 (contracts/utils/access/AccessControl.sol#47)

   - Recommendation: No specific recommendation provided.

15. **unused-state**
   - Contract: FYToken
   - Severity: Informational
   - Confidence: High
   - Line: 6
   - Description: Constants.RATE (contracts/constants/Constants.sol#6) is never used in FYToken (contracts/FYToken.sol#19-230)

   - Recommendation: No specific recommendation provided.

## Unsupported Or False Positive

1. **shadowing-local**
   - Contract: FYToken
   - Severity: Low
   - Confidence: High
   - Line: 47
   - Description: FYToken.constructor(bytes6,IOracle,IJoin,uint256,string,string).symbol (contracts/FYToken.sol#47) shadows:
	- ERC20.symbol (contracts/utils/token/ERC20.sol#33) (state variable)
	- IERC20Metadata.symbol() (contracts/interfaces/external/IERC20Metadata.sol#20) (function)

   - Recommendation: No specific recommendation provided.

2. **missing-zero-check**
   - Contract: FYToken
   - Severity: Low
   - Confidence: Medium
   - Line: 68
   - Description: PoolFactory.createPool(address,address).fyToken (contracts/yieldspace/PoolFactory.sol#68) lacks a zero-check on :
		- _nextFYToken = fyToken (contracts/yieldspace/PoolFactory.sol#70)

   - Recommendation: No specific recommendation provided.

3. **reentrancy-benign**
   - Contract: FYToken
   - Severity: Low
   - Confidence: Medium
   - Line: 219
   - Description: Reentrancy in FYToken.flashLoan(IERC3156FlashBorrower,address,uint256,bytes) (contracts/FYToken.sol#219-229):
	External calls:
	- require(bool,string)(receiver.onFlashLoan(msg.sender,token,amount,0,data) == FLASH_LOAN_RETURN,Non-compliant borrower) (contracts/FYToken.sol#226)
	State variables writte
   - Recommendation: No specific recommendation provided.

4. **reentrancy-events**
   - Contract: FYToken
   - Severity: Low
   - Confidence: Medium
   - Line: 101
   - Description: Reentrancy in FYToken._mature() (contracts/FYToken.sol#101-108):
	External calls:
	- (_chiAtMaturity,None) = oracle.get(underlyingId,CHI,1e18) (contracts/FYToken.sol#105)
	Event emitted after the call(s):
	- SeriesMatured(_chiAtMaturity) (contracts/FYToken.sol#107)

   - Recommendation: No specific recommendation provided.

5. **timestamp**
   - Contract: FYToken
   - Severity: Low
   - Confidence: Medium
   - Line: 41
   - Description: FYToken.constructor(bytes6,IOracle,IJoin,uint256,string,string) (contracts/FYToken.sol#41-63) uses timestamp for comparisons
	Dangerous comparisons:
	- require(bool,string)(maturity_ > now_ && maturity_ < now_ + MAX_TIME_TO_MATURITY && maturity_ < type()(uint32).max,Invalid maturity) (contracts/FYTo
   - Recommendation: No specific recommendation provided.
