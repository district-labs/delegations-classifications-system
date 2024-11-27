# Delegations Classification System

The Universal Smart Wallet uses the [MetaMask Delegation Framework](https://github.com/MetaMask/delegation-framework) to power the unique delegation, authorization and intent based features.

The framework includes 20+ [enforcer smart contract modules](https://github.com/MetaMask/delegation-framework/tree/main/src/enforcers) for dictating transaction execution capabilities.

How these enforcers are utilized has a significant impact on the user experience and system architecture.

The Universal Delegation Classification system is a way to classify these enforcer combinations in a more product centric normenclature. The goal is to provide a shared language for describing product features, instead of technical implementations.

## Credit Authorizations

A `CreditAuthorization` enables asset transfer from an account with **NO EXPLICIT** outcomes.

Canonical Name: **CreditAuthorization**

Core Enforcers:
 - ERC20AmountTransferEnforcer.sol
 - NativeTokenTransferAmountEnforcer.sol

Recommended Enforcers:
- BlockNumberEnforcer.sol
- TimestampEnforcer.sol

> [!NOTE]
> The credit authorization does not include an enforcement mechanism for "repayment" of credit, because those capabilities can happen indepdent of the enforcers: web of trust, decentralized protocol, centralized service, etc...

## Action Authorizations

An `ActionAuthorization` enables asset transfer from an account with **EXPLICIT** outcomes.

Canonical Name: **ActionAuthorization**

Core Enforcers:
 - ERC20BalanceGteEnforcer.sol
 - NativeBalanceGteEnforcer.sol

Recommended Enforcers:
- AllowedCalldataEnforcer.sol
- AllowedMethodsEnforcer.sol
- AllowedTargetsEnforcer.sol

Optional Enforcers:
- BlockNumberEnforcer.sol
- LimitedCallsEnforcer.sol
- TimestampEnforcer.sol
- NonceEnforcer.sol

Because the Action Authorization can include calls to smart contract that might be unknown to Universal it's important that the applications attempt to use smart contract addresses, function signatures and calldata to make educated assumptions about what the user the user's intent.

How these inferences are made is implementation specific and may differ from application to application.
