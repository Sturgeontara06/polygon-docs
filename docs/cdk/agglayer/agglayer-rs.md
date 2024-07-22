## Overview

The AggLayer is a Rust-based web service designed to ensure safety for cross-chain asset transfers among heterogeneous blockchain networks. This safety is provided using ZKPs, allowing end-users to interoperate with no additional trust assumptions.  

The service verifies the validity of proofs from various CDK chains before forwarding them to L1 for verification.

It replaces the previous [Golang implementation](agglayer-go.md).

## Architecture

### Components

- Unified bridge: A shared bridge contract for all AggLayer-connected chains, allowing for the transfer of native assets.
- Pessimistic proof: A novel ZKP that provides safety for the assets on the unified bridge by ensuring no chain can withdraw more tokens of any type than have been deposited into it. The pessimistic proof is validated the verifier contract on the L1. 

### Data flow

- Input: Proofs from various CDK chains.
- Processing: Verification of proofs.
- Output: Verified proofs sent to L1.

[pic-here]

## Getting started

### Prerequisites

#### Hardware 

- RPC nodes: Configure RPC nodes for each CDK chain, and synced with the target CDK, to check the state roots post L2 batch executions.

#### Software

- Rust

### Installation

1. Clone the repository:

      ```sh
      git clone https://github.com/AggLayer/agglayer-rs.git
      cd agglayer-rs
      ```

2. Build and run:

      ```sh
      cargo build
      cargo run
      ```

## How to

### Configure the service

Edit configuration by modifying the `agglayer.toml` file for service settings like RPC endpoints and network parameters. For example:

```toml
[network]
rpc_url = "https://your_rpc_url"
chain_id = "your_chain_id"
```

### Run tests

1. Run unit tests:

      ```sh
      cargo test
      ```

2. Run integration tests by first ensuring all necessary services are running, then execute:

      ```sh
      cargo test -- --ignored
      ```

## API reference

### Endpoints

#### Submit proof

- **Endpoint**: `/submit_zkp`
- **Method**: POST
- **Payload**: 

     ```json
     {
       "zkp": "base64_encoded_zkp",
       "chain_id": "cdk_chain_id"
     }
     ```

- **Response**:

     ```json
     {
       "status": "success",
       "message": "ZKP submitted successfully"
     }
     ```

---

For more information, visit the [AggLayer Rust repository](https://github.com/AggLayer/agglayer-rs).