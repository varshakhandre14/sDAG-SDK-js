## Requirements

-   Node.js
-   npm


## Installation

> npm i sdagraph


## Usage

### Create Account

#### Account Initialization

```
const sdag = require("sdagraph")

const pri = "eee21c84089ca7515d476a389f537d86edc80eb2c7b9d60c0c77d16ff40d2c87"
let account = new sdag.Accounts.NewAccount(pri)
```
#### Get account address and public key

```
account.Address
//11a0a990785b12d2bc09d35ac5a31a516ae9b77e
```
```
account.PublicKey
//04f6ff90a3717e09059272498b036390003782a2eb35085dcae8c471dd91472e21df38a4e43a7398698297d4b0e77a50abc7975b0d3984cdabef96c323d2cfbadf
```

### Transaction

#### Sign Transaction

##### Parameters

-   "To" : Enter the address of the destination (must be hex string without  prefix "0x").
    
-   "PrivateKey" : Enter the sender's private key.
    
-   "Balance" : Enter a number that is lower than the account balance in the sender's address.
    
-   "Nonce" : Enter the nonce number of the account in the sender's address.
    
-   "Gas" : Enter the number of transaction fees in the blockchain.
    
-   "Type" :
    
    1. "a64" : Stands for general transaction.  
    2. "a65" : Stands for contract of creation.  
    3. "a66" : Stands for contract of execution.
    
-   "Input" : The bytecode of the smart contract (must be hex string without  prefix "0x").

```
tx = {
	To : "a3d5b73a8e19e763df8ed9eb3e97c78958d440fb",
	PrivateKey : pri,
	Balance : "1",
	Nonce : "12",
	Gas : "1",
	Type : "a66",
	Input : "608060405234801561001057600080fd5b5060e68061001f6000396000f3fe6080604052600436106043576000357c01000000000000000000000000000000000000000000000000000000009004806360fe47b11460485780636d4ce63c14607f575b600080fd5b348015605357600080fd5b50607d60048036036020811015606857600080fd5b810190808035906020019092919050505060a7565b005b348015608a57600080fd5b50609160b1565b6040518082815260200191505060405180910390f35b8060008190555050565b6000805490509056fea165627a7a72305820249bb454073330c3d8e1b947438e2afa246e6705d2b5692b3764c41845d4bf3b0029"
}
let transaction = new sdag.Signs.NewTransaction(pri,tx)
var  signtrans  =  transaction.GetSignRawHexFull();
var  result  =  signtrans.result;
```
> ## result:
> balance:  "0000000000000000000001000000000000000000",

> crypto:  "a64",

> fee:  "0000000000000000000000000000000000000001",

>  gas:  "0000000000000000000000000000000000000001",

> input:  "608060405234801561001057600080fd5b5060e68061001f6000396000f3fe6080604052600436106043576000357c01000000000000000000000000000000000000000000000000000000009004806360fe47b11460485780636d4ce63c14607f575b600080fd5b348015605357600080fd5b50607d60048036036020811015606857600080fd5b810190808035906020019092919050505060a7565b005b348015608a57600080fd5b50609160b1565b6040518082815260200191505060405180910390f35b8060008190555050565b6000805490509056fea165627a7a72305820249bb454073330c3d8e1b947438e2afa246e6705d2b5692b3764c41845d4bf3b0029",

>  nonce:  11,

> publicKey:  "04f6ff90a3717e09059272498b036390003782a2eb35085dcae8c471dd91472e21df38a4e43a7398698297d4b0e77a50abc7975b0d3984cdabef96c323d2cfbadf",

> sign:  "c93445d7a9976a4c6f07cd8bb1cc7ec3f9f3ffb57b88e92fb965c498d35572e71c529fc3e8048bdbb2b33c14af08792ba9a92c30dec160a016878d3919db4d57",

> to:  "a3d5b73a8e19e763df8ed9eb3e97c78958d440fb",

> type:  "a66"


#### Broadcast Transaction

Above result will be used for broadcasting transaction.



