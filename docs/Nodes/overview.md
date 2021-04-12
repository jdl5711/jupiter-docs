# Overview


## General Wallet Info

The Jupiter blockchain is based on the NXT blockchain. 
[https://nxtdocs.jelurida.com/Getting_started](https://nxtdocs.jelurida.com/Getting_started) contains a lot of general info. So, if you need some help with the wallet, have a look over there and highly likely you will find your answer. 

Just to name some specific pages:

*	Account creation: [https://nxtdocs.jelurida.com/How_to_create_an_account](https://nxtdocs.jelurida.com/How_to_create_an_account)
*	The client interface: [https://nxtdocs.jelurida.com/Nxt_client_interface](https://nxtdocs.jelurida.com/Nxt_client_interface)
*	Sending JUP: [https://nxtdocs.jelurida.com/How_to_send_NXT](https://nxtdocs.jelurida.com/How_to_send_NXT)
*	Forging: [https://nxtdocs.jelurida.com/Forging_feature](https://nxtdocs.jelurida.com/Forging_feature)

    !!! note 
        It could be the forging bullet doesn’t turn green after entering your passphrase. Tests have shown the account is still forging.

*	Leasing: [https://nxtdocs.jelurida.com/Account_leasing](https://nxtdocs.jelurida.com/Account_leasing)

    !!! tip 
        You could use the leasing function to securely forge on your VPS. Create a new JUP account, send 1000 JUP to it, use this account to start forging on your VPS and then lease the rest of your JUP to this address. In this way you do not have to expose the seed of your main account to the VPS. Only thing you must take care of, the maximal leasing period is 65535 blocks, so you have to renew your lease every ~1.5 month.

*	Asset exchange: [https://nxtdocs.jelurida.com/Asset_exchange](https://nxtdocs.jelurida.com/Asset_exchange)
*	API guide: [https://nxtdocs.jelurida.com/API](https://nxtdocs.jelurida.com/API)


## Mainnet, ETH and BSC 

While mainnet JUP is needed to use dApps on the Jupiter blockchain, there are 2 more versions available, ERC20 JUP and BEP20 JUP, that are used for trading. You can switch 1:1 between the versions using gateways.
As a lot of info is updated now and then, instead of writing things down extensively with the risk the links might get outdated, below will only follow a short description of the different tokens and for more info you can have a look at the following link, that contains an up-to-date list of all important links related to Jupiter:
[https://docs.google.com/document/d/1iziiSDnbaOBIkbAJyzQFB8MRNjo8D7k8WxahwEKMgWM](https://docs.google.com/document/d/1iziiSDnbaOBIkbAJyzQFB8MRNjo8D7k8WxahwEKMgWM)

### Mainnet JUP
-	Gateway address: JUP-V5K2-269Z-QHGN-FSFT8
-	Can be stored in the native Jupiter wallet (web or standalone).
-	Can be used to create and use Jupiter dApps.
-	You can set up your own node and start forging to collect a share of the transaction fees. 
-	If you don’t want to run a node yourself, you can still earn transactions fees by participating in the FORGE pool. 


### ERC20 JUP
-	Contract address: 0x4B1E80cAC91e2216EEb63e29B957eB91Ae9C2Be8  
-	Gateway address: 0x34fbbb37eb4f50f447e736e7b771bd3ad20c41ca
-	Can be stored in any wallet that supports ERC20 tokens, for example Myetherwallet, MyCrypto, Trustwallet and Metamask (also in combination with Ledger and Trezor).  
-	Is used by exchanges, like Stex and Bilaxy.  
-	Can be traded on DEXes like Uniswap.


### BEP20 JUP
-	Contract address: 0x0231f91e02debd20345ae8ab7d71a41f8e140ce7
-	Gateway address: 0x34fbbb37eb4f50f447e736e7b771bd3ad20c41ca
-	Can be stored in any wallet that supports BEP20 tokens, for example Trustwallet and Metamask (also in combination with Ledger and Trezor).
-	Can be traded on DEXes like Pancakeswap.

## Other Sources
-	[https://github.com/jupiter-project/jupiter](https://github.com/jupiter-project/jupiter)
-	[https://github.com/jupiter-project/jupiter/releases](https://github.com/jupiter-project/jupiter/releases)
-	[https://nxtdocs.jelurida.com/Set_up_a_public_node_on_a_VPS](https://nxtdocs.jelurida.com/Set_up_a_public_node_on_a_VPS) 
-	[https://nxtdocs.jelurida.com/Getting_started](https://nxtdocs.jelurida.com/Getting_started)
-	[https://www.wavesassist.com/installation-waves-node](https://www.wavesassist.com/installation-waves-node)
-	[https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04)
-	[https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04)
-	[https://www.linode.com/docs/security/using-fail2ban-to-secure-your-server-a-tutorial](https://www.linode.com/docs/security/using-fail2ban-to-secure-your-server-a-tutorial)
-	[https://www.ssh.com/ssh/keygen](https://www.ssh.com/ssh/keygen)
-	[https://jupitertoolkit.com](https://jupitertoolkit.com)

