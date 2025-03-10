# FunC standard library
This section discuss the stdlib.fc library.

Currently the library is just a wrapper for most common assembler TVM commands, which aren't built-ins. Description of every TVM command used in the library can be found in [TVM documentation](https://ton-blockchain.github.io/docs/tvm.pdf) (Appendix A). Some of the descriptions were borrowed into this document.

Some of the library functions are commented out in the file. It means that they have already became built-ins for optimization purposes. However, the type signature and semantics remain the same.

Note that some less common commands are not presented in the stdlib. Someday they will also be added.

## Table of contents:
* [Tuple manipulation primitives](/func/stdlib?id=tuple-manipulation-primitives)
  * [Lisp-style lists primitives](/func/stdlib?id=lisp-style-lists)
    * [cons](/func/stdlib?id=cons)
    * [uncons](/func/stdlib?id=uncons)
    * [list_next](/func/stdlib?id=list_next)
    * [car](/func/stdlib?id=car)
    * [cdr](/func/stdlib?id=cdr)
  * [Other tuple primitives](/func/stdlib?id=other-tuple-primitives)
    * [empty_tuple](/func/stdlib?id=empty_tuple)
    * [tpush](/func/stdlib?id=tpush)
    * [single](/func/stdlib?id=single)
    * [unsingle](/func/stdlib?id=unsingle)
    * [pair](/func/stdlib?id=pair)
    * [unpair](/func/stdlib?id=unpair)
    * [triple](/func/stdlib?id=triple)  
    * [untriple](/func/stdlib?id=untriple)  
    * [tuple4](/func/stdlib?id=tuple4)  
    * [untuple4](/func/stdlib?id=untuple4)  
    * [first](/func/stdlib?id=first)  
    * [second](/func/stdlib?id=second)  
    * [third](/func/stdlib?id=third)  
    * [fourth](/func/stdlib?id=fourth)  
    * [pair_first](/func/stdlib?id=pair_first)  
    * [pair_second](/func/stdlib?id=pair_second)
    * [triple_first](/func/stdlib?id=triple_first)
    * [triple_second](/func/stdlib?id=triple_second)
    * [triple_third](/func/stdlib?id=triple_third)
