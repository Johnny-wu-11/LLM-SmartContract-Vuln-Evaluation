# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 12
- Retained Findings: 11
- Filtered Out: 1
- Total Reduction Rate: 8.33%
- False Positive Rate: 8.33%

## Confirmed Findings

1. **Role Management**
   - Contract: ChainlinkMultiOracle
   - Severity: Medium
   - Description: Role Management
   - Recommendation: Implement stricter role verification logic to ensure only authorized roles can execute sensitive functions.

2. **Oracle Manipulation**
   - Contract: ChainlinkMultiOracle
   - Severity: Medium
   - Description: Oracle Manipulation
   - Recommendation: Add validation checks to ensure oracle data integrity and prevent manipulation with tamper-proof mechanisms.

## Plausible But Unverified Findings

1. **Locking Roles**
   - Contract: ChainlinkMultiOracle
   - Severity: Medium
   - Description: Locking Roles
   - Recommendation: Review the role-locking mechanism to prevent accidental or malicious permanent locking of roles.

2. **Access Control on `setSource` and `setSources`**
   - Contract: ChainlinkMultiOracle
   - Severity: Medium
   - Description: Access Control on `setSource` and `setSources`
   - Recommendation: Ensure access control is enforced for `setSource` and `setSources` to restrict unauthorized modifications.

3. **Insecure Arithmetic**
   - Contract: ChainlinkMultiOracle
   - Severity: Medium
   - Description: Insecure Arithmetic
   - Recommendation: Use SafeMath library for arithmetic operations to prevent overflow and underflow vulnerabilities.

4. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: ChainlinkMultiOracle
   - Severity: HIGH
   - Line: 40
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Implement a guard mechanism to ensure LP token calculations are resistant to flashloan-induced manipulation.

5. **unused-return**
   - Contract: ChainlinkMultiOracle
   - Severity: Medium
   - Confidence: Medium
   - Line: 64
   - Description: ChainlinkMultiOracle._peek(bytes6,bytes6) (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#64-79) ignores return value by (roundId,rawPrice,None,updateTime,answeredInRound) = AggregatorV3Interface(source.source).latestRoundData() (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#70)

   - Recommendation: Check and appropriately handle the return values from `latestRoundData` to ensure data validity.

6. **boolean-equal**
   - Contract: ChainlinkMultiOracle
   - Severity: Informational
   - Confidence: High
   - Line: 64
   - Description: ChainlinkMultiOracle._peek(bytes6,bytes6) (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#64-79) compares to a boolean constant:
	-source.inverse == true (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#74)

   - Recommendation: Simplify boolean comparisons by using `if (source.inverse)` instead of comparing to `true`.

7. **solc-version**
   - Contract: ChainlinkMultiOracle
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint ^0.8.0 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Upgrade the Solidity compiler version to mitigate issues in version ^0.8.0 as per the official Solidity documentation.

8. **missing-inheritance**
   - Contract: ChainlinkMultiOracle
   - Severity: Informational
   - Confidence: High
   - Line: 13
   - Description: ChainlinkMultiOracle (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#13-100) should inherit from IMultiOracleGov (contracts/interfaces/vault/IMultiOracleGov.sol#4-6)

   - Recommendation: Ensure the `ChainlinkMultiOracle` contract inherits from `IMultiOracleGov` to implement necessary governance functions.

9. **too-many-digits**
   - Contract: ChainlinkMultiOracle
   - Severity: Informational
   - Confidence: Medium
   - Line: 13
   - Description: ChainlinkMultiOracle.slitherConstructorConstantVariables() (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#13-100) uses literals with too many digits:
	- ROOT = 0x00000000 (contracts/utils/access/AccessControl.sol#47)

   - Recommendation: Consider simplifying literals by removing unnecessary digits for more readable and maintainable code.

## Unsupported Or False Positive

1. **calls-loop**
   - Contract: ChainlinkMultiOracle
   - Severity: Low
   - Confidence: Medium
   - Line: 29
   - Description: ChainlinkMultiOracle.setSource(bytes6,bytes6,address) (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#29-44) has external calls inside a loop: decimals = AggregatorV3Interface(source).decimals() (contracts/oracles/chainlink/ChainlinkMultiOracle.sol#30)
	Calls stack containing the loop:
		Chain
   - Recommendation: No specific recommendation provided.
