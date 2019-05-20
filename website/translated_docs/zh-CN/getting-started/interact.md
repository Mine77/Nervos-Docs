---
id: interact
title: Interacting with CKB
---

Once you have successfully started [running your own CKB node](run-node) and the miner program with it, you can try to interact with your node now.

Here you can learn about how to do this with RPC commands for some basic operations. Also, we have provided a simple SDK made with Ruby, which has wallet functionalities for you to interact with your node easily.

## Use RPC Command

You can interact with your CKB node client via RPC port. Here's an example showing how to get the header information of the tip block (the latest block).

Open a new shell, and use this command to get the tip block header (note that you should have the `ckb run` running):

```shell
curl -d '{"id": 2, "jsonrpc": "2.0", "method":"get_tip_header","params": []}' -H 'content-type:application/json' 'http://localhost:8114'
```

<details> <summary>(click here to view response)</summary>

```json
{
    "jsonrpc":"2.0",
    "result":{
        "difficulty":"0x1000",
        "epoch":"0",
        "hash":"0x7ab75ce1a45f30a6fe0d83856aa56827243c88271f4b8e2f968809b175fa2e7e",
        "number":"227",
        "parent_hash":"0xc1b02d64c8a294f1bc935706655213314926d33f031e84fe97fc601559aae9b1",
        "proposals_hash":"0x0000000000000000000000000000000000000000000000000000000000000000",
        "seal":{
            "nonce":"12843279316432878493",
            "proof":"0xa1060000d51100007b130000fd16000031200000982b0000fd370000d757000071730000dc740000a3790000a37b0000"
            },
        "timestamp":"1558138968104",
        "transactions_root":"0xc7067232dc4b44d393b50cea57635a642193963ac19ee3f5385940b2c23a5073",
        "uncles_count":"0",
        "uncles_hash":"0x0000000000000000000000000000000000000000000000000000000000000000",
        "version":"0",
        "witnesses_root":"0x822916ce5ad8b248f5ce549139c456abfdbba3ea3d2a8642c55da706876d0734"
        },
    "id":2
}
```

</details>