* [Domain specific primitives](/func/stdlib?id=domain-specific-primitives)
  * [Extracting info from c7](/func/stdlib?id=extracting-info-from-c7)
    * [now](/func/stdlib?id=now)
    * [my_address](/func/stdlib?id=my_address)
    * [get_balance](/func/stdlib?id=get_balance)
    * [cur_lt](/func/stdlib?id=cur_lt)
    * [block_lt](/func/stdlib?id=block_lt)
    * [config_param](/func/stdlib?id=config_param)
  * [Hashes](/func/stdlib?id=Hashes)
    * [cell_hash](/func/stdlib?id=cell_hash)
    * [slice_hash](/func/stdlib?id=slice_hash)
    * [string_hash](/func/stdlib?id=string_hash)
  * [Signature checks](/func/stdlib?id=signature-checks)
    * [check_signature](/func/stdlib?id=check_signature)
    * [check_data_signature](/func/stdlib?id=check_data_signature)
  * [Computation of boc size](/func/stdlib?id=computation-of-boc-size)
    * [compute_data_size?](/func/stdlib?id=compute_data_size)
    * [slice_compute_data_size?](/func/stdlib?id=slice_compute_data_size)
    * [compute_data_size](/func/stdlib?id=compute_data_size-1)
    * [slice_compute_data_size](/func/stdlib?id=slice_compute_data_size-1)
  * [Persistent storage save and load](/func/stdlib?id=persistent-storage-save-and-load)
    * [get_data](/func/stdlib?id=get_data)
    * [set_data](/func/stdlib?id=set_data)
  * [Continuation primitives](/func/stdlib?id=continuation-primitives)
    * [get_c3](/func/stdlib?id=get_c3)
    * [set_c3](/func/stdlib?id=set_c3)
    * [bless](/func/stdlib?id=bless)
  * [Gas related primitives](/func/stdlib?id=gas-related-primitives)
    * [accept_message](/func/stdlib?id=accept_message)
    * [set_gas_limit](/func/stdlib?id=set_gas_limit)
    * [commit](/func/stdlib?id=commit)
    * [buy_gas](/func/stdlib?id=buy_gas)
  * [Actions primitives](//func/stdlib?id=actions-primitives)
    * [raw_reserve](/func/stdlib?id=raw_reserve)
    * [raw_reserve_extra](/func/stdlib?id=raw_reserve_extra)
    * [send_raw_message](/func/stdlib?id=send_raw_message)
    * [set_code](/func/stdlib?id=set_code)
  * [Random number generator primitives](/func/stdlib?id=random-number-generator-primitives)
    * [random](/func/stdlib?id=random)
    * [rand](/func/stdlib?id=rand)
    * [get_seed](/func/stdlib?id=get_seed)
    * [set_seed](/func/stdlib?id=set_seed)
    * [randomize](/func/stdlib?id=randomize)
    * [randomize_lt](/func/stdlib?id=randomize_lt)
  * [Address manipulation primitives](/func/stdlib?id=address-manipulation-primitives)
    * [load_msg_addr](/func/stdlib?id=load_msg_addr)
    * [parse_addr](/func/stdlib?id=parse_addr)
    * [parse_std_addr](/func/stdlib?id=parse_std_addr)
    * [parse_var_addr](/func/stdlib?id=parse_var_addr)
* [Debug primitives](/func/stdlib?id=debug-primitives)
  * [dump_stack](/func/stdlib?id=dump_stack)
* [Slice primitives](/func/stdlib?id=slice-primitives)
  * [begin_parse](/func/stdlib?id=begin_parse)
  * [end_parse](/func/stdlib?id=end_parse)
  * [load_ref](/func/stdlib?id=load_ref)
  * [preload_ref](/func/stdlib?id=preload_ref)
  * [load_int](/func/stdlib?id=load_int)
  * [load_uint](/func/stdlib?id=load_uint)
  * [preload_int](/func/stdlib?id=preload_int)
  * [preload_uint](/func/stdlib?id=preload_uint)
  * [load_bits](/func/stdlib?id=load_bits)
  * [preload_bits](/func/stdlib?id=preload_bits)
  * [load_grams](/func/stdlib?id=load_grams)
  * [skip_bits](/func/stdlib?id=skip_bits)
  * [first_bits](/func/stdlib?id=first_bits)
  * [skip_last_bits](/func/stdlib?id=skip_last_bits)
  * [slice_last](/func/stdlib?id=slice_last)
  * [load_dict](/func/stdlib?id=load_dict)
  * [preload_dict](/func/stdlib?id=preload_dict)
  * [skip_dict](/func/stdlib?id=skip_dict)
  * [Slice size primitives](/func/stdlib?id=slice-size-primitives)
    * [slice_refs](/func/stdlib?id=slice_refs)
    * [slice_bits](/func/stdlib?id=slice_bits)
    * [slice_bits_refs](/func/stdlib?id=slice_bits_refs)
    * [slice_empty?](/func/stdlib?id=slice_empty)
    * [slice_data_empty?](/func/stdlib?id=slice_data_empty)
    * [slice_depth](/func/stdlib?id=slice_depth)
* [Builder primitives](/func/stdlib?id=builder-primitives)
  * [begin_cell](/func/stdlib?id=begin_cell)
  * [end_cell](/func/stdlib?id=end_cell)
  * [store_ref](/func/stdlib?id=store_ref)
  * [store_uint](/func/stdlib?id=store_uint)
  * [store_int](/func/stdlib?id=store_int)
  * [store_slice](/func/stdlib?id=store_slice)
  * [store_grams](/func/stdlib?id=store_grams)
  * [store_dict](/func/stdlib?id=store_dict)
  * [store_maybe_ref](/func/stdlib?id=store_maybe_ref)
  * [Builder size primitives](/func/stdlib?id=builder-size-primitives)
    * [builder_refs](/func/stdlib?id=builder_refs)
    * [builder_bits](/func/stdlib?id=builder_bits)
    * [builder_depth](/func/stdlib?id=builder_depth)
* [Cell primitives](/func/stdlib?id=cell-primitives)
  * [cell_depth](/func/stdlib?id=cell_depth)
  * [cell_null?](/func/stdlib?id=cell_null)
* [Dictionaries primitives](/func/stdlib?id=dictionaries-primitives)
  * [Taxonomy note](/func/stdlib?id=taxonomy-note)
  * [Dictionary's values](/func/stdlib?id=dictionary39s-values)
  * [dict_set](/func/stdlib?id=dict_set)
  * [dict_set_ref](/func/stdlib?id=dict_set_ref)
  * [dict_get?](/func/stdlib?id=dict_get)
  * [dict_get_ref?](/func/stdlib?id=dict_get_ref)
  * [dict_get_ref](/func/stdlib?id=dict_get_ref-1)
  * [dict_set_get_ref](/func/stdlib?id=dict_set_get_ref)
  * [dict_delete?](/func/stdlib?id=dict_delete)
  * [dict_delete_get?](/func/stdlib?id=dict_delete_get)
  * [dict_add?](/func/stdlib?id=dict_add)
  * [dict_replace?](/func/stdlib?id=dict_replace)
  * [Builder counterparts](/func/stdlib?id=builder-counterparts)
    * [dict_set_builder](/func/stdlib?id=dict_set_builder)
    * [dict_add_builder?](/func/stdlib?id=dict_add_builder)
    * [dict_replace_builder?](/func/stdlib?id=dict_replace_builder)
  * [dict_delete_get_min](/func/stdlib?id=dict_delete_get_min)
  * [dict_delete_get_max](/func/stdlib?id=dict_delete_get_max)
  * [dict_get_min?](/func/stdlib?id=dict_get_min)
  * [dict_get_max?](/func/stdlib?id=dict_get_max)
  * [dict_get_min_ref?](/func/stdlib?id=dict_get_min_ref)
  * [dict_get_max_ref?](/func/stdlib?id=dict_get_max_ref)
  * [dict_get_next?](/func/stdlib?id=dict_get_next)
  * [dict_get_nexteq?](/func/stdlib?id=dict_get_nexteq)
  * [dict_get_prev?](/func/stdlib?id=dict_get_prev)
  * [dict_get_preveq?](/func/stdlib?id=dict_get_preveq)
  * [new_dict](/func/stdlib?id=new_dict)
  * [dict_empty?](/func/stdlib?id=dict_empty)
* [Prefix dictionaries primitives](/func/stdlib?id=prefix-dictionaries-primitives)
  * [pfxdict_get?](/func/stdlib?id=pfxdict_get)
  * [pfxdict_set?](/func/stdlib?id=pfxdict_set)
  * [pfxdict_delete?](/func/stdlib?id=pfxdict_delete)
* [Special primitives](/func/stdlib?id=special-primitives)
  * [null](/func/stdlib?id=null)
  * [~impure_touch](/func/stdlib?id=impure_touch)
* [Other primitives](/func/stdlib?id=other-primitives)
  * [min](/func/stdlib?id=min)
  * [max](/func/stdlib?id=max)
  * [minmax](/func/stdlib?id=minmax)
  * [abs](/func/stdlib?id=abs)

## Tuple manipulation primitives
The names and the types are mostly self-explaining. See [polymorhism with forall](/func/functions?id=polymorphism-with-forall) for more info on the polymorphic functions.

Note that currently values of atomic type `tuple` can't be cast to composite tuple type (e.g. `[int, cell]`) and vise versa.

### Lisp-style lists
Lists can be represented as nested 2-elements tuples. Empty list is conventionally represented as TVM `null` value (it can be obtained by calling `null()`). For example, tuple `(1, (2, (3, null)))` represents list `[1, 2, 3]`. Elements of a list can be of different types.
#### cons
```
forall X -> tuple cons(X head, tuple tail) asm "CONS";
```
Adds an element to the beginning of lisp-style list.
#### uncons
```
forall X -> (X, tuple) uncons(tuple list) asm "UNCONS";
```
Extracts the head and the tail of lisp-style list.
#### list_next
```
forall X -> (tuple, X) list_next(tuple list) asm( -> 1 0) "UNCONS";
```
Extracts the tail and the head of lisp-style list. Can be used as [(non-)modifying method](/func/statements?id=methods-calls).
```
() foo(tuple xs) {
    int x = xs.list_next(); ;; get the first element
    int y = xs~list_next(); ;; pop the first element
    int z = xs~list_next(); ;; pop the second element
}
```
#### car
```
forall X -> X car(tuple list) asm "CAR";
```
Returns the head of lisp-style list.
#### cdr
```
tuple cdr(tuple list) asm "CDR";
```
Returns the tail of lisp-style list.
### Other tuple primitives
#### empty_tuple
```
tuple empty_tuple() asm "NIL";
```
Creates 0-element tuple.
#### tpush
```
forall X -> tuple tpush(tuple t, X value) asm "TPUSH";
forall X -> (tuple, ()) ~tpush(tuple t, X value) asm "TPUSH";
```
Appends a value `x` to a `Tuple t = (x1, ..., xn)`, but only if the resulting `Tuple t' = (x1, ..., xn, x)` is of length at most 255. Otherwise throws a type check exception.
#### single
```
forall X -> [X] single(X x) asm "SINGLE";
```
Creates a singleton, i.e. a tuple of length one.
#### unsingle
```
forall X -> X unsingle([X] t) asm "UNSINGLE";
```
Unpacks a singleton.
#### pair
```
forall X, Y -> [X, Y] pair(X x, Y y) asm "PAIR";
```
Creates a pair.
#### unpair
```
forall X, Y -> (X, Y) unpair([X, Y] t) asm "UNPAIR";
```
Unpacks a pair.
#### triple
```
forall X, Y, Z -> [X, Y, Z] triple(X x, Y y, Z z) asm "TRIPLE";
```
Creates a triple.

#### untriple
```
forall X, Y, Z -> (X, Y, Z) untriple([X, Y, Z] t) asm "UNTRIPLE";
```
Unpacks a triple.

#### tuple4
```
forall X, Y, Z, W -> [X, Y, Z, W] tuple4(X x, Y y, Z z, W w) asm "4 TUPLE";
```
Creates 4-element tuple.

#### untuple4
```
forall X, Y, Z, W -> (X, Y, Z, W) untuple4([X, Y, Z, W] t) asm "4 UNTUPLE";
```
Unpack 4-element tuple.

#### first
```
forall X -> X first(tuple t) asm "FIRST";
```
Returns the first element of a tuple.

#### second
```
forall X -> X second(tuple t) asm "SECOND";
```
Returns the second element of a tuple.

#### third
```
forall X -> X third(tuple t) asm "THIRD";
```
Returns the third element of a tuple.

#### fourth
```
forall X -> X fourth(tuple t) asm "3 INDEX";
```
Returns the fourth element of a tuple.

#### pair_first
```
forall X, Y -> X pair_first([X, Y] p) asm "FIRST";
```
Returns the first element of a pair.

#### pair_second
```
forall X, Y -> Y pair_second([X, Y] p) asm "SECOND";
```
Returns the second element of a pair.

#### triple_first
```
forall X, Y, Z -> X triple_first([X, Y, Z] p) asm "FIRST";
```
Returns the first element of a triple.

#### triple_second
```
forall X, Y, Z -> Y triple_second([X, Y, Z] p) asm "SECOND";
```
Returns the second element of a triple.

#### triple_third
```
forall X, Y, Z -> Z triple_third([X, Y, Z] p) asm "THIRD";
```
Returns the third element of a triple.

## Domain specific primitives
### Extracting info from c7
Some useful information regarding smartcontract invocation can be found in c7 special register. Those primitives serve for convenient data extraction.
#### now
```
int now() asm "NOW";
```
Returns the current Unix time as an Integer
#### my_address
```
slice my_address() asm "MYADDR";
```
Returns the internal address of the current smart contract as a Slice with a `MsgAddressInt`. If necessary, it can be parsed further using primitives such as `parse_std_addr`.
#### get_balance
```
[int, cell] get_balance() asm "BALANCE";
```
Returns the remaining balance of the smart contract as a `tuple` consisting of an `int` (the remaining balance in nanotoncoins) and a `cell` (a dictionary with 32-bit keys representing the balance of “extra currencies”). Note that RAW primitives such as `send_raw_message` do not update this field.
#### cur_lt
```
int cur_lt() asm "LTIME";
```
Returns the logical time of the current transaction.
#### block_lt
```
int block_lt() asm "BLOCKLT";
```
Returns the starting logical time of the current
block.
#### config_param
```
cell config_param(int x) asm "CONFIGOPTPARAM";
```
Returns the value of the global configuration parameter with integer index `i` as a `cell` or `null` value.
### Hashes
#### cell_hash
```
int cell_hash(cell c) asm "HASHCU";
```
Computes the representation hash of a `cell c` and returns it as a 256-bit unsigned integer `x`. Useful for signing and checking signatures of arbitrary entities represented by a tree of cells.
#### slice_hash
```
int slice_hash(slice s) asm "HASHSU";
```
Computes the hash of a `slice s` and returns it as a 256-bit unsigned integer `x`. The result is the same as if an ordinary cell containing only data and references from `s` had been created and its hash computed by `cell_hash`.
#### string_hash
```
int string_hash(slice s) asm "SHA256U";
```
Computes sha256 of the data bits of `slice s`. If the bit length of `s` is not divisible by eight, throws a cell underflow exception. The hash value is returned as a 256-bit unsigned integer `x`.

### Signature checks
#### check_signature
```
int check_signature(int hash, slice signature, int public_key) asm "CHKSIGNU";
```
Checks the Ed25519-`signature` of a `hash` (a 256-bit unsigned integer, usually computed as the hash of some data) using `public_key` (also represented by a 256-bit unsigned integer). The signature must contain at least 512 data bits; only the first 512 bits are used. The result is −1 if the signature
is valid, 0 otherwise. Note that `CHKSIGNU` creates a 256-bit slice with the hash and calls `CHKSIGNS`. That is, if `hash` is computed as the hash of some data, these data are hashed _twice_, the second hashing occurring inside `CHKSIGNS`.
#### check_data_signature
```
int check_data_signature(slice data, slice signature, int public_key) asm "CHKSIGNS";
```
Checks whether `signature` is a valid Ed25519-signature of the data portion of `slice data` using `public_key`, similarly to `check_signature`. If the bit length of `data` is not divisible by eight, throws a cell underflow exception. The verification of Ed25519 signatures is the standard one, with sha256 used to reduce `data` to the 256-bit number that is actually signed.

### Computation of boc size
The primitives below may be useful for computing storage fees of user-provided data.
#### compute_data_size?
```
(int, int, int, int) compute_data_size?(cell c, int max_cells) asm "CDATASIZEQ NULLSWAPIFNOT2 NULLSWAPIFNOT";
```
Returns `(x, y, z, -1)` or `(null, null, null, 0)`. Recursively computes the count of distinct cells `x`, data bits `y`, and cell references `z` in the DAG rooted at `cell c`, effectively returning the total storage used by this DAG taking into account the identification of equal cells. The values of `x`, `y`, and `z` are computed by a depth-first traversal of this DAG, with a hash table of visited cell hashes used to prevent visits of already-visited cells. The total count of visited cells `x` cannot exceed non-negative `max_cells`; otherwise the computation is aborted before visiting the `(max_cells + 1)`-st cell and a zero flag is returned to indicate failure. If `c` is `null`, returns `x = y = z = 0`.
#### slice_compute_data_size?
```
(int, int, int, int) slice_compute_data_size?(slice s, int max_cells) asm "SDATASIZEQ NULLSWAPIFNOT2 NULLSWAPIFNOT";
```
Similar to `compute_data_size?`, but accepting a `slice s` instead of a `cell`. The returned value of `x` does not take into account the cell that contains the slice `s` itself; however, the data bits and the cell references of `s` are accounted for in `y` and `z`.
#### compute_data_size
```
(int, int, int) compute_data_size(cell c, int max_cells) impure asm "CDATASIZE";
```
A non-quiet version of `compute_data_size?` that throws a cell overflow exception (8) on failure.
#### slice_compute_data_size
```
(int, int, int) slice_compute_data_size(slice s, int max_cells) impure asm "SDATASIZE";
```
A non-quiet version of `slice_compute_data_size?` that throws a cell overflow exception (8) on failure.
### Persistent storage save and load
#### get_data
```
cell get_data() asm "c4 PUSH";
```
Returns the persistent contract storage cell. It can be parsed or modified with slice and builder primitives later.
#### set_data
```
() set_data(cell c) impure asm "c4 POP";
```
Sets cell `c` as persistent contract data. You can update persistent contract storage with this primitive.
### Continuation primitives
#### get_c3
```
cont get_c3() impure asm "c3 PUSH";
```
Usually `c3` has a continuation initialized by the whole code of the contract. It is used for function calls. The primitive returns the current value of `c3`.
#### set_c3
```
() set_c3(cont c) impure asm "c3 POP";
```
Updates the current value of `c3`. Usually, it is used for updating smart contract code in run-time. Note that after execution of this primitive the current code (and the stack of recursive function calls) won't change, but any other function call will use a function from the new code.
#### bless
```
cont bless(slice s) impure asm "BLESS";
```
Transforms a `slice s` into a simple ordinary continuation `c`, with `c.code = s` and an empty stack and savelist.

### Gas related primitives
#### accept_message
```
() accept_message() impure asm "ACCEPT";
```
Sets current gas limit `gl` to its maximal allowed value `gm`, and resets the gas credit `gc` to zero, decreasing the value of `gr` by `gc` in the process. In other words, the current smart contract agrees to buy some gas to finish the current transaction. This action is required to process external messages, which bring no value (hence no gas) with themselves.

For more details check [accept_message effects](/smart-contracts/accept)
#### set_gas_limit
```
() set_gas_limit(int limit) impure asm "SETGASLIMIT";
```
Sets current gas limit `gl` to the minimum of `limit` and `gm`, and resets the gas credit `gc` to zero. If the gas consumed so far (including the present instruction) exceeds the resulting value of `gl`, an (unhandled) out of gas exception is thrown before setting new gas limits. Notice that `set_gas_limit` with an argument `limit ≥ 2^63 − 1` is equivalent to `accept_message`.

For more details check [accept_message effects](/smart-contracts/accept)
#### commit
```
() commit() impure asm "COMMIT";
```
Commits the current state of registers `c4` (“persistent data”) and `c5` (“actions”) so that the current execution is considered “successful” with the saved values even if an exception is thrown later.
#### buy_gas
```
() buy_gas(int gram) impure asm "BUYGAS";
```
Computes the amount of gas that can be bought for `gram` nanotoncoins, and sets `gl` accordingly in the same way as `set_gas_limit`.

### Actions primitives
#### raw_reserve
```
() raw_reserve(int amount, int mode) impure asm "RAWRESERVE";
```
Creates an output action which would reserve exactly `amount` nanotoncoins (if `mode = 0`), at most `amount` nanotoncoins (if `mode = 2`), or all but `amount` nanotoncoins (if `mode = 1` or `mode = 3`), from the remaining balance of the account. It is roughly equivalent to creating an outbound message carrying `amount` nanotoncoins (or `b − amount` nanotoncoins, where `b` is the remaining balance) to oneself, so that the subsequent output actions would not be able to spend more money than the remainder. Bit +2 in `mode` means that the external action does not fail if the specified amount cannot be reserved; instead, all remaining balance is reserved. Bit +8 in `mode` means `amount <- -amount` before performing any further actions. Bit +4 in `mode` means that `amount` is increased by the original balance of the current account (before the compute phase), including all extra currencies, before performing any other checks and actions. Currently, `amount` must be a non-negative integer, and `mode` must be in the range `0..15`.
#### raw_reserve_extra
```
() raw_reserve_extra(int amount, cell extra_amount, int mode) impure asm "RAWRESERVEX";
```
Similar to `raw_reserve`, but also accepts a dictionary `extra_amount` (represented by a `cell` or `null`) with extra currencies. In this way currencies other than TonCoin can be reserved.
#### send_raw_message
```
() send_raw_message(cell msg, int mode) impure asm "SENDRAWMSG";
```
Sends a raw message contained in `msg`, which should contain a correctly serialized object Message X, with the only exception that the source address is allowed to have dummy value `addr_none` (to be automatically replaced with the current smart contract address), and `ihr_fee`, `fwd_fee`, `created_lt` and `created_at` fields can have arbitrary values (to be rewritten with correct values during the action phase of the current transaction). Integer parameter `mode` contains the flags. Currently `mode = 0` is used for ordinary messages;
`mode = 128` is used for messages that are to carry all the remaining balance of the current smart contract (instead of the value originally indicated in the message); `mode = 64` is used for messages that carry all the remaining value of the inbound message in addition to the value initially indicated in the new message (if bit 0 is not set, the gas fees are deducted from this amount); `mode' = mode + 1` means that the sender wants to pay transfer fees separately; `mode' = mode + 2` means that any errors arising while processing this message during the action phase should be ignored. Finally, `mode' = mode + 32` means that the current account must be destroyed if its resulting balance is zero. This flag is usually employed together with +128.

#### set_code
```
() set_code(cell new_code) impure asm "SETCODE";
```
Creates an output action that would change this smart contract code to that given by cell `new_code`. Notice that this change will take effect only after the successful termination of the current run of the smart contract (cf. [set_c3](/func/stdlib?id=set_c3)).

### Random number generator primitives
The pseudo-random number generator uses the random seed, an unsigned 256-bit Integer, and (sometimes) other data kept in c7. The initial value of the random seed before a smart contract is executed in TON Blockchain is a hash of the smart contract address and the global block random seed. If there are several runs of the same smart contract inside a block, then all of these runs will have the same random seed. This can be fixed, for example, by running `randomize_lt` before using the pseudo-random number generator for the first time.
#### random
```
int random() impure asm "RANDU256";
```
Generates a new pseudo-random unsigned 256-bit integer `x`. The algorithm is as follows: if `r` is the old value of the random seed, considered as a 32-byte array (by constructing the big-endian representation of an unsigned 256-bit integer), then its `sha512(r)` is computed; the first 32 bytes of this hash are stored as the new value `r'` of the random seed, and the remaining 32 bytes are returned as the next random value `x`.
#### rand
```
int rand(int range) impure asm "RAND";
```
Generates a new pseudo-random integer `z` in the range `0..range−1` (or `range..−1`, if `range < 0`). More precisely, an unsigned random value `x` is generated as in `random`; then `z := x * range / 2^256` is
computed.

#### get_seed
```
int get_seed() impure asm "RANDSEED";
```
Returns the current random seed as an unsigned 256-bit Integer.
#### set_seed
```
int set_seed(int seed) impure asm "SETRAND";
```
Sets the random seed to unsigned 256-bit `seed`.

#### randomize
```
() randomize(int x) impure asm "ADDRAND";
```
Mixes unsigned 256-bit integer `x` into the random seed `r` by setting the random seed to sha256 of the concatenation of two 32-byte strings: the first with the big-endian representation of the old seed `r`, and the second with the big-endian representation of `x`.

#### randomize_lt
```
() randomize_lt() impure asm "LTIME" "ADDRAND";
```
Equivalent to `randomize(cur_lt());`.

### Address manipulation primitives
The address manipulation primitives listed below serialize and deserialize values according to the following TL-B scheme:
```
addr_none$00 = MsgAddressExt;
addr_extern$01 len:(## 8) external_address:(bits len)
             = MsgAddressExt;
anycast_info$_ depth:(#<= 30) { depth >= 1 }
  rewrite_pfx:(bits depth) = Anycast;
addr_std$10 anycast:(Maybe Anycast)
  workchain_id:int8 address:bits256 = MsgAddressInt;
addr_var$11 anycast:(Maybe Anycast) addr_len:(## 9)
  workchain_id:int32 address:(bits addr_len) = MsgAddressInt;
_ _:MsgAddressInt = MsgAddress;
_ _:MsgAddressExt = MsgAddress;

int_msg_info$0 ihr_disabled:Bool bounce:Bool bounced:Bool
  src:MsgAddress dest:MsgAddressInt
  value:CurrencyCollection ihr_fee:Grams fwd_fee:Grams
  created_lt:uint64 created_at:uint32 = CommonMsgInfoRelaxed;
ext_out_msg_info$11 src:MsgAddress dest:MsgAddressExt
  created_lt:uint64 created_at:uint32 = CommonMsgInfoRelaxed;
```
A deserialized `MsgAddress` is represented by a tuple `t` as follows:
* `addr_none` is represented by `t = (0)`, i.e., a tuple containing exactly
one integer equal to zero.
* `addr_extern` is represented by `t = (1, s)`, where slice `s` contains the
field `external_address`. In other words, `t` is a pair (a tuple consisting of two entries), containing an integer equal to one and slice `s`.
* `addr_std` is represented by `t = (2, u, x, s)`, where `u` is either a `null` (if `anycast` is absent) or a slice `s'` containing `rewrite_pfx` (if `anycast` is present). Next, integer `x` is the `workchain_id`, and slice `s` contains the address.
* `addr_var` is represented by `t = (3, u, x, s)`, where `u`, `x`, and `s` have the same meaning as for `addr_std`.

#### load_msg_addr
```
(slice, slice) load_msg_addr(slice s) asm( -> 1 0) "LDMSGADDR";
```
Loads from `slice s` the only prefix that is a valid `MsgAddress`, and returns both this prefix `s'` and the remainder `s''` of `s` as slices.
#### parse_addr
```
tuple parse_addr(slice s) asm "PARSEMSGADDR";
```
Decomposes `slice s` containing a valid `MsgAddress` into a `tuple t` with separate fields of this `MsgAddress`. If `s` is not a valid `MsgAddress`, a cell deserialization exception is thrown.

#### parse_std_addr
```
(int, int) parse_std_addr(slice s) asm "REWRITESTDADDR";
```
Parses slice `s` containing a valid `MsgAddressInt` (usually a `msg_addr_std`), applies rewriting from the `anycast` (if present) to the same-length prefix of the address, and returns both the workchain and the 256-bit address as integers. If the address is not 256-bit, or if `s` is not a valid serialization of `MsgAddressInt`, throws a cell `deserialization` exception.
#### parse_var_addr
```
(int, slice) parse_var_addr(slice s) asm "REWRITEVARADDR";
```
A variant of `parse_std_addr` that returns the (rewritten) address as a slice `s`, even if it is not exactly 256 bit long (represented by a `msg_addr_var`).

## Debug primitives
Currently only one function is available.
#### dump_stack
```
() dump_stack() impure asm "DUMPSTK";
```
Dumps the stack (at most the top 255 values) and shows the total stack depth.

## Slice primitives
It is said that a primitive *loads* some data, if it returns the data and the remainder of the slice (so it can also be used as [modifying method](/func/statements?id=modifying-methods)).

It is said that a primitive *preloads* some data, if it returns only the data (it can be used as [non-modifying method](/func/statements?id=non-modifying-methods)).

Unless otherwise stated, loading and preloading primitives read the data from a prefix of the slice.
#### begin_parse
```
slice begin_parse(cell c) asm "CTOS";
```

Converts a `cell` into a `slice`. Notice that `c` must be either an ordinary cell, or an exotic cell (see [TVM.pdf](https://ton-blockchain.github.io/docs/tvm.pdf), 3.1.2) which is automatically loaded to yield an ordinary cell `c'`, converted into a `slice` afterwards.

#### end_parse
```
() end_parse(slice s) impure asm "ENDS";
```
Checks if `s` is empty. If not, throws an exception.
#### load_ref
```
(slice, cell) load_ref(slice s) asm( -> 1 0) "LDREF";
```
Loads the first reference from the slice.
#### preload_ref
```
cell preload_ref(slice s) asm "PLDREF";
```
Preloads the first reference from the slice.
#### load_int
```
;; (slice, int) ~load_int(slice s, int len) asm(s len -> 1 0) "LDIX";
```
Loads a signed `len`-bit integer from a slice.
#### load_uint
```
;; (slice, int) ~load_uint(slice s, int len) asm( -> 1 0) "LDUX";
```
Loads an unsigned `len`-bit integer from a slice.
#### preload_int
```
;; int preload_int(slice s, int len) asm "PLDIX";
```
Preloads a signed `len`-bit integer from a slice.
#### preload_uint
```
;; int preload_uint(slice s, int len) asm "PLDUX";
```
Preloads an unsigned `len`-bit integer from a slice.
#### load_bits
```
;; (slice, slice) load_bits(slice s, int len) asm(s len -> 1 0) "LDSLICEX";
```
Loads the first `0 ≤ len ≤ 1023` bits from slice `s` into a separate slice `s''`.

#### preload_bits
```
;; slice preload_bits(slice s, int len) asm "PLDSLICEX";
```
Preloads the first `0 ≤ len ≤ 1023` bits from slice `s` into a separate slice `s''`.

#### load_grams
```
(slice, int) load_grams(slice s) asm( -> 1 0) "LDGRAMS";
```
Loads serialized amount of TonCoins (any unsigned integer up to `2^128 - 1`).

#### skip_bits
```
slice skip_bits(slice s, int len) asm "SDSKIPFIRST";
(slice, ()) ~skip_bits(slice s, int len) asm "SDSKIPFIRST";
```
Returns all but the first `0 ≤ len ≤ 1023` bits of `s`.
#### first_bits
```
slice first_bits(slice s, int len) asm "SDCUTFIRST";
```
Returns the first `0 ≤ len ≤ 1023` bits of `s`.
#### skip_last_bits
```
slice skip_last_bits(slice s, int len) asm "SDSKIPLAST";
(slice, ()) ~skip_last_bits(slice s, int len) asm "SDSKIPLAST";
```
Returns all but the last `0 ≤ len ≤ 1023` bits of `s`.
#### slice_last
```
slice slice_last(slice s, int len) asm "SDCUTLAST";
```
Returns the last `0 ≤ len ≤ 1023` bits of `s`.
#### load_dict
```
(slice, cell) load_dict(slice s) asm( -> 1 0) "LDDICT";
```
Loads a dictionary `D` from slice `s`. May be applied to dictionaries or to values of arbitrary `Maybe ^Y` types (returns `null` if `nothing` constructor is used).
#### preload_dict
```
cell preload_dict(slice s) asm "PLDDICT";
```
Preloads a dictionary `D` from slice `s`.
#### skip_dict
```
slice skip_dict(slice s) asm "SKIPDICT";
```
Loads a dictionary as `load_dict`, but returns only the remainder of the slice.
### Slice size primitives
#### slice_refs
```
int slice_refs(slice s) asm "SREFS";
```
Returns the number of references in slice `s`.
#### slice_bits
```
int slice_bits(slice s) asm "SBITS";
```
Returns the number of data bits in slice `s`.
#### slice_bits_refs
```
(int, int) slice_bits_refs(slice s) asm "SBITREFS";
```
Returns both the number of data bits and the number of references in `s`.
#### slice_empty?
```
int slice_empty?(slice s) asm "SEMPTY";
```
Checks whether a slice `s` is empty (i.e., contains no bits of data and no cell references).
#### slice_data_empty?
```
int slice_data_empty?(slice s) asm "SDEMPTY";
```
Checks whether slice `s` has no bits of data.
#### slice_refs_empty?
```
int slice_refs_empty?(slice s) asm "SREMPTY";
```
Checks whether slice `s` has no references.
#### slice_depth
```
int slice_depth(slice s) asm "SDEPTH";
```
Returns the depth of slice `s`. If `s` has no references, then returns `0`; otherwise the returned value is one plus the maximum of depths of cells referred to from `s`.

## Builder primitives
It is said that a primitive *stores* a value `x` into a builder `b` if it returns a modified version of the builder `b'` with the value `x` stored at the end of it. It can be used as [non-modifying method](/func/statements?id=non-modifying-methods).

All the primitives below first check whether there is enough space in the `builder`, and only then check the range of the value being serialized.
#### begin_cell
```
builder begin_cell() asm "NEWC";
```
Creates a new empty `builder`.
#### end_cell
```
cell end_cell(builder b) asm "ENDC";
```
Converts a `builder` into an ordinary `cell`.
#### store_ref
```
builder store_ref(builder b, cell c) asm(c b) "STREF";
```
Stores a reference to cell `c` into builder `b`.
#### store_uint
```
;; builder store_uint(builder b, int x, int len) asm(x b len) "STUX";
```
Stores an unsigned `len`-bit integer `x` into `b` for `0 ≤ len ≤ 256`.
#### store_int
```
;; builder store_int(builder b, int x, int len) asm(x b len) "STIX";
```
Stores a signed `len`-bit integer `x` into `b` for `0 ≤ len ≤ 257`.
#### store_slice
```
builder store_slice(builder b, slice s) asm "STSLICER";
```
Stores slice `s` into builder `b`.
#### store_grams
```
builder store_grams(builder b, int x) asm "STGRAMS";
```
Stores (serializes) an integer `x` in the range `0..2^128 − 1` into builder `b`. The serialization of `x` consists of a 4-bit unsigned big-endian integer `l`, which is the smallest integer `l ≥ 0`, such that `x < 2^8l`, followed by an `8l`-bit unsigned big-endian representation of `x`. If `x` does not belong to the supported range, a range check exception is thrown.

It is the usual way to store amounts of TonCoins.

#### store_dict
```
builder store_dict(builder b, cell c) asm(c b) "STDICT";
```
Stores dictionary `D` represented by cell `c` or `null` into builder `b`. In other words, stores a `1`-bit and a reference to `c` if `c` is not `null` and `0`-bit otherwise.
#### store_maybe_ref
```
builder store_maybe_ref(builder b, cell c) asm(c b) "STOPTREF";
```
Equivalent to `store_dict`.

### Builder size primitives
#### builder_refs
```
int builder_refs(builder b) asm "BREFS";
```
Returns the number of cell references already stored in builder `b`.
#### builder_bits
```
int builder_bits(builder b) asm "BBITS";
```
Returns the number of data bits already stored in builder `b`.
#### builder_depth
```
int builder_depth(builder b) asm "BDEPTH";
```
Returns the depth of builder `b`. If no cell references are stored in `b`, then returns `0`; otherwise the returned value is one plus the maximum of depths of cells referred to from `b`.

## Cell primitives
#### cell_depth
```
int cell_depth(cell c) asm "CDEPTH";
```
Returns the depth of cell `c`. If `c` has no references, then return `0`; otherwise the returned value is one plus the maximum of depths of cells referred to from `c`. If `c` is a `null` instead of a cell, returns zero.
#### cell_null?
```
int cell_null?(cell c) asm "ISNULL";
```
Checks whether `c` is a `null`. Usually a `null`-cell represents an empty dictionary. FunC also has polymorphic `null?` built-in, see [built-ins](/func/builtins?id=other-primitives).

## Dictionaries primitives
As said in [TVM.pdf](https://ton-blockchain.github.io/docs/tvm.pdf):
> Dictionaries admit two different representations as TVM stack values:
> * A slice `s` with a serialization of a TL-B value of type `HashmapE(n, X)`. In other words, `s` consists either of one bit equal to zero (if the dictionary is empty), or of one bit equal to one and a reference to a cell containing the root of the binary tree, i.e., a serialized value of type `Hashmap(n, X)`.
> * A “Maybe cell” `c^?`, i.e., a value that is either a cell (containing a serialized value of type `Hashmap(n, X)` as before) or a `null` (corresponding to an empty dictionary, cf. [null values](/func/types?id=null-values)). When a “Maybe cell” `c^?` is used to represent a dictionary, we usually denote it by `D`.  
>
> Most of the dictionary primitives listed below accept and return dictionaries in the second form, which is more convenient for stack manipulation. However, serialized dictionaries inside larger TL-B objects use the first representation.

In FunC dictionaries are also represented by the `cell` type with an implicit assumption that it may be a `null` value. There is no separate types for dictionaries with different key lengths or values types (after all, it's FunC, not FunC++).

### Taxonomy note
A dictionary primitive may interpret the keys of the dictionary either as unsigned `l`-bit integers, as signed `l`-bit integers or as `l`-bit slices. The primitives listed below differ by the prefix before the word `dict` in their names. `i` stands for signed integer keys, `u` stands for unsigned integer keys and empty prefix stands for slice keys.

For example, `udict_set` is a set-by-key function for dictionaries with unsigned integer keys, `idict_set` is the corresponding function for dictionaries with signed integer keys and `dict_set` is the function for dictionaries with slice keys.

In the titles empty prefix is used.

Also some of the primitives have their counterpart prefixed with `~`. It makes it possible to use them as [modifying methods](/func/statements?id=modifying-methods).

### Dictionary's values
A value in a dictionary may be stored either directly as subslice of an inner dictionary cell, or as a reference to a separate cell. In the first case it is not guaranteed that if the value fits into a cell, it fits to the dictionary (because a part of the inner cell may already be occupied by a part of the corresponding key). On the other hand, the second storing way is less gas-efficient. The second way is equivalent to storing in the first way a slice with empty data bits and exactly one reference to the value.

#### dict_set
```
cell udict_set(cell dict, int key_len, int index, slice value) asm(value index dict key_len) "DICTUSET";
cell idict_set(cell dict, int key_len, int index, slice value) asm(value index dict key_len) "DICTISET";
cell dict_set(cell dict, int key_len, slice index, slice value) asm(value index dict key_len) "DICTSET";
(cell, ()) ~udict_set(cell dict, int key_len, int index, slice value) asm(value index dict key_len) "DICTUSET";
(cell, ()) ~idict_set(cell dict, int key_len, int index, slice value) asm(value index dict key_len) "DICTISET";
(cell, ()) ~dict_set(cell dict, int key_len, slice index, slice value) asm(value index dict key_len) "DICTSET";
```
Sets the value associated with `key_len`-bit key `index` in dictionary `dict` to `value` (a slice), and returns the resulting dictionary.
#### dict_set_ref
```
cell idict_set_ref(cell dict, int key_len, int index, cell value) asm(value index dict key_len) "DICTISETREF";
cell udict_set_ref(cell dict, int key_len, int index, cell value) asm(value index dict key_len) "DICTUSETREF";
(cell, ()) ~idict_set_ref(cell dict, int key_len, int index, cell value) asm(value index dict key_len) "DICTISETREF";
(cell, ()) ~udict_set_ref(cell dict, int key_len, int index, cell value) asm(value index dict key_len) "DICTUSETREF";
```
Similar to `dict_set`, but with the value set to a reference to cell `value`.
#### dict_get?
```
(slice, int) idict_get?(cell dict, int key_len, int index) asm(index dict key_len) "DICTIGET" "NULLSWAPIFNOT";
(slice, int) udict_get?(cell dict, int key_len, int index) asm(index dict key_len) "DICTUGET" "NULLSWAPIFNOT";
```
Looks up key `index` in dictionary `dict` with `ket_len`-bit keys. On success, returns the value found as a slice along with a `-1` flag indicating success. On failure, returns `(null, 0)`.
#### dict_get_ref?
```
(cell, int) idict_get_ref?(cell dict, int key_len, int index) asm(index dict key_len) "DICTIGETREF";
(cell, int) udict_get_ref?(cell dict, int key_len, int index) asm(index dict key_len) "DICTUGETREF";
```
Similar to `dict_get?`, but returns the first reference of the found value.
#### dict_get_ref
```
cell idict_get_ref(cell dict, int key_len, int index) asm(index dict key_len) "DICTIGETOPTREF";
```
A variant of `dict_get_ref?` that returns `null` instead of the value if the key `index` is absent from dictionary `dict`.

#### dict_set_get_ref
```
(cell, cell) idict_set_get_ref(cell dict, int key_len, int index, cell value) asm(value index dict key_len) "DICTISETGETOPTREF";
(cell, cell) udict_set_get_ref(cell dict, int key_len, int index, cell value) asm(value index dict key_len) "DICTUSETGETOPTREF";
```
Sets the value associated with `index` to `value` (if `value` is `null`, then the key is deleted instead) and returns the old value (or `null`, if the value was absent).
#### dict_delete?
```
(cell, int) idict_delete?(cell dict, int key_len, int index) asm(index dict key_len) "DICTIDEL";
(cell, int) udict_delete?(cell dict, int key_len, int index) asm(index dict key_len) "DICTUDEL";
```
Deletes `key_len`-bit key `index` from dictionary `dict`. If the key is present, returns the modified dictionary `dict'` and the success flag `−1`. Otherwise, returns the original dictionary `dict` and `0`.
#### dict_delete_get?
```
(cell, slice, int) idict_delete_get?(cell dict, int key_len, int index) asm(index dict key_len) "DICTIDELGET" "NULLSWAPIFNOT";
(cell, slice, int) udict_delete_get?(cell dict, int key_len, int index) asm(index dict key_len) "DICTUDELGET" "NULLSWAPIFNOT";
(cell, (slice, int)) ~idict_delete_get?(cell dict, int key_len, int index) asm(index dict key_len) "DICTIDELGET" "NULLSWAPIFNOT";
(cell, (slice, int)) ~udict_delete_get?(cell dict, int key_len, int index) asm(index dict key_len) "DICTUDELGET" "NULLSWAPIFNOT";
```
Deletes `ket_len`-bit key `index` from dictionary `dict`. If the key is present, returns the modified dictionary `dict'`, the original value `x` associated with the key k (represented by a Slice), and the success flag `−1`. Otherwise, returns `(dict, null, 0)`.
#### dict_add?
```
(cell, int) udict_add?(cell dict, int key_len, int index, slice value) asm(value index dict key_len) "DICTUADD";
(cell, int) idict_add?(cell dict, int key_len, int index, slice value) asm(value index dict key_len) "DICTIADD";
```
An `add` counterpart of `dict_set`: sets the value associated with key `index` in dictionary `dict` to `value`, but only if it is not already present in `D`. Returns either modified version of the dictionary and `-1` flag or `(dict, 0)`.
#### dict_replace?
```
(cell, int) udict_replace?(cell dict, int key_len, int index, slice value) asm(value index dict key_len) "DICTUREPLACE";
(cell, int) idict_replace?(cell dict, int key_len, int index, slice value) asm(value index dict key_len) "DICTIREPLACE";
```
A `replace` operation, which is similar to `dict_set`, but sets the value of key `index` in dictionary `dict` to `value` only if the key was already present in `dict`. Returns either modified version of the dictionary and `-1` flag or `(dict, 0)`.
### Builder counterparts
The following primitives accept the new value as a builder instead of a slice, which often is more convenient if the value needs to be serialized from several components computed in the stack. The net effect is roughly equivalent to converting b into a slice and executing the corresponding primitive listed above.
#### dict_set_builder
```
cell udict_set_builder(cell dict, int key_len, int index, builder value) asm(value index dict key_len) "DICTUSETB";
cell idict_set_builder(cell dict, int key_len, int index, builder value) asm(value index dict key_len) "DICTISETB";
cell dict_set_builder(cell dict, int key_len, slice index, builder value) asm(value index dict key_len) "DICTSETB";
(cell, ()) ~idict_set_builder(cell dict, int key_len, int index, builder value) asm(value index dict key_len) "DICTISETB";
(cell, ()) ~udict_set_builder(cell dict, int key_len, int index, builder value) asm(value index dict key_len) "DICTUSETB";
(cell, ()) ~dict_set_builder(cell dict, int key_len, slice index, builder value) asm(value index dict key_len) "DICTSETB";
```
Similar to `dict_set` but accept a builder.
#### dict_add_builder?
```
(cell, int) udict_add_builder?(cell dict, int key_len, int index, builder value) asm(value index dict key_len) "DICTUADDB";
(cell, int) idict_add_builder?(cell dict, int key_len, int index, builder value) asm(value index dict key_len) "DICTIADDB";
```
Similar to `dict_add?`, but accept a builder.
#### dict_replace_builder?
```
(cell, int) udict_replace_builder?(cell dict, int key_len, int index, builder value) asm(value index dict key_len) "DICTUREPLACEB";
(cell, int) idict_replace_builder?(cell dict, int key_len, int index, builder value) asm(value index dict key_len) "DICTIREPLACEB";
```
Similar to `dict_replace?`, but accept a builder.
#### dict_delete_get_min
```
(cell, int, slice, int) udict_delete_get_min(cell dict, int key_len) asm(-> 0 2 1 3) "DICTUREMMIN" "NULLSWAPIFNOT2";
(cell, int, slice, int) idict_delete_get_min(cell dict, int key_len) asm(-> 0 2 1 3) "DICTIREMMIN" "NULLSWAPIFNOT2";
(cell, slice, slice, int) dict_delete_get_min(cell dict, int key_len) asm(-> 0 2 1 3) "DICTREMMIN" "NULLSWAPIFNOT2";
(cell, (int, slice, int)) ~idict::delete_get_min(cell dict, int key_len) asm(-> 0 2 1 3) "DICTIREMMIN" "NULLSWAPIFNOT2";
(cell, (int, slice, int)) ~udict::delete_get_min(cell dict, int key_len) asm(-> 0 2 1 3) "DICTUREMMIN" "NULLSWAPIFNOT2";
(cell, (slice, slice, int)) ~dict::delete_get_min(cell dict, int key_len) asm(-> 0 2 1 3) "DICTREMMIN" "NULLSWAPIFNOT2";
```
Computes the minimal key `k` in the dictionary `dict`, removes it and returns `(dict', k, x, -1)`, where `dict'` is the modified version of `dict` and `x` is the value associated with `k`. If the dict is empty, returns `(dict, null, null, 0)`.

Note that the key returned by `idict_delete_get_min` may differ from the key returned by `dict_delete_get_min` and `udict_delete_get_min`.

#### dict_delete_get_max
```
(cell, int, slice, int) udict_delete_get_max(cell dict, int key_len) asm(-> 0 2 1 3) "DICTUREMMAX" "NULLSWAPIFNOT2";
(cell, int, slice, int) idict_delete_get_max(cell dict, int key_len) asm(-> 0 2 1 3) "DICTIREMMAX" "NULLSWAPIFNOT2";
(cell, slice, slice, int) dict_delete_get_max(cell dict, int key_len) asm(-> 0 2 1 3) "DICTREMMAX" "NULLSWAPIFNOT2";
(cell, (int, slice, int)) ~udict::delete_get_max(cell dict, int key_len) asm(-> 0 2 1 3) "DICTUREMMAX" "NULLSWAPIFNOT2";
(cell, (int, slice, int)) ~idict::delete_get_max(cell dict, int key_len) asm(-> 0 2 1 3) "DICTIREMMAX" "NULLSWAPIFNOT2";
(cell, (slice, slice, int)) ~dict::delete_get_max(cell dict, int key_len) asm(-> 0 2 1 3) "DICTREMMAX" "NULLSWAPIFNOT2";
```
Computes the maximal key `k` in the dictionary `dict`, removes it and returns `(dict', k, x, -1)`, where `dict'` is the modified version of `dict` and `x` is the value associated with `k`. If the dict is empty, returns `(dict, null, null, 0)`.

#### dict_get_min?
```
(int, slice, int) udict_get_min?(cell dict, int key_len) asm (-> 1 0 2) "DICTUMIN" "NULLSWAPIFNOT2";
(int, slice, int) idict_get_min?(cell dict, int key_len) asm (-> 1 0 2) "DICTIMIN" "NULLSWAPIFNOT2";
```
Computes the minimal key `k` in dictionary `dict`, the associated value `x` and returns `(k, x, -1)`. If the dictionary is empty, returns `(null, null, 0)`.
#### dict_get_max?
```
(int, slice, int) udict_get_max?(cell dict, int key_len) asm (-> 1 0 2) "DICTUMAX" "NULLSWAPIFNOT2";
(int, slice, int) idict_get_max?(cell dict, int key_len) asm (-> 1 0 2) "DICTIMAX" "NULLSWAPIFNOT2";
```
Computes the maximal key `k` in dictionary `dict`, the associated value `x` and returns `(k, x, -1)`. If the dictionary is empty, returns `(null, null, 0)`.
#### dict_get_min_ref?
```
(int, cell, int) udict_get_min_ref?(cell dict, int key_len) asm (-> 1 0 2) "DICTUMINREF" "NULLSWAPIFNOT2";
(int, cell, int) idict_get_min_ref?(cell dict, int key_len) asm (-> 1 0 2) "DICTIMINREF" "NULLSWAPIFNOT2";
```
Similar to `dict_get_min?`, but returns the only reference in the value as a reference.
#### dict_get_max_ref?
```
(int, cell, int) udict_get_max_ref?(cell dict, int key_len) asm (-> 1 0 2) "DICTUMAXREF" "NULLSWAPIFNOT2";
(int, cell, int) idict_get_max_ref?(cell dict, int key_len) asm (-> 1 0 2) "DICTIMAXREF" "NULLSWAPIFNOT2";
```
Similar to `dict_get_max?`, but returns the only reference in the value as a reference.
#### dict_get_next?
```
(int, slice, int) udict_get_next?(cell dict, int key_len, int pivot) asm(pivot dict key_len -> 1 0 2) "DICTUGETNEXT" "NULLSWAPIFNOT2";
(int, slice, int) idict_get_next?(cell dict, int key_len, int pivot) asm(pivot dict key_len -> 1 0 2) "DICTIGETNEXT" "NULLSWAPIFNOT2";
```
Computes the minimal key `k` in dictionary `dict` that is greater than `pivot`, and returns `k`, associated value and a flag indicating success. If the dictionary is empty, returns `(null, null, 0)`.
#### dict_get_nexteq?
```
(int, slice, int) udict_get_nexteq?(cell dict, int key_len, int pivot) asm(pivot dict key_len -> 1 0 2) "DICTUGETNEXTEQ" "NULLSWAPIFNOT2";
(int, slice, int) idict_get_nexteq?(cell dict, int key_len, int pivot) asm(pivot dict key_len -> 1 0 2) "DICTIGETNEXTEQ" "NULLSWAPIFNOT2";
```
Similar to `dict_get_next?`, but computes the minimal key `k` that is greater than or equal to `pivot`.
#### dict_get_prev?
```
(int, slice, int) udict_get_prev?(cell dict, int key_len, int pivot) asm(pivot dict key_len -> 1 0 2) "DICTUGETPREV" "NULLSWAPIFNOT2";
(int, slice, int) idict_get_prev?(cell dict, int key_len, int pivot) asm(pivot dict key_len -> 1 0 2) "DICTIGETPREV" "NULLSWAPIFNOT2";
```
Similar to `dict_get_next?`, but computes the maximal key `k` smaller than `pivot`.
#### dict_get_preveq?
```
(int, slice, int) udict_get_preveq?(cell dict, int key_len, int pivot) asm(pivot dict key_len -> 1 0 2) "DICTUGETPREVEQ" "NULLSWAPIFNOT2";
(int, slice, int) idict_get_preveq?(cell dict, int key_len, int pivot) asm(pivot dict key_len -> 1 0 2) "DICTIGETPREVEQ" "NULLSWAPIFNOT2";
```
Similar to `dict_get_prev?`, but computes the maximal key `k` smaller than or equal to `pivot`.
#### new_dict
```
cell new_dict() asm "NEWDICT";
```
Creates an empty dictionary, which is actually a `null` value. Special case of `null()`.
#### dict_empty?
```
int dict_empty?(cell c) asm "DICTEMPTY";
```
Checks whether a dictionary is empty. Equivalent to `cell_null?`.

## Prefix dictionaries primitives
TVM also support dictionaries with non-fixed length keys which form a prefix code (i.e. there is no key that is a prefix of another key). Learn more about them in [TVM.pdf](https://ton-blockchain.github.io/docs/tvm.pdf).

#### pfxdict_get?
```
(slice, slice, slice, int) pfxdict_get?(cell dict, int key_len, slice key) asm(key dict key_len) "PFXDICTGETQ" "NULLSWAPIFNOT2";
```
Returns `(s', x, s'', -1)` or `(null, null, s, 0)`.
Looks up the unique prefix of slice `key` present in the prefix code dictionary `dict`. If found, the prefix of `s` is returned as `s'`, and the corresponding value (also a slice) as `x`. The remainder of `s` is returned as a slice `s''`. If no prefix of `s` is a key in prefix code dictionary `dict`, returns the unchanged `s` and a zero flag to indicate failure.
#### pfxdict_set?
```
(cell, int) pfxdict_set?(cell dict, int key_len, slice key, slice value) asm(value key dict key_len) "PFXDICTSET";
```
Similar to `dict_set`, but may fail if the key is a prefix of another key presented in the dictionary. Returns flag, indicating success.
#### pfxdict_delete?
```
(cell, int) pfxdict_delete?(cell dict, int key_len, slice key) asm(key dict key_len) "PFXDICTDEL";
```
Similar to `dict_delete?`.

## Special primitives
#### null
```
forall X -> X null() asm "PUSHNULL";
```
By the TVM type `Null` FunC represents absence of a value of some atomic type. So `null` can actually have any atomic type.
#### ~impure_touch
```
forall X -> (X, ()) ~impure_touch(X x) impure asm "NOP";
```
Mark a variable as used, such that the code which produced it won't be deleted even it is not impure. (c.f. [impure specifier](/func/functions?id=impure-specifier))


## Other primitives
#### min
```
int min(int x, int y) asm "MIN";
```
Computes the minimum of two integers `x` and `y`.
#### max
```
int max(int x, int y) asm "MAX";
```
Computes the maximum of two integers `x` and `y`.
#### minmax
```
(int, int) minmax(int x, int y) asm "MINMAX";
```
Sorts two integers.
#### abs
```
int abs(int x) asm "ABS";
```
Computes the absolute value of an integer `x`.
