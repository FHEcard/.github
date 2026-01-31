# FHEcard

> [!WARNING]
> **Experimental Project**
> This software is currently in the Proof-of-Concept (PoC) phase and is intended for research and development purposes only. Do not use with real funds.

## Overview

**FHEcard** is a privacy-preserving subscription management protocol that bridges the gap between **Fully Homomorphic Encryption (FHE)** on-chain and traditional **Visa/Mastercard** payment rails off-chain.

The core problem FHEcard solves is the lack of privacy in traditional bank statements and the inability to control "zombie subscriptions" (services that are hard to cancel). By acting as a firewall between your money and merchants, FHEcard allows you to generate "Ghost Cards" with programmable, encrypted constraints.

## Target Result

The ultimate goal of FHEcard is to enable a user to:

1.  **Pay Privately:** Your bank statement only shows "FHEcard Protocol Funding", while the actual merchant (e.g., Netflix, Tinder) remains hidden cryptographically on-chain.
2.  **Control Spending:** Set private, encrypted rules (e.g., "Max $15/month"). If a merchant tries to charge $16, the FHE smart contract mathematically catches and rejects the violation without ever revealing your actual balance or limit.
3.  **Settlement Bridge:** Utilize an **Optimistic Settlement Model** to handle the speed mismatch between Visa (milliseconds) and FHE Blockchains (seconds), ensuring instant approvals with cryptographic assurance.

## Architecture

-   **Layer 1 (The Off-Chain Runner):** A Node.js relayer that holds a buffer balance on a card issuing platform (Lithic) and approves transactions instantly based on "Cached Intent."
-   **Layer 2 (The On-Chain Vault):** An FHE-enabled smart contract on **Fhenix** that holds user funds in `eUSDC`.
-   **Layer 3 (The Verification):** (Future) TLSNotary implementation to prove authentic web traffic, ensuring the relayer cannot fake charges.

## Tech Stack

-   **Blockchain:** Fhenix (FHE-EVM), Solidity
-   **Backend:** Node.js, Express
-   **Card Issuer:** Lithic API (Sandbox)
