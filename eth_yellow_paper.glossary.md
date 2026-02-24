# Ethereum Yellow Paper — Complete Symbol & Notation Glossary

---

## Table of Contents

1. [Greek Letters](#greek-letters)
2. [Latin Letters & Variables](#latin-letters--variables)
3. [Functions](#functions)
4. [Mathematical Operators & Notation](#mathematical-operators--notation)
5. [Set Notation](#set-notation)
6. [Subscript & Superscript Notation](#subscript--superscript-notation)
7. [Account State Fields](#account-state-fields)
8. [Transaction Fields](#transaction-fields)
9. [Block Header Fields](#block-header-fields)
10. [Transaction Receipt Fields](#transaction-receipt-fields)
11. [Withdrawal Fields](#withdrawal-fields)
12. [Log Entry Fields](#log-entry-fields)
13. [Machine State Fields](#machine-state-fields)
14. [Execution Environment Fields](#execution-environment-fields)
15. [Accrued Substate Fields](#accrued-substate-fields)
16. [Gas Constants](#gas-constants)
17. [EVM Opcodes Reference](#evm-opcodes-reference)

---

## Greek Letters

| Symbol | Name | Meaning |
|--------|------|---------|
| σ | sigma | The **world state** — the mapping of all addresses to their account states |
| σ' | sigma prime | The state **after** a transition (e.g., after a transaction executes) |
| σ₀ | sigma zero | The **checkpoint** state (state at the start of a transaction, after nonce/balance adjustments) |
| σ* | sigma star | An **intermediate** state during processing |
| σ** | sigma double-star | The state resulting from EVM code execution |
| σ_P | sigma P | The **provisional** post-execution state |
| μ | mu | The **machine state** of the EVM (gas, program counter, memory, stack, etc.) |
| μ' | mu prime | The updated machine state after one instruction cycle |
| μ_g | mu g | Gas available in the machine state |
| μ_pc | mu pc | Program counter (current instruction position) |
| μ_m | mu m | Memory contents |
| μ_i | mu i | Active number of 32-byte words in memory |
| μ_s | mu s | Stack contents |
| μ_o | mu o | Return data buffer (output from most recent sub-call) |
| Υ | upsilon | The **state transition function** — applies a transaction to the world state |
| Υ^g | upsilon g | Gas **used** by a transaction |
| Υ^l | upsilon l | **Logs** created by a transaction |
| Υ^z | upsilon z | **Status code** of a transaction (0 = fail, 1 = success) |
| Ξ | xi (capital) | The **execution function** — runs EVM code and returns results |
| Ξ_PRE | xi PRE | Template execution function for **precompiled contracts** |
| Ξ_ECREC | xi ECREC | Precompiled contract: ECRECOVER (address 1) |
| Ξ_SHA256 | xi SHA256 | Precompiled contract: SHA-256 hash (address 2) |
| Ξ_RIP160 | xi RIP160 | Precompiled contract: RIPEMD-160 hash (address 3) |
| Ξ_ID | xi ID | Precompiled contract: Identity / data copy (address 4) |
| Ξ_EXPMOD | xi EXPMOD | Precompiled contract: Modular exponentiation (address 5) |
| Ξ_BN_ADD | xi BN_ADD | Precompiled contract: Elliptic curve addition on G₁ (address 6) |
| Ξ_BN_MUL | xi BN_MUL | Precompiled contract: Elliptic curve scalar multiplication on G₁ (address 7) |
| Ξ_SNARKV | xi SNARKV | Precompiled contract: zkSNARK pairing check (address 8) |
| Ξ_BLAKE2_F | xi BLAKE2_F | Precompiled contract: BLAKE2 compression (address 9) |
| Λ | lambda (capital) | The **contract creation** function |
| Θ | theta (capital) | The **message call** function |
| Π | pi (capital) | The **block-level state transition** function (processes all transactions in a block) |
| π | pi (lowercase) | The set of **precompiled contract addresses** {1, 2, 3, 4, 5, 6, 7, 8, 9} |
| Φ | phi (capital) | The **block transition function** (maps incomplete block to complete block) |
| Γ | gamma (capital) | The function that maps a block to its **initial (pre-transaction) state** |
| β | beta | The **chain ID** of the network (e.g., 1 for Ethereum mainnet) |
| δ | delta (lowercase) | The number of stack items **removed** (popped) by an instruction |
| α | alpha (lowercase) | The number of stack items **added** (pushed) by an instruction |
| Δ | delta (capital) | **Net stack change**: α - δ (items added minus items removed) |
| τ | tau | The **gas target** — half the block gas limit (gasLimit / ρ) |
| ρ | rho | The **elasticity multiplier** = 2 (gas target = gasLimit / 2) |
| ν | nu | The magnitude of the **base fee change** per block |
| ξ | xi (lowercase) | The **base fee max change denominator** = 8 (max 12.5% change per block) |
| ζ | zeta | The **salt** for CREATE2 (32 bytes, or empty for CREATE) |
| λ | lambda (lowercase) | The **slope** used in elliptic curve point addition |
| δ_p | delta p | Function that validates a field element for G₁ (checks x < p) |
| δ₁ | delta 1 | Function that validates a G₁ curve point from 64 bytes |
| δ₂ | delta 2 | Function that validates a G₂ curve point from 128 bytes |

---

## Latin Letters & Variables

| Symbol | Meaning |
|--------|---------|
| a | An account **address** |
| B | A **block** |
| B_H | Block **header** |
| B_T | Block **transactions** (ordered list) |
| B_U | Block **ommer/uncle headers** (deprecated, always empty) |
| B_W | Block **withdrawals** |
| B_R | Block **receipts** |
| B_t | **Total difficulty** of a block |
| b | Code body (bytecode) of a contract |
| C | The **gas cost function** for an instruction |
| C_mem | **Memory** gas cost function |
| C_SSTORE | Gas cost function for **SSTORE** |
| C_SLOAD | Gas cost function for **SLOAD** |
| C_CALL | Gas cost function for **CALL** |
| C_CALLGAS | Gas allocated to a **sub-call** |
| C_GASCAP | Gas **cap** for a sub-call |
| C_EXTRA | **Extra** gas cost for CALL (access + value + new account) |
| C_XFER | Gas cost for **value transfer** in CALL |
| C_NEW | Gas cost for **new account** creation in CALL |
| C_access | **Access cost** function (warm vs cold) |
| c | Code-deposit cost (for contract creation) OR node composition function (in trie) |
| D | The set of **valid JUMP destinations** in bytecode |
| D_J | Recursive helper for computing valid jump destinations |
| d | Input **data** of a message call |
| E | Withdrawal state transition function OR access list entry |
| E_a | Access list entry: **address** |
| E_s | Access list entry: **storage keys** |
| e | The current **call/creation depth** |
| F | The **exception condition** flag (true if contract creation should fail) |
| F(H) | The **base fee** calculation function |
| F_London | The initial base fee at the London fork = 1000000000 (1 Gwei) |
| f | The **priority fee** per gas |
| G | Various **gas cost constants** (see Gas Constants section) |
| g | **Available gas** |
| g' | **Remaining gas** after execution |
| g* | **Total refundable gas** |
| g₀ | **Intrinsic gas** (minimum gas a transaction needs) |
| H | Block **header** OR the **normal halting function** |
| H(μ, I) | The normal **halting function** — returns output data or ∅ |
| H_RETURN(μ) | Extracts **return data** from memory |
| h(T) | The **hash** of a transaction (for signing) |
| I | The **execution environment** tuple |
| i | **Init code** (for contract creation) |
| K | The block-level **withdrawal** state transition function |
| k | A storage **key** (32 bytes) |
| L | The "all but one 64th" function: L(n) = n - ⌊n/64⌋ |
| L_A | Address generation function for CREATE/CREATE2 |
| L_B | Block **serialisation** function |
| L_H | Block header **serialisation** function |
| L_R | Receipt **serialisation** function |
| L_S | World state **collapse** function (for trie encoding) |
| L_T | Transaction **serialisation** function |
| L̃_T | Transaction serialisation with **EIP-2718 type prefix** |
| L_W | Withdrawal **serialisation** function |
| L_X | Transaction content for **signing** |
| L₁ | Base transformation for storage trie key/value pairs |
| L*_i | Collapse function for storage trie key/value pairs |
| l | Length |
| M | The **Bloom filter** function OR the **memory-expansion** function |
| M(s, f, l) | Memory expansion: ensures memory covers offset f with length l |
| M_{3:2048} | Bloom filter sub-function (sets 3 bits in a 2048-bit array) |
| m | Gas price used for balance check (T_p or T_m depending on tx type) |
| N | The function that returns the **next valid instruction position** |
| n | Block **number** OR nonce OR number of items |
| O | A single **execution cycle** of the EVM (one instruction) |
| o | **Output** data from execution |
| P | The function that returns a block's **parent block** |
| P(H) | The **parent block** of block with header H |
| p | The **effective gas price** |
| p(a) | The encoding of account a for the state trie |
| p_r | A **private key** (32 bytes) |
| p_u | A **public key** (64 bytes) |
| R | A transaction **receipt** OR the initcode cost function |
| R(x) | Initcode cost: G_initcodeword × ⌈x/32⌉ |
| r | **Recipient** address (in message call) |
| S | The **sender** recovery function: S(T) recovers who sent transaction T |
| S(T) | The **sender** of transaction T |
| s | **Sender** address |
| T | A **transaction** |
| t | The **to** address or topics in a log |
| V | Block header **validity** function: V(H) |
| v | **Value** in Wei to transfer OR a storage value |
| v₀ | **Up-front cost** of a transaction |
| v' | Pre-existing balance of an account |
| ṽ | **Apparent value** (for DELEGATECALL — the original call's value) |
| W | A **withdrawal** OR the function checking **state-modifying operations** |
| w | The current **opcode** being executed |
| X | The **iterative execution** function (main EVM loop) |
| x | General variable |
| Z | The **exceptional halting** function |
| z | **Status code** (0 = failure, 1 = success) |

---

## Functions

| Function | Meaning |
|----------|---------|
| KEC(x) | **Keccak-256** hash of x. Ethereum's primary hash function. Takes any input, outputs 32 bytes. |
| KEC512(x) | **Keccak-512** hash of x. Outputs 64 bytes. Used in Ethash. |
| RLP(x) | **Recursive Length Prefix** encoding of x. Ethereum's serialisation format. |
| R_b(x) | RLP encoding of a **byte array** x |
| R_l(x) | RLP encoding of a **list** x |
| TRIE(𝔍) | Root hash of the **Merkle Patricia Trie** built from key-value set 𝔍 |
| HP(x, t) | **Hex-Prefix** encoding of nibble sequence x with flag t |
| BE(x) | **Big-Endian** encoding — converts integer x to minimal-length bytes, most significant first |
| BE_k(x) | **Big-Endian** k-byte encoding of integer x |
| LE_k(x) | **Little-Endian** k-byte encoding of integer x |
| SHA256(x) | **SHA-256** hash function |
| RIPEMD160(x) | **RIPEMD-160** hash function |
| ECDSAPUBKEY(p_r) | Derives a 64-byte **public key** from a 32-byte private key |
| ECDSASIGN(e, p_r) | **Signs** hash e with private key p_r → returns (v, r, s) |
| ECDSARECOVER(e, v, r, s) | **Recovers** the public key from hash e and signature (v, r, s) |
| ADDR(s, n, ζ, i) | Computes the **address** of a new contract from sender, nonce, salt, init code |
| EMPTY(σ, a) | True if account a is **empty** (no code, zero nonce, zero balance) |
| DEAD(σ, a) | True if account a is **dead** (non-existent or empty) |
| S(T) | Recovers the **sender address** of transaction T from its signature |
| A(p_r) | Derives the **Ethereum address** from private key p_r |
| G(T, p_r) | Produces a **signed transaction** from T and private key p_r |
| F(H) | Calculates the **base fee** for block with header H |
| V(H) | Checks **block header validity** for header H |
| J_JUMP(μ) | Returns the **JUMP destination** (top of stack) |
| J_JUMPI(μ) | Returns the **JUMPI destination** (conditional: top of stack if condition true, else pc+1) |
| H(μ, I) | The **normal halting** function — returns output or ∅ if not halting |
| H_RETURN(μ) | Extracts **return data** from memory for RETURN/REVERT |
| Z(σ, μ, A, I) | The **exceptional halting** function — true if execution should crash |
| W(w, μ) | Checks if instruction w is **state-modifying** (forbidden in STATICCALL) |
| D(c) | Returns the set of **valid JUMP destinations** in code c |
| D_J(c, i) | Recursive helper for building jump destination set from position i |
| N(i, w) | Returns the **next instruction position** after position i with opcode w |
| E_prime(x, y) | Finds the largest **prime** ≤ x (used for Ethash sizes) |
| E_FNV(x, y) | **FNV hash**: (x × (0x01000193 ⊕ y)) mod 2³² |
| E_epoch(H_i) | Computes the **Ethash epoch** number: ⌊H_i / 30000⌋ |
| PREVRANDAO() | Returns the **RANDAO** value from the previous block's Beacon Chain state |
| PoW(H_M, H_n, d) | The Ethash **Proof of Work** function (deprecated post-Merge) |

---

## Mathematical Operators & Notation

| Symbol | Name | Meaning |
|--------|------|---------|
| ≡ | equivalence | "is defined as" or "is identical to" |
| = | equals | Equality (in equations and conditions) |
| ∧ | logical AND | Both conditions must be true |
| ∨ | logical OR | At least one condition must be true |
| ¬ | logical NOT | Negation — flips true↔false |
| ∀ | for all | "For every" — universal quantifier |
| ∃ | there exists | "There is at least one" — existential quantifier |
| ∈ | element of | "belongs to" or "is a member of" |
| ∉ | not element of | "does not belong to" |
| ⊆ | subset | Every element of the left set is in the right set |
| ∅ | empty set / nil | Nothing / non-existent / undefined |
| () | empty sequence | An empty tuple or list (distinct from ∅) |
| ⊎ | disjoint union | Union of two non-overlapping sets |
| ∪ | union | Combination of two sets (all elements from both) |
| ∩ | intersection | Elements common to both sets |
| \ | set difference | Elements in left set but not in right set |
| ⊕ | XOR | Bitwise exclusive OR |
| · | concatenation | Joining two sequences end-to-end (also used for multiplication) |
| ‖x‖ | length / norm | The number of elements (bytes) in sequence x |
| ⌊x⌋ | floor | Round **down** to nearest integer. ⌊3.7⌋ = 3 |
| ⌈x⌉ | ceiling | Round **up** to nearest integer. ⌈3.2⌉ = 4 |
| mod | modulo | Remainder after division. 7 mod 3 = 1 |
| ÷ | division | Integer division (same as ⌊a/b⌋) |
| × | multiplication | Standard multiplication |
| x[a..b] | byte slice | Bytes from position a to b (inclusive) of x |
| x[a] | index | The element at position a in sequence x (0-indexed) |
| 𝔹₉₆..₂₅₅(x) | bit slice | Bits 96–255 of x = the last 160 bits = last 20 bytes |
| sgn(x) | sign function | +1 if x > 0, −1 if x < 0, 0 if x = 0 |
| log₂(x) | logarithm | Base-2 logarithm |
| log₂₅₆(x) | logarithm | Base-256 logarithm (≈ number of bytes needed to represent x) |
| 2²⁵⁶ | exponentiation | 2 raised to the 256th power |
| ∑ | summation | Sum of a series of values |
| ∏ | product | Product of a series of values |
| ⊥ | bottom / false | Represents false or "no permission" (used for I_w in STATICCALL) |
| ℓ(x) | last element | The last element of sequence x |

---

## Set Notation

| Symbol | Name | Meaning |
|--------|------|---------|
| 𝔹 | byte arrays | The set of **all** byte arrays (any length) |
| 𝔹_n | n-byte arrays | The set of all byte arrays of **exactly** length n |
| 𝔹₀ | empty bytes | The set containing only the empty byte array |
| 𝔹₁ | 1-byte arrays | All single-byte values |
| 𝔹₂₀ | 20-byte arrays | All possible Ethereum **addresses** |
| 𝔹₃₂ | 32-byte arrays | All possible 256-bit **hashes/words** |
| 𝔹₆₄ | 64-byte arrays | All possible **public keys** |
| 𝔹₂₅₆ | 256-byte arrays | **Bloom filter** size |
| 𝔹₅₁₂ | 512-byte arrays | Used in G₂ point representation |
| 𝔹₁₀₂₄ | 1024-byte arrays | Used in G₂ point representation |
| ℕ | natural numbers | Non-negative integers: {0, 1, 2, 3, ...} |
| ℕ_n | bounded naturals | Non-negative integers less than 2^n: {0, 1, ..., 2^n − 1} |
| ℕ₆₄ | 64-bit naturals | {0, 1, ..., 2⁶⁴ − 1} |
| ℕ₂₅₆ | 256-bit naturals | {0, 1, ..., 2²⁵⁶ − 1} — all possible EVM stack values |
| ℕ₁ | 1-bit naturals | {0, 1} |
| 𝕆 | octets | The set of all 8-bit values: {0, 1, ..., 255} |
| 𝕋 | structures | All possible RLP-encodable structures (𝕃 ⊎ 𝔹) |
| 𝕃 | lists | All tree-like (recursive) list structures |
| 𝕐 | nibbles | The set of all 4-bit values: {0, 1, ..., 15} |
| F_p | finite field | Integers modulo prime p (elliptic curve math) |
| F_{p²} | extension field | Quadratic extension of F_p (for G₂ curve) |
| C₁ | curve G₁ | BN128 elliptic curve: Y² = X³ + 3 over F_p |
| C₂ | curve G₂ | BN128 elliptic curve over F_{p²} |
| G₁ | group 1 | Cyclic subgroup of C₁ used in zkSNARK |
| G₂ | group 2 | Cyclic subgroup of C₂ used in zkSNARK |
| G_T | target group | Target group of the bilinear pairing |
| P_T | pairing target | Generator of G_T |
| P₁ | generator G₁ | The point (1, 2) that generates G₁ |
| P₂ | generator G₂ | The specific point that generates G₂ |

---

## Subscript & Superscript Notation

| Notation | Meaning |
|----------|---------|
| x' | x **prime** — the value after an operation/transition |
| x'' | x **double prime** — after a second operation |
| x* | x **star** — an intermediate value |
| x** | x **double-star** — another intermediate value |
| x₀ | Initial value or value at index 0 |
| x[n] | The nth element (0-indexed) |
| σ[a] | The **account state** of address a in world state σ |
| σ[a]_n | Account a's **nonce** |
| σ[a]_b | Account a's **balance** |
| σ[a]_s | Account a's **storage root** (or a specific storage value when used as σ[a]_s[k]) |
| σ[a]_c | Account a's **code hash** |
| P(H)_{H_x} | Field x of the **parent block's** header |
| ℓ(x) | The **last element** of sequence x |
| 0_n | A sequence of n **zero bits** or zero bytes |
| 0₂₅₆ | 256 zero bits (32 zero bytes) |
| 0₁₆₀ | 160 zero bits (20 zero bytes) |
| 0₂₀₄₈ | 2048 zero bits (256 zero bytes) — empty Bloom filter |

---

## Account State Fields

| Symbol | Formal | Meaning |
|--------|--------|---------|
| σ[a]_n | nonce | Number of transactions sent (EOA) or contracts created (contract) |
| σ[a]_b | balance | Amount of **Wei** owned by this account |
| σ[a]_s | storageRoot | 256-bit hash of the root of the account's **storage trie** |
| σ[a]_c | codeHash | Keccak-256 hash of the account's **EVM code**. For EOAs: KEC(()) |

---

## Transaction Fields

| Symbol | Formal Name | Meaning |
|--------|-------------|---------|
| T_x | type | Transaction type: 0 (legacy), 1 (EIP-2930), or 2 (EIP-1559) |
| T_n | nonce | Sender's transaction count (must match current account nonce) |
| T_p | gasPrice | Wei per unit of gas (type 0 and 1 only) |
| T_g | gasLimit | Maximum gas this transaction can consume |
| T_t | to | Recipient address (160-bit/20-byte), or ∅ for contract creation |
| T_v | value | Wei to transfer to the recipient |
| T_r | r | ECDSA signature component r |
| T_s | s | ECDSA signature component s |
| T_y | yParity | Signature recovery parity (0 or 1) — type 1 and 2 |
| T_w | w | Combined chainId + yParity for legacy (type 0) transactions |
| T_c | chainId | Network identifier (1 = mainnet). Type 1 and 2 only. |
| T_A | accessList | List of (address, storageKeys) to pre-warm. Type 1 and 2 only. |
| T_m | maxFeePerGas | Absolute maximum Wei per gas the sender will pay. Type 2 only. |
| T_f | maxPriorityFeePerGas | Maximum tip to validator per gas. Type 2 only. |
| T_i | init | Contract initialisation bytecode (for contract creation tx) |
| T_d | data | Input data (calldata) for message call transactions |

---

## Block Header Fields

| Symbol | Formal Name | Meaning |
|--------|-------------|---------|
| H_p | parentHash | Keccak-256 hash of the parent block's entire header |
| H_o | ommersHash | Hash of the ommer list. Deprecated: always KEC(RLP(())) |
| H_c | beneficiary | Address receiving priority fees (the validator's reward address) |
| H_r | stateRoot | Root hash of the world state trie after processing this block |
| H_t | transactionsRoot | Root hash of the transactions trie for this block |
| H_e | receiptsRoot | Root hash of the transaction receipts trie |
| H_b | logsBloom | 2048-bit (256-byte) Bloom filter of all logs in this block |
| H_d | difficulty | Deprecated post-Merge: always 0 |
| H_i | number | Block number (genesis = 0) |
| H_l | gasLimit | Maximum total gas allowed in this block |
| H_g | gasUsed | Total gas actually consumed by all transactions |
| H_s | timestamp | Unix timestamp (seconds since 1970-01-01) of block creation |
| H_x | extraData | Arbitrary validator-chosen data, max 32 bytes |
| H_a | prevRandao | RANDAO mix from the previous Beacon Chain block (post-Merge randomness) |
| H_n | nonce | Deprecated post-Merge: always 0x0000000000000000 |
| H_f | baseFeePerGas | Minimum gas price; this portion is **burned** (EIP-1559) |
| H_w | withdrawalsRoot | Root hash of the withdrawals trie |

---

## Transaction Receipt Fields

| Symbol | Formal Name | Meaning |
|--------|-------------|---------|
| R_x | type | Transaction type (matches the transaction) |
| R_z | statusCode | 0 = transaction failed, 1 = transaction succeeded |
| R_u | cumulativeGasUsed | Total gas used by all transactions up to and including this one |
| R_b | logsBloom | 256-byte Bloom filter for this transaction's logs |
| R_l | logs | The sequence of log entries emitted during execution |

---

## Withdrawal Fields

| Symbol | Formal Name | Meaning |
|--------|-------------|---------|
| W_g | globalIndex | Unique, ever-increasing withdrawal ID |
| W_v | validatorIndex | Which validator is withdrawing staked ETH |
| W_r | recipient | 20-byte address that receives the withdrawn Ether |
| W_a | amount | Withdrawal amount in **Gwei** (1 Gwei = 10⁹ Wei = 0.000000001 ETH) |

---

## Log Entry Fields

| Symbol | Formal Name | Meaning |
|--------|-------------|---------|
| O_a | address | The 20-byte address of the contract that emitted the log |
| O_t | topics | Up to 4 indexed 32-byte values used for filtering and searching |
| O_d | data | Arbitrary-length byte array of non-indexed log data |

---

## Machine State Fields

| Symbol | Meaning |
|--------|---------|
| μ_g | **Gas** available for execution |
| μ_pc | **Program counter** — byte position of the current instruction in the bytecode |
| μ_m | **Memory** contents (volatile byte array, all zeros initially) |
| μ_i | **Active memory** size in 32-byte words |
| μ_s | **Stack** contents (LIFO structure, max 1024 items, each 256-bit) |
| μ_s[0] | **Top** of stack (most recently pushed item) |
| μ_s[1] | **Second** item from top of stack |
| μ_s[n] | The (n+1)th item from the top of the stack |
| μ_o | **Return data** buffer — output from the most recent external call |
| μ'_s[0] | New top-of-stack value **after** instruction execution |
| μ'_g | Gas remaining **after** instruction execution |
| μ'_m | Memory **after** instruction execution |
| μ'_i | Active memory size **after** instruction execution |
| μ'_pc | Program counter **after** instruction execution |

---

## Execution Environment Fields

| Symbol | Formal Name | Meaning |
|--------|-------------|---------|
| I_a | address | Address of the account **owning** the executing code |
| I_o | origin | Address of the **original** transaction sender (always the EOA) |
| I_p | gasPrice | **Effective gas price** for this execution |
| I_d | data | **Input data** (calldata) byte array |
| I_s | sender | Address that **directly caused** this execution (the caller) |
| I_v | value | **Wei** sent with this call (apparent value for DELEGATECALL) |
| I_b | code | The **bytecode** being executed |
| I_H | blockHeader | The current **block's header** |
| I_e | depth | Current **call/creation depth** (increments with each CALL/CREATE) |
| I_w | permission | Whether **state modifications** are allowed (false = read-only/STATICCALL) |

---

## Accrued Substate Fields

| Symbol | Formal Name | Meaning |
|--------|-------------|---------|
| A_s | selfDestructSet | Set of accounts scheduled for **deletion** after the transaction |
| A_l | logs | Ordered sequence of **log entries** (events) emitted during execution |
| A_t | touchedAccounts | Set of accounts that were **interacted with** during execution |
| A_r | refundBalance | Accumulated gas **refund** counter (e.g., from clearing storage) |
| A_a | accessedAddresses | Set of **addresses** accessed during this transaction (warm/cold pricing) |
| A_K | accessedStorageKeys | Set of **(address, storageKey)** pairs accessed (warm/cold pricing) |
| A⁰ | emptySubstate | Initial substate: (∅, (), ∅, 0, π, ∅) — only precompile addresses are pre-warmed |

---

## Gas Constants

| Constant | Value | Description |
|----------|-------|-------------|
| G_zero | 0 | Free operations: STOP, RETURN, REVERT |
| G_jumpdest | 1 | JUMPDEST marker |
| G_base | 2 | Basic ops: ADDRESS, ORIGIN, CALLER, CALLVALUE, etc. |
| G_verylow | 3 | Simple arithmetic: ADD, SUB, AND, OR, XOR, PUSH, DUP, SWAP, etc. |
| G_low | 5 | Moderate arithmetic: MUL, DIV, MOD, SIGNEXTEND, SELFBALANCE |
| G_mid | 8 | ADDMOD, MULMOD, JUMP |
| G_high | 10 | JUMPI (conditional jump) |
| G_warmaccess | 100 | Accessing an already-touched (warm) account or storage slot |
| G_accesslistaddress | 2400 | Pre-warming an address via the transaction's access list |
| G_accessliststorage | 1900 | Pre-warming a storage slot via the access list |
| G_coldaccountaccess | 2600 | First-time (cold) access to an account in this transaction |
| G_coldsload | 2100 | First-time (cold) read from a storage slot |
| G_sset | 20000 | SSTORE: setting a slot from zero to non-zero |
| G_sreset | 2900 | SSTORE: changing a slot that already has a non-zero value |
| R_clear | 4800 | Refund for clearing a storage slot (setting non-zero → zero) |
| G_selfdestruct | 5000 | SELFDESTRUCT operation |
| G_create | 32000 | CREATE or CREATE2 contract deployment |
| G_codedeposit | 200 | Per byte of contract code stored on-chain |
| G_initcodeword | 2 | Per 32-byte word of initialisation code |
| G_callvalue | 9000 | Sending ETH with a CALL instruction |
| G_callstipend | 2300 | Free gas stipend given to callee when ETH is sent |
| G_newaccount | 25000 | Creating a brand new account via CALL or SELFDESTRUCT |
| G_exp | 10 | Base cost for EXP (exponentiation) |
| G_expbyte | 50 | Per byte in the exponent for EXP |
| G_memory | 3 | Per additional 32-byte word of active memory |
| G_txcreate | 32000 | Contract creation initiated by a transaction (not by opcode) |
| G_txdatazero | 4 | Per zero byte in transaction calldata |
| G_txdatanonzero | 16 | Per non-zero byte in transaction calldata |
| G_transaction | 21000 | Base cost for every transaction (this is why minimum tx cost is 21k gas) |
| G_log | 375 | Base cost for any LOG operation |
| G_logdata | 8 | Per byte of data in a LOG |
| G_logtopic | 375 | Per topic in a LOG |
| G_keccak256 | 30 | Base cost for KECCAK256 hash operation |
| G_keccak256word | 6 | Per 32-byte word of data hashed by KECCAK256 |
| G_copy | 3 | Per 32-byte word for *COPY operations (CALLDATACOPY, etc.) |
| G_blockhash | 20 | BLOCKHASH operation |
| G_quaddivisor | 3 | Divisor in EXPMOD gas calculation |
| secp256k1n | ≈1.158 × 10⁷⁷ | Order of the secp256k1 elliptic curve used for signatures |

---

## EVM Opcodes Reference

### 0s: Stop and Arithmetic

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x00 | STOP | 0 | 0 | Halts execution normally |
| 0x01 | ADD | 2 | 1 | a + b (mod 2²⁵⁶) |
| 0x02 | MUL | 2 | 1 | a × b (mod 2²⁵⁶) |
| 0x03 | SUB | 2 | 1 | a − b (mod 2²⁵⁶) |
| 0x04 | DIV | 2 | 1 | a ÷ b (integer, 0 if b=0) |
| 0x05 | SDIV | 2 | 1 | Signed division (two's complement) |
| 0x06 | MOD | 2 | 1 | a mod b (0 if b=0) |
| 0x07 | SMOD | 2 | 1 | Signed modulo |
| 0x08 | ADDMOD | 3 | 1 | (a + b) mod m — no intermediate overflow |
| 0x09 | MULMOD | 3 | 1 | (a × b) mod m — no intermediate overflow |
| 0x0a | EXP | 2 | 1 | a^b (mod 2²⁵⁶) |
| 0x0b | SIGNEXTEND | 2 | 1 | Extend sign bit of a smaller integer to 256 bits |

### 10s: Comparison & Bitwise Logic

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x10 | LT | 2 | 1 | Unsigned less-than |
| 0x11 | GT | 2 | 1 | Unsigned greater-than |
| 0x12 | SLT | 2 | 1 | Signed less-than |
| 0x13 | SGT | 2 | 1 | Signed greater-than |
| 0x14 | EQ | 2 | 1 | Equality check |
| 0x15 | ISZERO | 1 | 1 | Returns 1 if value is 0, else 0 |
| 0x16 | AND | 2 | 1 | Bitwise AND |
| 0x17 | OR | 2 | 1 | Bitwise OR |
| 0x18 | XOR | 2 | 1 | Bitwise XOR (exclusive or) |
| 0x19 | NOT | 1 | 1 | Bitwise NOT (flip all bits) |
| 0x1a | BYTE | 2 | 1 | Get byte N from a 256-bit word (N=0 is leftmost) |
| 0x1b | SHL | 2 | 1 | Left shift |
| 0x1c | SHR | 2 | 1 | Logical right shift (fill with zeros) |
| 0x1d | SAR | 2 | 1 | Arithmetic right shift (preserve sign) |

### 20s: Keccak256

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x20 | KECCAK256 | 2 | 1 | Keccak-256 hash of a memory region |

### 30s: Environmental Information

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x30 | ADDRESS | 0 | 1 | Address of currently executing contract |
| 0x31 | BALANCE | 1 | 1 | ETH balance of a given address |
| 0x32 | ORIGIN | 0 | 1 | Original transaction sender (always the EOA) |
| 0x33 | CALLER | 0 | 1 | Direct caller of this execution |
| 0x34 | CALLVALUE | 0 | 1 | Wei sent with this call |
| 0x35 | CALLDATALOAD | 1 | 1 | Load 32 bytes of calldata at given offset |
| 0x36 | CALLDATASIZE | 0 | 1 | Size of calldata in bytes |
| 0x37 | CALLDATACOPY | 3 | 0 | Copy calldata to memory |
| 0x38 | CODESIZE | 0 | 1 | Size of executing code in bytes |
| 0x39 | CODECOPY | 3 | 0 | Copy executing code to memory |
| 0x3a | GASPRICE | 0 | 1 | Effective gas price of the transaction |
| 0x3b | EXTCODESIZE | 1 | 1 | Code size of another account |
| 0x3c | EXTCODECOPY | 4 | 0 | Copy another account's code to memory |
| 0x3d | RETURNDATASIZE | 0 | 1 | Size of return data from last sub-call |
| 0x3e | RETURNDATACOPY | 3 | 0 | Copy return data to memory |
| 0x3f | EXTCODEHASH | 1 | 1 | Keccak-256 hash of another account's code |

### 40s: Block Information

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x40 | BLOCKHASH | 1 | 1 | Hash of a recent block (up to 256 blocks back) |
| 0x41 | COINBASE | 0 | 1 | Block's beneficiary (validator) address |
| 0x42 | TIMESTAMP | 0 | 1 | Block's Unix timestamp |
| 0x43 | NUMBER | 0 | 1 | Current block number |
| 0x44 | PREVRANDAO | 0 | 1 | Previous block's RANDAO mix (randomness source) |
| 0x45 | GASLIMIT | 0 | 1 | Current block's gas limit |
| 0x46 | CHAINID | 0 | 1 | Chain ID (1 = Ethereum mainnet) |
| 0x47 | SELFBALANCE | 0 | 1 | Balance of the executing contract itself |
| 0x48 | BASEFEE | 0 | 1 | Current block's base fee (EIP-1559) |

### 50s: Stack, Memory, Storage and Flow

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x50 | POP | 1 | 0 | Remove and discard top stack item |
| 0x51 | MLOAD | 1 | 1 | Load 32 bytes from memory |
| 0x52 | MSTORE | 2 | 0 | Store 32 bytes to memory |
| 0x53 | MSTORE8 | 2 | 0 | Store 1 byte to memory |
| 0x54 | SLOAD | 1 | 1 | Load word from persistent storage |
| 0x55 | SSTORE | 2 | 0 | Store word to persistent storage |
| 0x56 | JUMP | 1 | 0 | Unconditional jump (must target JUMPDEST) |
| 0x57 | JUMPI | 2 | 0 | Conditional jump (jumps if condition ≠ 0) |
| 0x58 | PC | 0 | 1 | Current program counter value |
| 0x59 | MSIZE | 0 | 1 | Active memory size in bytes (multiple of 32) |
| 0x5a | GAS | 0 | 1 | Remaining gas available |
| 0x5b | JUMPDEST | 0 | 0 | Valid jump destination marker (no runtime effect) |

### 5f, 60s–70s: Push Operations

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x5f | PUSH0 | 0 | 1 | Push the value 0 onto stack |
| 0x60 | PUSH1 | 0 | 1 | Push 1 byte of inline data from code |
| 0x61 | PUSH2 | 0 | 1 | Push 2 bytes of inline data |
| ... | ... | 0 | 1 | ... |
| 0x7f | PUSH32 | 0 | 1 | Push 32 bytes (full word) of inline data |

### 80s: Duplication Operations

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x80 | DUP1 | 1 | 2 | Duplicate 1st (top) stack item |
| 0x81 | DUP2 | 2 | 3 | Duplicate 2nd stack item |
| ... | ... | ... | ... | ... |
| 0x8f | DUP16 | 16 | 17 | Duplicate 16th stack item |

### 90s: Exchange (Swap) Operations

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0x90 | SWAP1 | 2 | 2 | Swap 1st and 2nd stack items |
| 0x91 | SWAP2 | 3 | 3 | Swap 1st and 3rd stack items |
| ... | ... | ... | ... | ... |
| 0x9f | SWAP16 | 17 | 17 | Swap 1st and 17th stack items |

### a0s: Logging Operations

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0xa0 | LOG0 | 2 | 0 | Emit log with 0 indexed topics |
| 0xa1 | LOG1 | 3 | 0 | Emit log with 1 topic |
| 0xa2 | LOG2 | 4 | 0 | Emit log with 2 topics |
| 0xa3 | LOG3 | 5 | 0 | Emit log with 3 topics |
| 0xa4 | LOG4 | 6 | 0 | Emit log with 4 topics |

### f0s: System Operations

| Opcode | Mnemonic | δ | α | Description |
|--------|----------|---|---|-------------|
| 0xf0 | CREATE | 3 | 1 | Deploy a new contract (address = hash of sender + nonce) |
| 0xf1 | CALL | 7 | 1 | Call another contract / send ETH |
| 0xf2 | CALLCODE | 7 | 1 | Call with another's code in own context (deprecated) |
| 0xf3 | RETURN | 2 | 0 | Halt execution, return output data |
| 0xf4 | DELEGATECALL | 6 | 1 | Call with another's code, preserving sender + value (proxy pattern) |
| 0xf5 | CREATE2 | 4 | 1 | Deploy contract with deterministic address (uses salt) |
| 0xfa | STATICCALL | 6 | 1 | Read-only call — no state modifications allowed |
| 0xfd | REVERT | 2 | 0 | Halt, undo all state changes, return data + remaining gas |
| 0xfe | INVALID | — | — | Designated invalid instruction (consumes all gas) |
| 0xff | SELFDESTRUCT | 1 | 0 | Schedule contract for deletion, send balance to recipient (deprecated) |
