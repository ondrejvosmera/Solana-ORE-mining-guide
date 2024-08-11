# Mining $ORE Tokens on the Solana Blockchain with Ore V2 CLI
![ore](https://github.com/user-attachments/assets/2f730257-fb18-4078-b8c2-7bccd4c8e160)

This is a newbie-friendly guide to mining $ORE tokens on the Solana blockchain with Ore V2 Command Line Interface (CLI) on Linux-based operating systems (macOS, Ubuntu, Debian, etc.). Windows guide coming soon…

## Linux-based systems (macOS)

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
To update to the newest version, run this command:

```sh
solana-install update
```

### 4. Add Solana to your PATH

To ensure you can run Solana commands from any terminal session, add the following line to your shell configuration file. Replace <USER> with your own username. (If you don’t know yours, run command echo $USER).

```sh
export PATH="Users/<USER>/.local/share/solana/install/active_release/bin:$PATH"
```

### 5. Import Your Wallet

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
Restart your terminal before you start mining.

## Windows

### 1. Install Rust and Cargo

Go to https://www.rust-lang.org/tools/install and download Rust (to find out if you have 32bit or 64bit system — Start button -> Settings -> System -> About). Run the .exe, when prompted type “1” press Enter. You may be prompted to install Visual Studio C++ Build tools, which is necessary, so install it aswell.

### 2. Install Solana CLI
Open CMD as an administrator (Search -> type “cmd.exe”, right click and choose “Run as administrator”), and run this command:

```sh
cmd /c "curl https://release.solana.com/v1.18.18/solana-install-init-x86_64-pc-windows-msvc.exe --output C:\solana-install-tmp\solana-install-init.exe --create-dirs"
```

Next, run this command. If you see security pop-up, select to allow the program to run:

```sh
C:\solana-install-tmp\solana-install-init.exe v1.18.18
```

After this you will need to close your terminal and open it again (as administrator).

For updating to latest version, run:

```sh
solana-install update
```

### 3. Import your wallet
To import your wallet, run this command (ensure you have atleast 0.05 SOL inside):

```sh
solana-keygen recover prompt:?key=0/0 — outfile %USERPROFILE%\.config\solana\id.json
```

This command will prompt you to enter your seed phrase. You can find this phrase in your Phantom app under Settings -> click your wallet at the top -> Show secret recovery phrase. Type in the 12 words, press Enter, and follow the prompts to confirm.

Recovered pubkey should and needs match your wallet address you see in Phantom.

You can always check the pubkey with this command:

```sh
solana-keygen pubkey
```

### 4. Install Ore CLI
Install the Ore CLI with the following command (you will also use this command to update your CLI):

```sh
cargo install ore-cli
```

Restart your terminal again, before you start mining.


## Mining Setup

### 1. Setting Up RPC Endpoint

To optimize your mining efficiency, you will need to set up an RPC endpoint. There are multiple providers to choose from, such as Helius, Alchemy, or Triton.

For this tutorial we will use Helius:

1. Go to [Helius](https://www.helius.dev/), click on “Start for free” and sign up.
2. Once you are in the Dashboard choose “RPCs” in the menu.
3. Here, under Mainnet is your RPC URL.

### 2. Configuring the Mining

You need to configure several options for mining. This command displays all available commands and options for the ORE CLI.

```sh
ore -h
```
Here are some of the key options you’ll need to configure:

- `--rpc <NETWORK_URL>`: Paste your RPC endpoint URL here.
- `--keypair <KEYPAIR_FILEPATH>`: Enter the path to your keypair. This typically looks like "/Users/&lt;USER&gt;/.config/solana/id.json". Replace `<USER>` with your actual username.
-  `--dynamic-fee`: Sets fees dynamically and is capped with priority-fee command. Works only with Helius and Triton RPC.
- `--priority-fee <AMOUNT>`: Specify the maximum priority fee you are willing to pay for each transaction. A typical value might be 50,000 microlamports, considering the conversion rate where 1 SOL = 1,000,000,000 lamports and 1 lamport = 1,000 microlamports. Adjust according to network conditions and your willingness to pay for faster transaction processing.
- `--cores <NUMBER_OF_CORES>`: Set the number of CPU cores you want to allocate for mining. My M1 macbook has 8 cores, so I use 8.

### 3. Final Command

Compile your settings into the final command to start mining. It should look something like this:

```sh
ore --rpc "<RPC_ENDPOINT>" --keypair "/Users/<USER>/.config/solana/id.json" --dynamic-fee --priority-fee 50000 mine --cores 8
```

Make sure to replace <RPC_ENDPOINT>, <USER> and adjust the priority-fee and cores according to your preferences and system capabilities.

## Happy mining!!!
