# Smart Contract Audit Report

**Status**: Completed

## Total Findings
- Raw Total Findings: 35
- Retained Findings: 27
- Filtered Out: 8
- Total Reduction Rate: 22.86%
- False Positive Rate: 25.71%

## Confirmed Findings

None

## Plausible But Unverified Findings

1. **uninitialized-local**
   - Contract: DAO
   - Function: newGrantProposal(address,uint256)
   - Severity: Medium
   - Confidence: Medium
   - Description: DAO.newGrantProposal(address,uint256).grant (contracts/DAO.sol#61) is a local variable never initialized

   - Remediation: Initialize the 'grant' variable before using it to avoid unpredictable behavior.

2. **boolean-equal**
   - Contract: DAO
   - Function: voteProposal(uint256)
   - Severity: Informational
   - Confidence: High
   - Description: DAO.voteProposal(uint256) (contracts/DAO.sol#79-92) compares to a boolean constant:
	-hasQuorum(proposalID) && mapPID_finalising[proposalID] == false (contracts/DAO.sol#82)

   - Remediation: Refactor to use implicit boolean checks, replacing '== false' with '!mapPID_finalising[proposalID]'.

3. **boolean-equal**
   - Contract: DAO
   - Function: init(address,address,address)
   - Severity: Informational
   - Confidence: High
   - Description: DAO.init(address,address,address) (contracts/DAO.sol#46-53) compares to a boolean constant:
	-require(bool)(inited == false) (contracts/DAO.sol#47)

   - Remediation: Simplify the requirement to 'require(!inited)' to enhance code clarity.

4. **boolean-equal**
   - Contract: DAO
   - Function: finaliseProposal(uint256)
   - Severity: Informational
   - Confidence: High
   - Description: DAO.finaliseProposal(uint256) (contracts/DAO.sol#111-125) compares to a boolean constant:
	-require(bool,string)(mapPID_finalising[proposalID] == true,Must be finalising) (contracts/DAO.sol#113)

   - Remediation: Use 'require(mapPID_finalising[proposalID], "Must be finalising")' for better readability.

5. **solc-version**
   - Contract: DAO
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Version constraint 0.8.3 contains known severe issues...
   - Remediation: Upgrade the Solidity compiler version to a stable release that fixes these known issues.

6. **naming-convention**
   - Contract: DAO
   - Function: hasMajority(uint256)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter DAO.hasMajority(uint256)._proposalID (contracts/DAO.sol#165) is not in mixedCase

   - Remediation: Rename '_proposalID' to 'proposalID' to adhere to the mixedCase naming convention.

7. **naming-convention**
   - Contract: DAO
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable DAO.mapPID_type (contracts/DAO.sol#29) is not in mixedCase

   - Remediation: Change 'mapPID_type' to 'mapPidType' to conform to mixedCase standards.

8. **naming-convention**
   - Contract: DAO
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable DAO.VADER (contracts/DAO.sol#21) is not in mixedCase

   - Remediation: Rename 'VADER' to 'vader' for compliance with mixedCase style.

9. **naming-convention**
   - Contract: DAO
   - Function: Unknown
   - Severity: Informational
   - Confidence: High
   - Description: Variable DAO.mapPID_finalised (contracts/DAO.sol#33) is not in mixedCase

   - Remediation: Modify 'mapPID_finalised' to 'mapPidFinalised' to match mixedCase conventions.

10. **naming-convention**
   - Contract: DAO
   - Function: moveUtils(uint256)
   - Severity: Informational
   - Confidence: High
   - Description: Parameter DAO.moveUtils(uint256)._proposalID (contracts/DAO.sol#144) is not in mixedCase

   - Remediation: Update '_proposalID' to 'proposalID' for consistent mixedCase naming.

## Unsupported Or False Positive

1. **missing-zero-check**
   - Contract: DAO
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: DAO.init(address,address,address)._vader (contracts/DAO.sol#46) lacks a zero-check on :
		- VADER = _vader (contracts/DAO.sol#49)


2. **missing-zero-check**
   - Contract: DAO
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: DAO.init(address,address,address)._usdv (contracts/DAO.sol#46) lacks a zero-check on :
		- USDV = _usdv (contracts/DAO.sol#50)


3. **missing-zero-check**
   - Contract: DAO
   - Function: init(address,address,address)
   - Severity: Low
   - Confidence: Medium
   - Description: DAO.init(address,address,address)._vault (contracts/DAO.sol#46) lacks a zero-check on :
		- VAULT = _vault (contracts/DAO.sol#51)


4. **reentrancy-benign**
   - Contract: DAO
   - Function: moveUtils(uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in DAO.moveUtils(uint256) (contracts/DAO.sol#144-149):
	External calls:
	- iVADER(VADER).changeUTILS(_proposedAddress) (contracts/DAO.sol#147)
	State variables written after the call(s):
	- completeProposal(_proposalID) (contracts/DAO.sol#148)
		- mapPID_finalised[_proposalID] = true (con

5. **reentrancy-benign**
   - Contract: DAO
   - Function: moveRewardAddress(uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in DAO.moveRewardAddress(uint256) (contracts/DAO.sol#150-155):
	External calls:
	- iVADER(VADER).setRewardAddress(_proposedAddress) (contracts/DAO.sol#153)
	State variables written after the call(s):
	- completeProposal(_proposalID) (contracts/DAO.sol#154)
		- mapPID_finalised[_proposalID

6. **reentrancy-events**
   - Contract: DAO
   - Function: moveUtils(uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in DAO.moveUtils(uint256) (contracts/DAO.sol#144-149):
	External calls:
	- iVADER(VADER).changeUTILS(_proposedAddress) (contracts/DAO.sol#147)
	Event emitted after the call(s):
	- FinalisedProposal(msg.sender,_proposalID,mapPID_votes[_proposalID],iVAULT(VAULT).totalWeight(),_typeStr) (con

7. **reentrancy-events**
   - Contract: DAO
   - Function: moveRewardAddress(uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: Reentrancy in DAO.moveRewardAddress(uint256) (contracts/DAO.sol#150-155):
	External calls:
	- iVADER(VADER).setRewardAddress(_proposedAddress) (contracts/DAO.sol#153)
	Event emitted after the call(s):
	- FinalisedProposal(msg.sender,_proposalID,mapPID_votes[_proposalID],iVAULT(VAULT).totalWeight(),_

8. **timestamp**
   - Contract: DAO
   - Function: finaliseProposal(uint256)
   - Severity: Low
   - Confidence: Medium
   - Description: DAO.finaliseProposal(uint256) (contracts/DAO.sol#111-125) uses timestamp for comparisons
	Dangerous comparisons:
	- require(bool,string)((block.timestamp - mapPID_timeStart[proposalID]) > coolOffPeriod,Must be after cool off) (contracts/DAO.sol#112)

