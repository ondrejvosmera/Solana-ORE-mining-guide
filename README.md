# Mining $ORE Tokens on the Solana Blockchain with Ore V2 CLI
![ore](https://github.com/user-attachments/assets/2f730257-fb18-4078-b8c2-7bccd4c8e160)

This is a newbie-friendly guide to mining $ORE tokens on the Solana blockchain with Ore V2 Command Line Interface (CLI) on Linux-based operating systems (macOS, Ubuntu, Debian, etc.). Windows guide coming soon…

## Installation

### 1. Open Terminal

For macOS, press `command + space` and type “terminal” to open it.

### 2. Install Rust and Cargo

Run the following command and use the standard installation (press Enter when prompted):

```sh
curl https://sh.rustup.rs -sSf | sh
```

### 3. Install Solana CLI

Run the following command to install the Solana CLI:

```sh
sh -c "$(curl -sSfL https://release.solana.com/v1.18.4/install)"
```
### 4. Import Your Wallet

To import your wallet, run this command (ensure you have atleast 0.05 SOL inside):

```sh
solana-keygen recover 'prompt:?key=0/0' --outfile ~/.config/solana/id.json
```
This command will prompt you to enter your seed phrase. You can find this phrase in your Phantom app under Settings -> click your wallet at the top -> Show secret recovery phrase. Type in the 12 words, press Enter, and follow the prompts to confirm.

### 5. Check the Public Key

To verify that the public key matches the wallet address you have in Phantom, run:

```sh
solana-keygen pubkey
```
This command will output the public key of the wallet configured in your system. Compare this with the address in your Phantom wallet to ensure they match.

### 6. Install Ore CLI

Install the Ore CLI with the following command:

```sh
cargo install ore-cli
```

### 7. Mining Setup

#### Setting Up RPC Endpoint

To optimize your mining efficiency, you will need to set up an RPC endpoint. There are multiple providers to choose from, such as Helius, Alchemy, or Triton.

For this tutorial, we will use Alchemy:

1. Visit [Alchemy](https://www.alchemy.com/solana) and create a FREE plan profile.
2. Once you are in the Dashboard, select "Apps" from the menu.
3. Click on "Endpoints" on the right.
4. Locate Solana and copy the URL - this is your RPC endpoint.

#### Configuring the Mining

You need to configure several options for mining. This command displays all available commands and options for the ORE CLI.

```sh
ore -h
```
Here are some of the key options you’ll need to configure:

- `--rpc <NETWORK_URL>`: Paste your RPC endpoint URL here.
- `--keypair <KEYPAIR_FILEPATH>`: Enter the path to your keypair. This typically looks like "/Users/&lt;USER&gt;/.config/solana/id.json". Replace `<USER>` with your actual username.
- `--priority-fee <AMOUNT>`: Specify the maximum priority fee you are willing to pay for each transaction. A typical value might be 50,000 microlamports, considering the conversion rate where 1 SOL = 1,000,000,000 lamports and 1 lamport = 1,000 microlamports. Adjust according to network conditions and your willingness to pay for faster transaction processing.
- `--cores <NUMBER_OF_CORES>`: Set the number of CPU cores you want to allocate for mining. My M1 macbook has 8 cores, so I use 8.

### Final Command

Compile your settings into the final command to start mining. It should look something like this:

```sh
ore --rpc "<RPC_ENDPOINT>" --keypair "/Users/<USER>/.config/solana/id.json" --priority-fee 50000 mine --cores 8
```

Make sure to replace <RPC_ENDPOINT>, <USER> and adjust the priority-fee and cores according to your preferences and system capabilities.

## Happy mining!!!
