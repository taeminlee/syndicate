# ![Syndicate](https://raw.githubusercontent.com/u3mur4/syndicate/master/logo.png) Syndicate Guide
Last update: 2017.09.13

Use this instruction and the youtube video to install the wallet, fix wallet issues and setup one/multiple masternode(s).
This guide is for the creation of separate Controller Wallet & Masternode.
For Security reasons, THIS IS THE PREFERRED way to run a Masternode. By running your Masternode in this way you are protecting
your coins in your private wallet, and are not required to have your local wallet running after the Masternode has been started successfully.
Your coins will be safe if the masternode server gets hacked.

## Table of Content
* [1. Desktop Wallet Preparation](#1-desktop-wallet-preparation)
	* [1.1 Download the desktop wallet](#11-download-the-desktop-wallet)
	* [1.2 Fix Wallet Sync Issue](#12-fix-wallet-sync-issue)
* [2. Masternode Setup](#2-masternode-setup)
	* [2.1 Send the coins to your wallet](#21-send-the-coins-to-your-wallet)
	* [2.2 VPS setup](#22-vps-setup)
	* [2.3 Automatic Masternode Setup](#23-automatic-masternode-setup)
	* [2.4 Add masternode on the desktop wallet](#24-add-masternode-on-the-desktop-wallet)
* [3. FAQ](#3-faq)
* [4. The last and the most important step](#4-the-last-and-the-most-important-step)


## 1. Desktop Wallet Preparation <a href="https://www.youtube.com/watch?v=CtnJlrl-kU0" target="_blank"><img src="http://mupantquat.com/wp-content/plugins/social-profiles-sidebar-widget/iconsets/elegant-media-icons/32x32/youtube.png"></a>

### 1.1 Download the desktop wallet
| Wallet        | Description  |
| --------------| -------------|
| [v1.0.1.8](https://github.com/SyndicateLabs/SyndicateQT/releases/download/v1.0.1.8/Syndicate.exe) | Sometimes freezes
| [v1.0.0.7](https://github.com/SyndicateLabs/SyndicateQT/releases/download/v1.0.0.7/SyndicateQTv1.0.0.7-2016-07-26.zip) | Still freezes!
| [~~patched~~](https://mega.nz/#!srpBkKyL!iUNsdLXDRiimHhkG-iNDFe8tEv5m70L1TWePHFnSkHQ)  | There is a patched wallet version on synxhodl slack channel. That is a good wallet but **not** official!

### 1.2 Fix Wallet Sync Issue
1. Unzip the wallet.
1. Start and Close the wallet. (creates the folder structure)
1. Download [Syndicate_blockchain_2017_09_10.zip](https://transfer.sh/t2Xo2/Syndicate_blockchain_2017_09_10.zip) bootstrap file. [mirror1](https://mega.nz/#!1iYBiSLR!-3UHVqz4X5fjLNBqn65OQTM_9zdl3V_AWhfzDb3meok) [older chain](http://108.61.216.160/cryptochainer.chains/chains/Syndicate_blockchain.zip)
1. Extract the zip file to `%appdata%/Syndicate/` folder. Override existing files!
1. Add the following content to the `%appdata%/Syndicate/Syndicate.conf` file or use [this](https://transfer.sh/14vce1/nodelist_09_10.txt) file that contains 122 active nodes.

    ```
    addnode=92.222.87.24:9996
    addnode=212.47.246.150:9999
    addnode=165.227.155.52:9999
    addnode=45.76.24.63:9999
    addnode=81.100.185.152:9999
    addnode=213.178.56.195:9999
    addnode=162.243.121.185:9999
    addnode=45.76.131.151:9999
    addnode=108.61.172.175:9999
    ```

1. Delete `%appdata%/Syndicate/peers.dat` file.
1. Start the wallet and wait for the sync. (30min to 10h depending on the number of the connections)
	
## 2. Masternode Setup <a href="https://www.youtube.com/watch?v=-Lt-ifQxS-w" target="_blank"><img src="http://mupantquat.com/wp-content/plugins/social-profiles-sidebar-widget/iconsets/elegant-media-icons/32x32/youtube.png"></a>

### 2.1 Send the coins to your wallet
1. Open Console (Help => Debug window => Console)
1. Create a new address. `getnewaddress Masternode1`
1. Send exactly 5000 coins to this address. (One transaction, pay attention to the fee)
1. Wait for the conformation.
1. Save the transaction id, index `masternode outputs`, and generate and save a new masternode private key `masternode genkey`.
1. You can optionaly encrypt the wallet (Settings => Encypt wallet) for security reasons. Do not forget the password or you lose the coins that you have.
1. Backup `%appdata%/Syndicate/wallet.dat` file. This contains your coins. DO NOT LOSE IT!

### 2.2 VPS setup
1. Register on [vultr](https://www.vultr.com/?ref=7205683). (or [DigitalOcean](https://m.do.co/c/93892c483019))
1. Send some money (10$ is enough for two months) to your account to deploy a server. (1 server cost 5$/mo, you can pay with bitcoin)
1. Deploy a new server.
    - Server Type: Ubuntu 14.04  
    - Server Size: 5$/mo, 1GB memory (This server is capable to run 3 masternodes. One masternode need 300-400Mb memory)

### 2.3 Automatic Masternode Setup
- Note: Use [this](https://github.com/u3mur4/syndicate/blob/master/MANUAL_SETUP.md) instruction to manualy setup the server.
1. Download [putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.70-installer.msi)
1. Start putty and login as root user. (Root password and server ip address is in vultr overview tab)
1. Paste this command and answer the questions:
```
wget https://raw.githubusercontent.com/taeminlee/syndicate/master/synx.py && python synx.py
```

### 2.4 Add masternode on the desktop wallet

1. Open wallet, wait for sync, unlock wallet
1. Go Masternodes tab
1. Click create
	- Set a name: Masternode1
	- Set the VPS ip and the port: [Ip:Port]
	- Set the generated private key: step 2.1.5
	- Click Add and after click Start
	- Wait 1 day to start receiving coins. Check your the masternode address here: [http://synx.cryptophi.com/](http://synx.cryptophi.com/)
	- Note: You can't edit the masternodes config in the wallet but you can edit the file. `%appdata%/Syndicate/masternode.conf`.

## 3. FAQ

1. What if I restart the server?
	- Connect to the server
	- Login every masternode account (use root account): `su mnX`
	- Start the masternode: `Syndicated`
	- Wait until fully sync
	- Start masternode from the wallet
1. How to get masternode profit?
	- Enable coin controll feature (Settings => Options => Display => Display coin controll feature)
	- Go send tab
	- Select from the input button only the 5 coin lines
	- Click OK
	- You can send selected amount to an address.
	- Note: DO NOT EVER Transfer synx from that original 5k deposit or you'll break your Masternode.
1. What is the password for the mn1, mn2, ...mnX accounts?
	- There is no default password. When you create a user it does not have a password yet, so you cannot login with that username until you create a password. There is one other way to act as a new user without its password. As root type `su - mn1`
	- You need to set a password for the user. Use the passwd command: `passwd mn1`
1. I get the following error: "Could not allocate vin"
	- Make sure your wallet fully synced and UNLOCKED.
1. How many masternodes can I run using one IP/server?
	- The limit is only the memory. One masternode requires 300-400mb ram. A server with 1GB memory can run 3 masternodes.
1. My wallet says my masternodes are not running.
	- The wallet will tell you its not running sometimes when it is. If you still receving the masternode rewards then everything is fine.
1. I got stuck. Can you help me?
	- Write an email to `u3mur4@gmail.com` with your problem or find me on synxhodl.slack.com (my username is u3mur4). Make sure to include the tx id that was generated by step 4 :)

## 4. The last and the most important step

Don't be shy, send a small amount of coin if you found this instruction helpful.

| Coin           | Address  |
| ---------------| ---------|
| Syndicate coin | SQaK48Xo9HToqCvG36YZACkFKbmHNamH6T |
| BTC 			 | 1GMWb8sGBrbYweyDnHtMzon56fcmQRb1j  |
| ETH 			 | 0x5E7c58EE90a684202227AB432d27DaAf51BBCA0f |

	
