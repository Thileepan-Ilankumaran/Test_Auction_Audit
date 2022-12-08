# Test Auction audit report.


# Summary

This is the report from a security audit performed on [Test Contract](https://gist.github.com/yuriy77k/edf8b3bcddbc3d43967f5765edf4727e) by [Thileepan-Ilankumaran](https://github.com/Thileepan-Ilankumaran). 

The audit focused primarily on the security of funds and fault tolerance of the test auction contract. The main intention of this smart contract is to offer Tokens by auction.

# In scope

1. [testAuction.sol](https://gist.github.com/yuriy77k/edf8b3bcddbc3d43967f5765edf4727e)

# Findings

In total, **10 issues** were reported including:

- 2 high severity issues.

- 1 medium severity issue.

- 7 low severity issues.

2 critical security issues were found.

## Security issues

### 1. Re-entrancy Attack.

#### Severity: high

#### Description

Any interaction from a contract (A) with another contract (B) and any transfer of Ether hands over control to that contract (B). This makes it possible for B to call back into A before this interaction is completed.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/1)

#### Recommendation

You can use the [Checks-Effects-Interactions](https://docs.soliditylang.org/en/v0.4.21/security-considerations.html#re-entrancy). pattern

### 2. Unchecked Transfer

#### Severity: high

#### Description

Several tokens do not revert in case of failure and return false. If one of these tokens is used then attacker can withdraw tokens for free.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#unchecked-transfer). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/2)

#### Recommendation

Use `SafeERC20`, or ensure that the transfer/transferFrom return value is checked.

### 3. Reentrancy Vulnerablity

#### Severity: medium

#### Description

Detection of the [reentrancy bug](https://github.com/crytic/not-so-smart-contracts/tree/master/reentrancy). Do not report reentrancies that involve Ether

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-1). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/3)

### 4. Missing events arithmetic

#### Severity: low

#### Description

Detect missing events for critical arithmetic parameters.

`setCaps()`has no event, so it is difficult to track off-chain changes in the buy price

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#missing-events-arithmetic). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/4)

### 5. Inner variables visibility.

#### Severity: low

#### Description

Detect missing zero address validation.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#missing-zero-address-validation). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/5)

#### Recommendation

Check that the address is not zero.

### 6. Reentrancy Vulnerablity (Double call)

#### Severity: low

#### Description

Detection of the [reentrancy bug](https://github.com/crytic/not-so-smart-contracts/tree/master/reentrancy). Only report reentrancy that acts as a double call.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-2). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/6)

### 7. Calls inside a loop. 

#### Severity: low

#### Description

Calls inside a loop might lead to a denial-of-service attack.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation/#calls-inside-a-loop). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/7)

#### Recommendation

Favor pull over push strategy for external calls.

### 8. Block timestamp.

#### Severity: low

#### Description

Dangerous usage of timestamp comparison can be manipulated by miners.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#block-timestamp). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/8)

#### Recommendation

Avoid relying on timestamps.

### 9. Boolean Equality.

#### Severity: low

#### Description

Detects the comparison to boolean constants.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#boolean-equality). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/9)

#### Recommendation

Remove the equality to the boolean constant.

### 10. Reentrancy Vulnerablity (transfer)

#### Severity: low

#### Description

Detection of the [reentrancy bug](https://github.com/crytic/not-so-smart-contracts/tree/master/reentrancy). Only report reentrancy that is based on `transfer` or `send`.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-4). Code ---> [here](https://github.com/Thileepan-Ilankumaran/Test_Auction_Audit/issues/10)

### 10. Reentrancy Vulnerablity (transfer)

#### Severity: low

#### Description

Detection of the [reentrancy bug](https://github.com/crytic/not-so-smart-contracts/tree/master/reentrancy). Only report reentrancy that is based on `transfer` or `send`.

Detailed description can be found [here](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-4).

# Specification

These contracts are not in ready to use condition. At the time of the audit, the development of this contracts is considered complete but need fixation before deployment. The last fixation was made on November 14, 2022. the last commit was made at 14 Nov 2022.

Bug Bounties were not conducted.

Any further changes to the contracts will leave them in unaudited state.

# Conclusion

2 critical vulnerabilities were detected. The reported issues can directly hurt the Test_Auction smart-contract. The auction smart-contract doesn't satisfy the main goal and could not be used for official development without correction.

It is highly recommended to complete a bug bounty before use.