> The RPC port can be set in your [node configuration](https://github.com/nervosnetwork/ckb/blob/develop/docs/configure.md) file. By default, it uses port 8114.

You can find all the RPC commands in the [RPC API document](../api/rpc).

## Use Ruby SDK

There's a simple [Ruby SDK](https://github.com/nervosnetwork/ckb-sdk-ruby) that can provide an interactive console to help you work with your node.

### Installation

#### Install Ruby

First please refer the [Ruby official guidance](https://www.ruby-lang.org/en/downloads/) for installing the latest version of Ruby.

Ruby v2.4 or above are required for this SDK. Please check your Ruby version with:

```shell
ruby -v
```

#### Install Bundler

Then install bundler in case you have not installed it yet:

```shell
gem install bundler
```

#### Dependencies

[bitcoin-secp256k1](https://github.com/bitcoin-core/secp256k1) and [libsodium](https://download.libsodium.org/doc/) are needed as dependencies for this SDK.

To install bitcoin-secp256k1, clone the code to anywhere you like and install it with the scripts in it (you will need to enter your sudo password for the last step):

```shell
git clone https://github.com/bitcoin-core/secp256k1.git && \
cd secp256k1 && \
./autogen.sh && \
./configure && \
make && \
sudo make install 
```

To install libsodium, for macOS user you can use brew (for other systems please refer to the [libsodium wiki](https://github.com/crypto-rb/rbnacl/wiki/Installing-libsodium)):

```shell
brew install libsodium
```

#### Install SDK

Then clone the Ruby SDK repo to anywhere you like:

```shell
git clone https://github.com/nervosnetwork/ckb-sdk-ruby && \
cd ckb-sdk-ruby
```

Checkout to `master` branch:

```shell
git checkout master
```

Run bundler to install dependencies:

```shell
bundle
```

### Use API

Use this command to enter an interactive console:

```shell
bin/console
```

<details> <summary>(click here to view response)</summary>

```shell
$ bin/console 
[1] pry(main)> 
```

</details>

In the console, create an API instance (you need to keep the `ckb run` process alive for using API):

```ruby
api = CKB::API.new
```

<details> <summary>(click here to view response)</summary>

```ruby
[1] pry(main)> api = CKB::API.new
=> #<API@http://localhost:8114>
```

</details>

Then call RPC command with it:

```ruby
api.get_tip_header
```

<details> <summary>(click here to view response)</summary>

```ruby
[2] pry(main)> api.get_tip_header
=> #<CKB::Types::BlockHeader:0x00007fe5db8fcfa0
 @difficulty="0x1000",
 @epoch="0",
 @hash="0x09798b1170adcd608b65f2fbdc360b21555acde5b05295212f8b6cde9e72e880",
 @number="285",
 @parent_hash="0x12e738f2968bde032007349c543d4fa99cf8d82f354c102ab8a0a4ef6d284288",
 @proposals_hash="0x0000000000000000000000000000000000000000000000000000000000000000",
 @seal=
  #<CKB::Types::Seal:0x00007fe5db8fd068
   @nonce="4164299460367927268",
   @proof="0x140e0000191500004d1f0000ea2c0000ee2d0000362e0000f22e0000be310000993e000029470000bc5a0000fb6c0000">,
 @timestamp="1558139378253",
 @transactions_root="0x671a66d80e28103e1f19bdd631ec91feb4b8107e72341b0abe0e453e5fe961da",
 @uncles_count="0",
 @uncles_hash="0x0000000000000000000000000000000000000000000000000000000000000000",
 @version="0",
 @witnesses_root="0x0000000000000000000000000000000000000000000000000000000000000000">
```

</details>

> In the [GitHub repo](https://github.com/nervosnetwork/ckb-sdk-ruby/blob/master/lib/ckb/api.rb), you can find all the available RPC API in this Ruby SDK.

### Create Wallet

To create a wallet, we first need to generate a private key:

```ruby
privkey = CKB::Key.random_private_key
```

<details> <summary>(click here to view response)</summary>

```ruby
[1] pry(main)> privkey = CKB::Key.random_private_key
=> "0x99f5b41b3d02b74f262790f827890ab03c0b4f1e80427d0d24ceac2f0148d047"
```

</details>

You need to write down the returned privkey in order to use it later.

> Note that your private key is the only key to your tokens and assets. Losing private key or give it to others is as same as losing your tokens or give them away.

Then create an API instance:

```ruby
api = CKB::API.new
```

<details> <summary>(click here to view response)</summary>

```ruby
[2] pry(main)> api = CKB::API.new
=> #<API@http://localhost:8114>
```

</details>

Then we create a wallet with our private key:

```ruby
wallet = CKB::Wallet.from_hex(api, privkey)
```

<details> <summary>(click here to view response)</summary>

```ruby
[3] pry(main)> wallet = CKB::Wallet.from_hex(api, privkey)
=> #<CKB::Wallet:0x00007f932597a530
 @api=#<API@http://localhost:8114>,
 @key=
  #<CKB::Key:0x00007f932597b318
   @address=
    #<CKB::Address:0x00007f932597a580
     @prefix="ckt",
     @pubkey="0x0353051e82d41413c5e14e0ad3e24eba15c9e50c0823b920fae5c777f59265370c">,
   @privkey="0x99f5b41b3d02b74f262790f827890ab03c0b4f1e80427d0d24ceac2f0148d047",
   @pubkey="0x0353051e82d41413c5e14e0ad3e24eba15c9e50c0823b920fae5c777f59265370c">>
```

</details>

We can check the address of our wallet:

```ruby
wallet.address
```

<details> <summary>(click here to view response)</summary>

```ruby
[4] pry(main)> wallet.address
=> "ckt1q9gry5zgavgjvc3qhnvcujj5w95we9pyuxl3rj8mhwalwg"
```

</details>

Now we have successfully created a wallet instance from the generated private key in the Ruby SDK environment. If you encountered any problems, don't worry, check out the [trouble shooting document](../references/troubleshooting).

> In the [GitHub repo](https://github.com/nervosnetwork/ckb-sdk-ruby/blob/master/lib/ckb/wallet.rb), you can find all the available Wallet API in this Ruby SDK.

## More SDKs

SDKs in other languages are also available to use. Their documents will be supplemented soon. For now, please kindly refer the tests as usage examples.

* [Ruby SDK](https://github.com/nervosnetwork/ckb-sdk-ruby)
* [Javascript SDK](https://github.com/nervosnetwork/ckb-sdk-js)
* [Java SDK](https://github.com/nervosnetwork/ckb-sdk-java)
* [Swift SDK](https://github.com/nervosnetwork/ckb-sdk-swift)