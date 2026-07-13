---
title: sgns

---

# sgns





## Namespaces

| Name           |
| -------------- |
| **[sgns::input_validator_constants](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/)**  |
| **[sgns::utxo_merkle](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/)** <br/>Utilities for building deterministic Merkle roots over ordered UTXO payloads.  |
| **[sgns::utxo_address](/source-reference/Namespaces/dd/de2/namespacesgns_1_1utxo__address/)**  |
| **[sgns::api](/source-reference/Namespaces/df/d66/namespacesgns_1_1api/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |
| **[sgns::version](/source-reference/Namespaces/d8/d5b/namespacesgns_1_1version/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::crypto](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |
| **[sgns::sgprocessing](/source-reference/Namespaces/d1/dc7/namespacesgns_1_1sgprocessing/)**  |
| **[sgns::face](/source-reference/Namespaces/d0/d0d/namespacesgns_1_1face/)**  |
| **[sgns::subscription](/source-reference/Namespaces/d4/d82/namespacesgns_1_1subscription/)**  |
| **[sgns::evmwatcher](/source-reference/Namespaces/df/d85/namespacesgns_1_1evmwatcher/)**  |
| **[sgns::watcher](/source-reference/Namespaces/d4/d7f/namespacesgns_1_1watcher/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::AccountMessenger](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/)**  |
| struct | **[sgns::BurnEventParams](/source-reference/Classes/da/d8d/structsgns_1_1_burn_event_params/)** <br/>Parsed burn event parameters shared between real-time watch (OnWatchEvent) and startup catch-up scan (PerformStartupCatchupScan).  |
| class | **[sgns::BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/)** <br/>Registers both BridgeSourceBurned (v1) and BridgeOutInitiated (v2) watches on a shared EthWatchService across multiple chains and calls MintFunds when burns are detected. OnWatchEvent dispatches on the variant type of values[5] to handle both event formats (D-06).  |
| struct | **[sgns::ChainContractPair](/source-reference/Classes/d5/d01/structsgns_1_1_chain_contract_pair/)** <br/>Represents a chain name and its GNUS bridge contract address.  |
| class | **[sgns::IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/)** <br/>Observer interface notified when RPC endpoints have been loaded and wired.  |
| class | **[sgns::ChainRpcEndpointProvider](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/)** <br/>Encapsulates ChainList RPC endpoint loading and validator wiring.  |
| class | **[sgns::EscrowTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/)** <br/>Transaction that reserves funds for a job escrow while tracking peer payout metadata.  |
| class | **[sgns::GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/)**  |
| class | **[sgns::GeniusInputValidator](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/)** <br/>Validator for native Genius-chain transactions.  |
| class | **[sgns::GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/)** <br/>High-level facade that initializes and coordinates account, networking, transaction, blockchain, and processing subsystems.  |
| class | **[sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)** <br/>Base class of the [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/).  |
| struct | **[sgns::OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/)** <br/>Unique identifier for a transaction output.  |
| class | **[sgns::GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/)** <br/>Immutable-style UTXO value object containing ownership, token, amount, and outpoint metadata.  |
| class | **[sgns::IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/)** <br/>Interface for a migration step between two schema versions.  |
| class | **[sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)** <br/>Strategy interface for validating transaction inputs and their witness data.  |
| class | **[sgns::Migration0_2_0To1_0_0](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/)** <br/>Migration step for version 0.2.0 to 1.0.0.  |
| class | **[sgns::Migration1_0_0To3_4_0](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/)** <br/>Migration step for version 1.0.0 to 3.4.0. Changes the full node topic from CRDT heads.  |
| class | **[sgns::Migration3_4_0To3_5_0](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/)** <br/>Migration step for version 3.4.0 to 3.5.0. Updates persisted data required by the 3.5.0 node layout.  |
| class | **[sgns::Migration3_5_0To3_6_0](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/)** <br/>Executes the storage migration from database version 3.5.1 to 3.6.0.  |
| class | **[sgns::Migration3_6_0To3_7_0](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/)** <br/>Executes the 3.6.0 to 3.7.0 migration, including legacy balance recovery.  |
| class | **[sgns::MigrationAllowList](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/)** <br/>Stores observed legacy balances and validates migration claim eligibility.  |
| class | **[sgns::MigrationInputValidator](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/)** <br/>Implements the InputValidator for a Migration type.  |
| class | **[sgns::MigrationManager](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/)** <br/>Executes a sequence of migration steps to update a CRDT store.  |
| class | **[sgns::MigrationTransaction](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/)**  |
| class | **[sgns::MintTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/)** <br/>Transaction that mints tokens after proving a corresponding source-chain event.  |
| class | **[sgns::MintTransactionV2](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/)** <br/>Implements a Mint Version 2 transaction.  |
| class | **[sgns::ProcessingTransaction](/source-reference/Classes/d6/d7f/classsgns_1_1_processing_transaction/)**  |
| struct | **[sgns::WeightedRpcEndpoint](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/)** <br/>Weighted RPC endpoint used for multi-provider consensus verification.  |
| class | **[sgns::PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/)** <br/>Validator for transactions that reference external public-chain proofs.  |
| class | **[sgns::TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/)** <br/>Utility for GNUS token fixed-point parsing, formatting and cost calculation.  |
| class | **[sgns::TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/)** <br/>Represents a 32-byte token identifier while preserving legacy GNUS semantics.  |
| class | **[sgns::TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/)** <br/>Coordinates transaction creation, CRDT propagation, verification, and status tracking.  |
| class | **[sgns::TransferTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/)** <br/>Transaction for transferring funds between UTXO inputs and outputs.  |
| struct | **[sgns::OutPointHash](/source-reference/Classes/d5/d40/structsgns_1_1_out_point_hash/)** <br/>Hash functor for using [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/) keys in unordered containers.  |
| class | **[sgns::UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/)** <br/>Owns the local UTXO set, supports coin selection, validation, persistence, reservations, and deterministic snapshot hashing.  |
| struct | **[sgns::InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/)** <br/>Raw UTXO input data included in a spend request.  |
| struct | **[sgns::OutputDestInfo](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/)** <br/>Single UTXO output destination entry.  |
| class | **[sgns::ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/)** <br/>Represents a decimal value using an integer scaled by 10^precision.  |
| struct | **[sgns::Unused](/source-reference/Classes/da/dac/structsgns_1_1_unused/)**  |
| struct | **[sgns::lambda_visitor](/source-reference/Classes/d2/db4/structsgns_1_1lambda__visitor/)**  |
| struct | **[sgns::lambda_visitor< Lambda, Lambdas... >](/source-reference/Classes/d2/d5d/structsgns_1_1lambda__visitor_3_01_lambda_00_01_lambdas_8_8_8_01_4/)**  |
| struct | **[sgns::lambda_visitor< Lambda >](/source-reference/Classes/dc/d78/structsgns_1_1lambda__visitor_3_01_lambda_01_4/)**  |
| class | **[sgns::Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/)** <br/>Manages genesis/account-creation blocks and consensus integration.  |
| class | **[sgns::ConsensusManager](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/)** <br/>Implements Consensus with weighted voting.  |
| class | **[sgns::ValidatorRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/)** <br/>Maintains validator registry state and applies certificate-driven updates.  |
| class | **[sgns::CoinGeckoPriceRetriever](/source-reference/Classes/d9/da9/classsgns_1_1_coin_gecko_price_retriever/)**  |
| class | **[sgns::AndroidSecureStorage](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/)**  |
| class | **[sgns::AppleSecureStorage](/source-reference/Classes/d9/d1f/classsgns_1_1_apple_secure_storage/)**  |
| class | **[sgns::JSONSecureStorage](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/)**  |
| class | **[sgns::JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/)**  |
| class | **[sgns::LinuxSecureStorage](/source-reference/Classes/dd/de8/classsgns_1_1_linux_secure_storage/)**  |
| class | **[sgns::MemorySecureStorage](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/)** <br/>In-memory JSON backend for tests. Stores data in a map — no OS keychain access, no password prompts, no cleanup needed.  |
| class | **[sgns::WindowsSecureStorage](/source-reference/Classes/db/d24/classsgns_1_1_windows_secure_storage/)**  |
| class | **[sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/)**  |
| class | **[sgns::GeniusAssigner](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/)**  |
| class | **[sgns::GeniusProver](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/)** <br/>Prover class of SuperGenius.  |
| class | **[sgns::IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/)** <br/>Base proof class header file.  |
| class | **[sgns::NilFileHelper](/source-reference/Classes/d4/d4f/classsgns_1_1_nil_file_helper/)**  |
| class | **[sgns::ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/)** <br/>A class for generating and verifying processing proofs.  |
| class | **[sgns::RecursiveTransferProof](/source-reference/Classes/d3/d2f/classsgns_1_1_recursive_transfer_proof/)** <br/>A class for generating a recursive Transfer Proof.  |
| class | **[sgns::TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/)** <br/>A class for generating and verifying transfer proofs.  |

## Types

|                | Name           |
| -------------- | -------------- |
| using std::function< std::optional< std::string >()> | **[ChainlistFetcher](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-chainlistfetcher)** <br/>Fetches the chainlist dataset (JSON text) used to discover public RPC URLs at startup.  |
| using std::function< std::unique_ptr< eth::rpc::JsonRpcTransport >(const std::string &url, std::chrono::seconds timeout)> | **[TransportFactory](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-transportfactory)** <br/>Factory callable that produces a JsonRpcTransport from a URL and timeout.  |
| using std::pair< std::string, [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) > | **[EscrowDataPair](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-escrowdatapair)**  |
| using std::pair< std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) >, std::vector< [OutputDestInfo](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/) > > | **[UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters)** <br/>Pair of signed inputs and destination outputs that make up a UTXO transaction payload.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[BridgeRelayerLogger](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-bridgerelayerlogger)**()<br/>Returns a new instance of the [BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/) logger.  |
| [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[InputValidatorLogger](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-inputvalidatorlogger)**() |
| [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[GeniusNodeLogger](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-geniusnodelogger)**() |
| std::string | **[generate_uuid_with_ipfs_id](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-generate_uuid_with_ipfs_id)**(const std::string & ipfs_id) |
| [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[TransactionManagerLogger](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-transactionmanagerlogger)**() |
| template <size_t N,class Stream \> <br/>Stream & | **[operator<<](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-operator<<)**(Stream & s, const [Unused](/source-reference/Classes/da/dac/structsgns_1_1_unused/)< N > & ) |
| template <size_t N,class Stream \> <br/>Stream & | **[operator>>](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-operator>>)**(Stream & s, [Unused](/source-reference/Classes/da/dac/structsgns_1_1_unused/)< N > & ) |
| std::string | **[to_string](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-to_string)**(const std::vector< unsigned char > & bytes)<br/>Convert a byte array to a hexadecimal string.  |
| bool | **[isLittleEndian](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-islittleendian)**()<br/>Checks if the architecture is little endian.  |
| template <typename T \> <br/>T | **[Vector2Num](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-vector2num)**(const std::vector< uint8_t > & bytes)<br/>Converts a little-endian byte vector into a number.  |
| uint128_t | **[Vector2Num](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-vector2num)**(const std::vector< uint8_t > & bytes) |
| uint256_t | **[Vector2Num](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-vector2num)**(const std::vector< uint8_t > & bytes) |
| template <typename T \> <br/>std::vector< uint8_t > | **[Num2Vector](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-num2vector)**(const T & num, std::size_t num_bytes_resolution =sizeof(T))<br/>Converts a number into a byte vector (little-endian).  |
| template <typename T \> <br/>T | **[HexASCII2Num](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-hexascii2num)**(const char * p_char, std::size_t num_nibbles_resolution =sizeof(T) *2)<br/>Converts a hexadecimal ASCII char array into a number.  |
| template <typename T \> <br/>std::vector< T > | **[HexASCII2NumStr](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-hexascii2numstr)**(const char * p_char, std::size_t char_ptr_size)<br/>Converts a hexadecimal ASCII char array into a vector of numbers.  |
| template <typename T \> <br/>std::enable_if_t< std::is_same_v< typename T::value_type, uint8_t > > | **[AdjustEndianess](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-adjustendianess)**(T & data, std::optional< typename T::iterator > start =std::nullopt, std::optional< typename T::iterator > finish =std::nullopt)<br/>Adjust endianess if needed.  |
| std::string | **[Uint256ToString](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-uint256tostring)**(const uint256_t & value) |
| template <class... Fs\> <br/>auto | **[make_visitor](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-make_visitor)**(Fs &&... fs)<br/>Creates a compile-time visitor from a set of lambdas.  |
| template <typename TVariant ,typename... TVisitors\> <br/>decltype(auto) | **[visit_in_place](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-visit_in_place)**(TVariant && variant, TVisitors &&... visitors)<br/>Applies an in-place visitor to a boost::variant.  |
| template <typename T ,typename Matcher \> <br/>decltype(auto) | **[match](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-match)**(T && t, Matcher && m)<br/>apply Matcher to optional T  |
| template <typename T ,typename... Fs\> <br/>decltype(auto) | **[match_in_place](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-match_in_place)**(T && t, Fs &&... fs)<br/>construct visitor from Fs and apply it to optional T  |
| [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[ConsensusManagerLogger](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-consensusmanagerlogger)**() |
| outcome::result< std::vector< uint8_t > > | **[ProposalSigningBytes](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-proposalsigningbytes)**(const ConsensusProposal & proposal)<br/>Builds canonical bytes used to sign a consensus proposal.  |
| outcome::result< std::vector< uint8_t > > | **[VoteSigningBytes](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-votesigningbytes)**(const ConsensusVote & vote)<br/>Builds canonical bytes used to sign a consensus vote.  |
| outcome::result< std::vector< uint8_t > > | **[VoteBundleSigningBytes](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-votebundlesigningbytes)**(const ConsensusVoteBundle & bundle)<br/>Builds canonical bytes used to sign a consensus vote bundle.  |
| outcome::result< std::string > | **[ComputeProposalId](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-computeproposalid)**(const ConsensusProposal & proposal)<br/>Computes deterministic proposal id from proposal content.  |
| bool | **[ValidateProposal](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-validateproposal)**(const ConsensusProposal & proposal)<br/>Validates proposal basic shape, signature, and computed id.  |
| std::string | **[decodeChunkedTransfer](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-decodechunkedtransfer)**(const std::string & chunkedData) |
| [GeniusProver::ProofType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-prooftype) | **[GetSnarkFromProto](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-getsnarkfromproto)**(const SGProof::BaseProofData & proof_proto_data) |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[HashLeaf](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-hashleaf)**(const std::vector< uint8_t > & payload)<br/>Hashes a serialized UTXO leaf payload with the leaf domain separator.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[HashNode](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-hashnode)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & left, const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & right)<br/>Hashes two child nodes with the internal-node domain separator.  |
| std::string | **[OutPointKey](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-outpointkey)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & txid, uint32_t idx)<br/>Generates a canonical key for a UTXO outpoint, used for deterministic ordering in Merkle tree construction.  |
| void | **[AppendUInt32BE](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-appenduint32be)**(std::vector< uint8_t > & out, uint32_t value)<br/>Appends a 32-bit unsigned integer in big-endian order.  |
| void | **[AppendUInt64BE](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-appenduint64be)**(std::vector< uint8_t > & out, uint64_t value)<br/>Appends a 64-bit unsigned integer in big-endian order.  |
| uint32_t | **[ReadUInt32BE](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-readuint32be)**(const uint8_t * data)<br/>Reads a 32-bit unsigned integer from big-endian bytes.  |
| uint64_t | **[ReadUInt64BE](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-readuint64be)**(const uint8_t * data)<br/>Reads a 64-bit unsigned integer from big-endian bytes.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[HashLeaf](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-hashleaf)**(const std::vector< uint8_t > & payload)<br/>Hashes a serialized UTXO leaf payload with the leaf domain separator.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[HashNode](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-hashnode)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & left, const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & right)<br/>Hashes two child nodes with the internal-node domain separator.  |
| std::string | **[OutPointKey](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-outpointkey)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & txid, uint32_t idx)<br/>Generates a canonical key for a UTXO outpoint, used for deterministic ordering in Merkle tree construction.  |
| uint32_t | **[ReadUInt32BE](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-readuint32be)**(const uint8_t * data)<br/>Reads a 32-bit unsigned integer from big-endian bytes.  |
| uint64_t | **[ReadUInt64BE](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-readuint64be)**(const uint8_t * data)<br/>Reads a 64-bit unsigned integer from big-endian bytes.  |
| std::vector< uint8_t > | **[SerializeUTXOLeafPayload](/source-reference/Namespaces/d2/d2b/namespacesgns/#function-serializeutxoleafpayload)**(const [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) & utxo)<br/>Serializes a UTXO into the canonical leaf payload used for Merkle hashing.  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| std::string_view | **[kBridgeSourceBurnedSig](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-kbridgesourceburnedsig)** <br/>Canonical Solidity event signatures for bridge events. Single source of truth — shared by watch registration, catch-up scan, and RPC endpoint validation.  |
| std::string_view | **[kBridgeOutInitiatedSig](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-kbridgeoutinitiatedsig)**  |
| bool | **[kGeniusValidatorRegistered](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-kgeniusvalidatorregistered)**  |
| bool | **[kMigrationValidatorRegistered](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-kmigrationvalidatorregistered)** <br/>Static instance to trigger registration of the [MigrationInputValidator](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/) before main() starts.  |
| size_t | **[MAX_PUBSUB_TX_BYTES](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-max_pubsub_tx_bytes)**  |
| std::string_view | **[NONCE_SUBJECT_TYPE](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-nonce_subject_type)**  |
| std::string_view | **[TASK_RESULT_SUBJECT_TYPE](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-task_result_subject_type)**  |
| std::string_view | **[REGISTRY_BATCH_SUBJECT_TYPE](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-registry_batch_subject_type)**  |
| std::string_view | **[FILE_NAME](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-file_name)**  |
| size_t | **[HASH256_BYTES](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-hash256_bytes)**  |
| size_t | **[SERIALIZED_UINT32_BYTES](/source-reference/Namespaces/d2/d2b/namespacesgns/#variable-serialized_uint32_bytes)**  |

## Types Documentation

### using ChainlistFetcher

```cpp
using sgns::ChainlistFetcher = std::function<std::optional<std::string>()>;
```

Fetches the chainlist dataset (JSON text) used to discover public RPC URLs at startup. 

**Return**: The chainlist JSON text, or std::nullopt on fetch failure. 

Production default: HTTPS GET of [https://chainid.network/chains.json](https://chainid.network/chains.json). Tests inject a callable returning canned JSON (no network).


### using TransportFactory

```cpp
using sgns::TransportFactory = std::function<std::unique_ptr<eth::rpc::JsonRpcTransport>( const std::string   &url,
                                                                                       std::chrono::seconds timeout )>;
```

Factory callable that produces a JsonRpcTransport from a URL and timeout. 

**Parameters**: 

  * **url** RPC endpoint URL. 
  * **timeout** Transport operation timeout. 


**Return**: Unique ownership of a transport implementing JsonRpcTransport. 

Injected via SetTransportFactory(). When not set, the default factory creates real RpcHttpTransport instances (production path per D-16). Tests inject a factory that returns MockRpcTransport instances (D-07, D-14).


### using EscrowDataPair

```cpp
using sgns::EscrowDataPair = std::pair<std::string, base::Buffer>;
```


### using UTXOTxParameters

```cpp
using sgns::UTXOTxParameters = std::pair<std::vector<InputUTXOInfo>, std::vector<OutputDestInfo>>;
```

Pair of signed inputs and destination outputs that make up a UTXO transaction payload. 


## Functions Documentation

### function BridgeRelayerLogger

```cpp
base::Logger BridgeRelayerLogger()
```

Returns a new instance of the [BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/) logger. 

**Return**: Logger instance for [BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/). 

**Note**: This is used for 2 reasons: (1) to enable logging on static methods, and (2) to avoid static initialization order issues when its created before the one with the same name on [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/), which can have the output configured to file. If we initialize this logger statically it could end up outputing to console instead. 

### function InputValidatorLogger

```cpp
base::Logger InputValidatorLogger()
```


### function GeniusNodeLogger

```cpp
base::Logger GeniusNodeLogger()
```


### function generate_uuid_with_ipfs_id

```cpp
std::string generate_uuid_with_ipfs_id(
    const std::string & ipfs_id
)
```


### function TransactionManagerLogger

```cpp
base::Logger TransactionManagerLogger()
```


### function operator<<

```cpp
template <size_t N,
class Stream >
Stream & operator<<(
    Stream & s,
    const Unused< N > & 
)
```


### function operator>>

```cpp
template <size_t N,
class Stream >
Stream & operator>>(
    Stream & s,
    Unused< N > & 
)
```


### function to_string

```cpp
static std::string to_string(
    const std::vector< unsigned char > & bytes
)
```

Convert a byte array to a hexadecimal string. 

**Parameters**: 

  * **bytes** A vector of bytes to be converted. 


**Return**: A hexadecimal string representation of the bytes. 

### function isLittleEndian

```cpp
static bool isLittleEndian()
```

Checks if the architecture is little endian. 

**Return**: true if little endian, false otherwise 

### function Vector2Num

```cpp
template <typename T >
static T Vector2Num(
    const std::vector< uint8_t > & bytes
)
```

Converts a little-endian byte vector into a number. 

**Parameters**: 

  * **bytes** Byte vector to convert. 


**Template Parameters**: 

  * **T** uint8_t, uint16_t, uint32_t, uint64_t, or supported multiprecision integer types. 


**Return**: The converted number. 

### function Vector2Num

```cpp
uint128_t Vector2Num(
    const std::vector< uint8_t > & bytes
)
```


### function Vector2Num

```cpp
uint256_t Vector2Num(
    const std::vector< uint8_t > & bytes
)
```


### function Num2Vector

```cpp
template <typename T >
static std::vector< uint8_t > Num2Vector(
    const T & num,
    std::size_t num_bytes_resolution =sizeof(T)
)
```

Converts a number into a byte vector (little-endian). 

**Parameters**: 

  * **num** Number to convert. 
  * **num_bytes_resolution** Optional byte resolution (defaults to sizeof(T)). 


**Template Parameters**: 

  * **T** uint8_t, uint16_t, uint32_t or uint64_t 


**Return**: The converted byte vector. 

### function HexASCII2Num

```cpp
template <typename T >
static T HexASCII2Num(
    const char * p_char,
    std::size_t num_nibbles_resolution =sizeof(T) *2
)
```

Converts a hexadecimal ASCII char array into a number. 

**Parameters**: 

  * **p_char** Hexadecimal ASCII char array 
  * **num_nibbles_resolution** How many nibbles will constitute a number 


**Template Parameters**: 

  * **T** uint8_t, uint16_t, uint32_t or uint64_t 


**Return**: The converted number (8-64 bit variable) 

### function HexASCII2NumStr

```cpp
template <typename T >
static std::vector< T > HexASCII2NumStr(
    const char * p_char,
    std::size_t char_ptr_size
)
```

Converts a hexadecimal ASCII char array into a vector of numbers. 

**Parameters**: 

  * **p_char** Hexadecimal ASCII char array 
  * **char_ptr_size** Size of the char array 


**Template Parameters**: 

  * **T** uint8_t, uint16_t, uint32_t or uint64_t 


**Return**: The vector of converted numbers 

### function AdjustEndianess

```cpp
template <typename T >
static std::enable_if_t< std::is_same_v< typename T::value_type, uint8_t > > AdjustEndianess(
    T & data,
    std::optional< typename T::iterator > start =std::nullopt,
    std::optional< typename T::iterator > finish =std::nullopt
)
```

Adjust endianess if needed. 

**Parameters**: 

  * **data** The container of data (vector/array) 
  * **start** Optional beginning of the valid data 
  * **finish** Optional ending of the valid data 


**Template Parameters**: 

  * **T** std::vector<uint8_t> or std::array<uint8_t,N> 


### function Uint256ToString

```cpp
static std::string Uint256ToString(
    const uint256_t & value
)
```


### function make_visitor

```cpp
template <class... Fs>
auto make_visitor(
    Fs &&... fs
)
```

Creates a compile-time visitor from a set of lambdas. 

**Return**: Visitor instance that dispatches to the provided lambdas. 

Example: ```cpp

make_visitor([](int a){ return 1; },
             [](std::string b) { return 2; });
```

This is essentially the same as: ```cpp

struct visitor : public boost::static_visitor<int> {
  int operator()(int a) { return 1; }
  int operator()(std::string b) { return 2; }
};
```


### function visit_in_place

```cpp
template <typename TVariant ,
typename... TVisitors>
decltype(auto) visit_in_place(
    TVariant && variant,
    TVisitors &&... visitors
)
```

Applies an in-place visitor to a boost::variant. 

Example: ```cpp

boost::variant<int, std::string> value = "1234";

visit_in_place(value,
               [](int v) { std::cout << "(int)" << v; },
               [](std::string v) { std::cout << "(string)" << v; });
```


### function match

```cpp
template <typename T ,
typename Matcher >
decltype(auto) match(
    T && t,
    Matcher && m
)
```

apply Matcher to optional T 

### function match_in_place

```cpp
template <typename T ,
typename... Fs>
decltype(auto) match_in_place(
    T && t,
    Fs &&... fs
)
```

construct visitor from Fs and apply it to optional T 

### function ConsensusManagerLogger

```cpp
base::Logger ConsensusManagerLogger()
```


### function ProposalSigningBytes

```cpp
inline outcome::result< std::vector< uint8_t > > ProposalSigningBytes(
    const ConsensusProposal & proposal
)
```

Builds canonical bytes used to sign a consensus proposal. 

**Parameters**: 

  * **proposal** Proposal object to serialize for signing. 


**Return**: Serialized signing bytes on success, or `std::errc::invalid_argument` when protobuf serialization fails. 

The signature field is cleared before serialization so signatures are never part of their own signing payload.


### function VoteSigningBytes

```cpp
inline outcome::result< std::vector< uint8_t > > VoteSigningBytes(
    const ConsensusVote & vote
)
```

Builds canonical bytes used to sign a consensus vote. 

**Parameters**: 

  * **vote** Vote object to serialize for signing. 


**Return**: Serialized signing bytes on success, or `std::errc::invalid_argument` when protobuf serialization fails. 

The signature field is cleared before serialization so signatures are never part of their own signing payload.


### function VoteBundleSigningBytes

```cpp
inline outcome::result< std::vector< uint8_t > > VoteBundleSigningBytes(
    const ConsensusVoteBundle & bundle
)
```

Builds canonical bytes used to sign a consensus vote bundle. 

**Parameters**: 

  * **bundle** Vote bundle to serialize for signing. 


**Return**: Serialized signing bytes on success, or `std::errc::invalid_argument` when protobuf serialization fails. 

The signature field is cleared before serialization so signatures are never part of their own signing payload.


### function ComputeProposalId

```cpp
inline outcome::result< std::string > ComputeProposalId(
    const ConsensusProposal & proposal
)
```

Computes deterministic proposal id from proposal content. 

**Parameters**: 

  * **proposal** Proposal used to derive the identifier. 


**Return**: Lowercase hex SHA-256 proposal id on success, or propagated error when signing bytes cannot be produced. 

The proposal id field is cleared before hashing to guarantee stable id derivation from the signed payload content only.


### function ValidateProposal

```cpp
inline bool ValidateProposal(
    const ConsensusProposal & proposal
)
```

Validates proposal basic shape, signature, and computed id. 

**Parameters**: 

  * **proposal** Proposal to validate. 


**Return**: `true` when proposer id/signature/id are present, signature is valid, and computed proposal id matches; otherwise `false`. 

### function decodeChunkedTransfer

```cpp
std::string decodeChunkedTransfer(
    const std::string & chunkedData
)
```


### function GetSnarkFromProto

```cpp
static GeniusProver::ProofType GetSnarkFromProto(
    const SGProof::BaseProofData & proof_proto_data
)
```


### function HashLeaf

```cpp
inline base::Hash256 HashLeaf(
    const std::vector< uint8_t > & payload
)
```

Hashes a serialized UTXO leaf payload with the leaf domain separator. 

**Parameters**: 

  * **payload** The payload to hash 


**Return**: The hash of the payload as a leaf node in the Merkle tree 

### function HashNode

```cpp
inline base::Hash256 HashNode(
    const base::Hash256 & left,
    const base::Hash256 & right
)
```

Hashes two child nodes with the internal-node domain separator. 

**Parameters**: 

  * **left** The hash of the left child node 
  * **right** The hash of the right child node 


**Return**: The hash of the parent node 

### function OutPointKey

```cpp
inline std::string OutPointKey(
    const base::Hash256 & txid,
    uint32_t idx
)
```

Generates a canonical key for a UTXO outpoint, used for deterministic ordering in Merkle tree construction. 

**Parameters**: 

  * **txid** The transaction hash that created the UTXO 
  * **idx** The output index of the UTXO within the transaction 


**Return**: Canonical string key in the format "txid:idx" where txid is the readable hex representation of the transaction hash 

### function AppendUInt32BE

```cpp
inline void AppendUInt32BE(
    std::vector< uint8_t > & out,
    uint32_t value
)
```

Appends a 32-bit unsigned integer in big-endian order. 

**Parameters**: 

  * **out** The vector to append to 
  * **value** the value to append 


### function AppendUInt64BE

```cpp
inline void AppendUInt64BE(
    std::vector< uint8_t > & out,
    uint64_t value
)
```

Appends a 64-bit unsigned integer in big-endian order. 

**Parameters**: 

  * **out** The vector to append to 
  * **value** the value to append 


### function ReadUInt32BE

```cpp
inline uint32_t ReadUInt32BE(
    const uint8_t * data
)
```

Reads a 32-bit unsigned integer from big-endian bytes. 

**Parameters**: 

  * **data** A pointer to the byte array 


**Return**: the 32 bit unsigned integer represented by the bytes 

### function ReadUInt64BE

```cpp
inline uint64_t ReadUInt64BE(
    const uint8_t * data
)
```

Reads a 64-bit unsigned integer from big-endian bytes. 

**Parameters**: 

  * **data** A pointer to the byte array 


**Return**: the 64 bit unsigned integer represented by the bytes 

### function HashLeaf

```cpp
inline base::Hash256 HashLeaf(
    const std::vector< uint8_t > & payload
)
```

Hashes a serialized UTXO leaf payload with the leaf domain separator. 

**Parameters**: 

  * **payload** The payload to hash 


**Return**: The hash of the payload as a leaf node in the Merkle tree 

### function HashNode

```cpp
inline base::Hash256 HashNode(
    const base::Hash256 & left,
    const base::Hash256 & right
)
```

Hashes two child nodes with the internal-node domain separator. 

**Parameters**: 

  * **left** The hash of the left child node 
  * **right** The hash of the right child node 


**Return**: The hash of the parent node 

### function OutPointKey

```cpp
inline std::string OutPointKey(
    const base::Hash256 & txid,
    uint32_t idx
)
```

Generates a canonical key for a UTXO outpoint, used for deterministic ordering in Merkle tree construction. 

**Parameters**: 

  * **txid** The transaction hash that created the UTXO 
  * **idx** The output index of the UTXO within the transaction 


**Return**: Canonical string key in the format "txid:idx" where txid is the readable hex representation of the transaction hash 

### function ReadUInt32BE

```cpp
inline uint32_t ReadUInt32BE(
    const uint8_t * data
)
```

Reads a 32-bit unsigned integer from big-endian bytes. 

**Parameters**: 

  * **data** A pointer to the byte array 


**Return**: the 32 bit unsigned integer represented by the bytes 

### function ReadUInt64BE

```cpp
inline uint64_t ReadUInt64BE(
    const uint8_t * data
)
```

Reads a 64-bit unsigned integer from big-endian bytes. 

**Parameters**: 

  * **data** A pointer to the byte array 


**Return**: the 64 bit unsigned integer represented by the bytes 

### function SerializeUTXOLeafPayload

```cpp
inline std::vector< uint8_t > SerializeUTXOLeafPayload(
    const GeniusUTXO & utxo
)
```

Serializes a UTXO into the canonical leaf payload used for Merkle hashing. 

**Parameters**: 

  * **utxo** The UTXO to serialize 


**Return**: The serialized leaf payload 


## Attributes Documentation

### variable kBridgeSourceBurnedSig

```cpp
std::string_view kBridgeSourceBurnedSig                                                      =
"BridgeSourceBurned(address,uint256,uint256,uint256,uint256,bytes)";
```

Canonical Solidity event signatures for bridge events. Single source of truth — shared by watch registration, catch-up scan, and RPC endpoint validation. 

**Note**: The old signature with 5 parameters it not supported as it was wrong. 

### variable kBridgeOutInitiatedSig

```cpp
std::string_view kBridgeOutInitiatedSig                                                      =
"BridgeOutInitiated(address,uint256,uint256,uint256,uint256,bytes32,bool)";
```


### variable kGeniusValidatorRegistered

```cpp
static bool kGeniusValidatorRegistered = GeniusInputValidator::Register();
```


### variable kMigrationValidatorRegistered

```cpp
static bool kMigrationValidatorRegistered = MigrationInputValidator::Register();
```

Static instance to trigger registration of the [MigrationInputValidator](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/) before main() starts. 

### variable MAX_PUBSUB_TX_BYTES

```cpp
static size_t MAX_PUBSUB_TX_BYTES = 64 * 1024;
```


### variable NONCE_SUBJECT_TYPE

```cpp
static std::string_view NONCE_SUBJECT_TYPE = "sgns.nonce.v1";
```


### variable TASK_RESULT_SUBJECT_TYPE

```cpp
static std::string_view TASK_RESULT_SUBJECT_TYPE = "sgns.task_result.v1";
```


### variable REGISTRY_BATCH_SUBJECT_TYPE

```cpp
static std::string_view REGISTRY_BATCH_SUBJECT_TYPE = "sgns.registry_batch.v1";
```


### variable FILE_NAME

```cpp
std::string_view FILE_NAME = "secure_storage.json";
```


### variable HASH256_BYTES

```cpp
size_t HASH256_BYTES;
```


### variable SERIALIZED_UINT32_BYTES

```cpp
size_t SERIALIZED_UINT32_BYTES;
```





-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700