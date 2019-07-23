#### Libra-Core-POC

###==============Clone and Build Libra Core===========######

### Clone the Libra Core Repository

$ git clone https://github.com/libra/libra.git

for testnet use --> 
 
 $ cd libra
 
 $ git checkout testnet

### Setup Libra Core

To setup Libra Core, change to the libra directory and run the setup script to install the dependencies, as shown below:

$ ./scripts/dev_setup.sh

### The setup script performs these actions:

    Installs rustup — rustup is an installer for the Rust programming language, which Libra Core is implemented in.
    Installs the required versions of the rust-toolchain.
    Installs CMake — to manage the build process.
    Installs protoc — a compiler for protocol buffers.
    Installs Go — for building protocol buffers.


### Build Libra CLI Client and Connect to the Testnet

To connect to a validator node running on the Libra testnet, run the client as shown below. 

###  Create Accounts


libra% account create
>> Creating/retrieving next account from wallet
Created/retrieved account #0 address 0c7ca9d474e464d8715f0615c1ed9c3cf98e31652f8c8c0f8c54cd96c7d63181

libra% account create
>> Creating/retrieving next account from wallet
Created/retrieved account #1 address 449c52af2c45f622d684150b83abcbc6dafd3aaa0d8ebc38501ea04abe2d36ed

libra% account list
User account index: 0, address: 0c7ca9d474e464d8715f0615c1ed9c3cf98e31652f8c8c0f8c54cd96c7d63181, sequence number: 0, status: Local
User account index: 1, address: 449c52af2c45f622d684150b83abcbc6dafd3aaa0d8ebc38501ea04abe2d36ed, sequence number: 0, status: Local

libra% account mint 0 1000000000000
>> Minting coins
Mint request submitted

libra% account mint 1 2000000000000
>> Minting coins
Mint request submitted

libra% query balance 0
Balance is: 1000000000000.000000

libra% query balance 1
Balance is: 2000000000000.000000

libra% query sequence 0
>> Getting current sequence number
Sequence number is: 0

libra% query sequence 1
>> Getting current sequence number
Sequence number is: 0

libra% transfer 0 1 123456
>> Transferring
Transaction submitted to validator
To query for transaction status, run: query txn_acc_seq 0 0 <fetch_events=true|false>

libra% txn_acc_seq 0 0 true
Unknown command: "txn_acc_seq"
libra% query txn_acc_seq 0 0 true
>> Getting committed transaction by account and sequence number
Committed transaction: SignedTransaction { 
 raw_txn: RawTransaction { 
	sender: 0c7ca9d474e464d8715f0615c1ed9c3cf98e31652f8c8c0f8c54cd96c7d63181, 
	sequence_number: 0, 
	payload: {, 
		transaction: peer_to_peer_transaction, 
		args: [ 
			{ADDRESS: 449c52af2c45f622d684150b83abcbc6dafd3aaa0d8ebc38501ea04abe2d36ed},
			{U64: 123456000000}, 
		]
	}, 
	max_gas_amount: 10000, 
	gas_unit_price: 0, 
	expiration_time: 1563907098s, 
}, 
 public_key: 1cf039769238aae9487d2d2ccef195208395c98d75e03d6db943ec94fb6b22af, 
 signature: Signature( R: CompressedEdwardsY: [206, 211, 205, 16, 104, 182, 67, 70, 19, 58, 230, 7, 254, 216, 77, 255, 30, 213, 79, 165, 141, 194, 89, 159, 182, 149, 70, 166, 222, 52, 67, 229], s: Scalar{
	bytes: [203, 21, 254, 161, 66, 236, 7, 248, 137, 148, 82, 202, 174, 214, 119, 26, 206, 235, 218, 93, 10, 28, 44, 183, 214, 8, 144, 115, 227, 88, 44, 3],
} ), 
 }
Events: 
ContractEvent { access_path: AccessPath { address: 0c7ca9d474e464d8715f0615c1ed9c3cf98e31652f8c8c0f8c54cd96c7d63181, type: Resource, hash: "217da6c6b3e19f1825cfb2676daecce3bf3de03cf26647c78df00b371b25cc97", suffix: "/sent_events_count/" } , index: 0, event_data: AccountEvent { account: 449c52af2c45f622d684150b83abcbc6dafd3aaa0d8ebc38501ea04abe2d36ed, amount: 123456000000 } }
ContractEvent { access_path: AccessPath { address: 449c52af2c45f622d684150b83abcbc6dafd3aaa0d8ebc38501ea04abe2d36ed, type: Resource, hash: "217da6c6b3e19f1825cfb2676daecce3bf3de03cf26647c78df00b371b25cc97", suffix: "/received_events_count/" } , index: 0, event_data: AccountEvent { account: 0c7ca9d474e464d8715f0615c1ed9c3cf98e31652f8c8c0f8c54cd96c7d63181, amount: 123456000000 } }
libra% query balance 1
Balance is: 2000000123456.000000

libra% query balance 0
Balance is: 999999876544.000000

libra% transferb 0 1 50
>> Transferring
[waiting transaction is stored!
Finished transaction!
To query for transaction status, run: query txn_acc_seq 0 1 <fetch_events=true|false>

