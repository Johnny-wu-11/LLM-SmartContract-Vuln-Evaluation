# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 9
- Retained Findings: 9
- Filtered Out: 0
- Total Reduction Rate: 0.00%
- False Positive Rate: 0.00%

## Confirmed Findings

1. **Source Management**
   - Contract: CompoundMultiOracle
   - Severity: Medium
   - Description: Source Management
   - Recommendation: Ensure source contracts are properly verified before integration. Implement strict access control to manage sources.

2. **Denial of Service (DoS)**
   - Contract: CompoundMultiOracle
   - Severity: Medium
   - Description: Denial of Service (DoS)
   - Recommendation: Introduce careful gas usage checks and limits for loop and recursive function calls. Ensure critical operations are non-blocking.

## Plausible But Unverified Findings

1. **Role Locking**
   - Contract: CompoundMultiOracle
   - Severity: Medium
   - Description: Role Locking
   - Recommendation: Validate role changes by ensuring only authorized accounts can modify roles. Add logging for role changes for better audit trails.

2. **Price Calculation**
   - Contract: CompoundMultiOracle
   - Severity: Medium
   - Description: Price Calculation
   - Recommendation: Introduce safeguards to prevent price manipulation. Implement time-weighted average price calculations to mitigate manipulation risks.

3. **MWE-200: Insecure LP Token Value Calculation**
   - Contract: CompoundMultiOracle
   - Severity: HIGH
   - Line: 40
   - Description: Liquidity token value/price can be manipulated to cause flashloan attacks.
   - Recommendation: Employ validation using checks against known reliable price oracles. Consider integrating a time-weighted average to reduce the potential for manipulation.

4. **uninitialized-local**
   - Contract: CompoundMultiOracle
   - Severity: Medium
   - Confidence: Medium
   - Line: 41
   - Description: CompoundMultiOracle._peek(bytes6,bytes6).rawPrice (contracts/oracles/compound/CompoundMultiOracle.sol#41) is a local variable never initialized

   - Recommendation: Initialize the variable `rawPrice` before use to avoid unpredictable behavior. Default to a known safe value if applicable.

5. **solc-version**
   - Contract: CompoundMultiOracle
   - Severity: Informational
   - Confidence: High
   - Line: 2
   - Description: Version constraint ^0.8.0 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
	- FullInlinerNonExpressionSplitArgumentEvaluationOrder
	- MissingSideEffectsOnSelectorAccess
	- AbiReencodingHeadOverflowWithStaticArrayCleanup
	- DirtyBytesArrayToStorage
	- DataLocationCha
   - Recommendation: Update Solidity to a newer version that addresses known issues. Verify all contracts under the updated compiler settings.

6. **missing-inheritance**
   - Contract: CompoundMultiOracle
   - Severity: Informational
   - Confidence: High
   - Line: 10
   - Description: CompoundMultiOracle (contracts/oracles/compound/CompoundMultiOracle.sol#10-75) should inherit from IMultiOracleGov (contracts/interfaces/vault/IMultiOracleGov.sol#4-6)

   - Recommendation: Ensure that `CompoundMultiOracle` inherits from `IMultiOracleGov`. Verify that all interface functions are implemented properly.

7. **too-many-digits**
   - Contract: CompoundMultiOracle
   - Severity: Informational
   - Confidence: Medium
   - Line: 10
   - Description: CompoundMultiOracle.slitherConstructorConstantVariables() (contracts/oracles/compound/CompoundMultiOracle.sol#10-75) uses literals with too many digits:
	- ROOT = 0x00000000 (contracts/utils/access/AccessControl.sol#47)

   - Recommendation: Review and possibly refactor the constants with excessive digits to improve code readability. Ensure literals represent intended values accurately.

## Unsupported Or False Positive

None
