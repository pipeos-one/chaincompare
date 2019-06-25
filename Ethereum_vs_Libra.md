

|  **Dimensions** | **Libra** | **Eth1.x** | **Eth2.0** |
| :---: | :---: | :---: | :---: |
|  Documentation | https://developers.libra.org | https://github.com/ethereum/yellowpaper | https://github.com/ethereum/eth2.0-specs |
|  **Coin** | Libra | Ether | Ether |
|   | Fully backed with a basket of bank deposits and treasuries from high-quality central banks. Planned to be a stablecoin. | Intrinsic value, that fluctuates with the market | Intrinsic value, that fluctuates with the market |
|  **External Developers** |  |  |  |
|  Contracts | Currently, external developers are not allowed to publish Move modules. Libra comes with predefined ones. User-defined smart contracts are planned in the future | Developers can build their own smart contracts | Developers can build their own smart contracts |
|  **Core blockchain mechanisms** |  |  |  |
|   | Defined in Move modules, changing does not require hard forks | Defined in the client implementation, changing requires hard forks | Some of the mechanisms will be defined in smart contracts, on the beacon chain |
|   | Fully open system planned, but not initially. Existing Libra institutions control the mechanisms initially | Open system, with EIP process for proposing changes. However, core developers give the final implementation decision. | Multiple VMs will be supported in beacon chain contracts. EIP process will remain in place. |
|  Accounts | A user is free to create multiple<br/>accounts by generating multiple key-pairs. Accounts controlled by the same user have no inherent<br/>link to each other. Pseudonymity for users. The Libra protocol does not link accounts to a real-world identity, but they will have KYC in their official onboarding. | Users have pseudonymity. | Users have pseudonymity. |
|  Verifying reads and transactions | Authenticated reads, clients can easily verify validator transaction history, as each transaction determines a new ledger state that can be recomputed and checked. | Necessary to replay the whole history, starting from a trusted block, all the way until the given transaction. |  |


|  **Dimensions** | **Libra** | **Eth1.x** | **Eth2.0** |
| :---: | :---: | :---: | :---: |
|  Account | An account could represent direct end users of the system as well as modules, such as<br/>custodial wallets | Both externally owned accounts (end users) & contracts | Both externally owned accounts (end users) & contracts |
|  Account keys | 32 byte | 20 byte | 32 byte |
|  Account keys | Multiple private/public key pairs per account address | One private/public key pair per account address | One private/public key pair per account address |
|  Hashing | SHA3-256 | SHA3 / keccak256 | SHA2-256 |
|  Signatures | EdDSA, edwards 25519 | ECDSA | BLS |
|  **Transactions** |  |  |  |
|   | Sequential transactions, each of which determines another version of the entire ledger, corresponding to the new state. A version number is an unsigned 64-bit integer that corresponds to the number of transactions the system has executed. Blocks are just batches used for increasing efficiency of the consensus mechanism. | Transactions have an order inside the block, but the block itself is the one that provides backwards linking with the previous block, through the header. There is no clear limit to the number of total transactions, which will be determined by hardware memory capabilities, etc. |  |
|  Transaction data | Program: Move bytecode script + inputs. Script can target multiple Move modules, doing a one time complex transaction (like an unpublished Move module). Optionally, can contain a list of Move modules to publish. | Encoded inputs for a contract function, function signature, contract address. Can target only one contract function. |  |
|  Transaction output | status code, gas usage, and event list |  |  |
|  Transaction sender | Sender address & public key | Sender address |  |
|  Gas price | Gas price | Gas price |  |
|  Max gas | Max gas | Gas limit |  |
|  Account transaction nonce | Sequence number: <addr>LibraAccount.T | Account Nonce |  |
|  **Contracts** |  |  |  |
|  **** | Modules are published under the sender's account | Contracts are published at their own address |  |
|  **** | Modules are immutable, they cannot be modified or deleted, except via a hard fork. Safe module updates in future versions. | Various patterns for contract updates already exist, with some limitations. |  |
|  **** | Modules & resources are in the global scope and can be easily reused. | Libraries and contracts need sources/interfaces to be reused |  |
|  **** | Modules have no state | Libraries have no state. Contracts can have state. |  |
|  **** | State is stored in each user account, which looks like AccountKey => {resources: (Resource: value)][], modules: (Module: code)[]} | State is only stores in contracts. |  |
|  Available types | booleans, unsigned 64-bit integers, 256-bit addresses, fixed-size byte arrays, structs (including resources), and references | A lot more types: https://solidity.readthedocs.io/en/v0.5.9/types.html |  |
|   | Custom resource types, with rules that are checked by the bytecode verifier at compile time | No compile time checks for custom types, though possible to build on top of the current protocol. | Possible to build on top of the protocol |
|  Logs | Events: Not readable from Move VM, cheap, used to read changes live or back in history | Events: Not readable from Move VM, cheap, used to read changes live or back in history | Events: Not readable from Move VM, cheap, used to read changes live or back in history |
|   | Contained in each transaction output | Contained in each block |  |
|  Blocks | Transactions are batched as an optimization, in the consensus protocol. Otherwise, transactions are treated sequentially. | Blocks are crucial, they provide the link to the previous block, along with the proof that the entire chain is valid. |  |
