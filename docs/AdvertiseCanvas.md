# Advertise Canvas

## Connect to Metamask

 ```
 async function connectMetamask(){

  //Collect param values

  var wei = Number(document.getElementById('weiprice').value);
  var weitohex = "0x" + wei.toString(16);
  var inputhex = document.getElementById('span_inputhex').innerHTML.trim();
  var smartContractaddress = document.getElementById('span_address').innerHTML.trim();

  console.log(weitohex+','+inputhex+','+smartContractaddress)

  if (typeof window.ethereum !== 'undefined'
      || (typeof window.web3 !== 'undefined')) {
      // Web3 browser user detected. You can now use the provider.
      const provider = window['ethereum'] || window.web3.currentProvider
  }
  console.log(ethereum.isMetaMask);

  try {
    const accounts = await ethereum.enable();
    console.log("account: " +  accounts[0]);

    ethereum.send({
      method: 'eth_sendTransaction',
      params: [{"from": accounts[0],
      "to": smartContractaddress,
      "gas": "0x2DC6C0", // 30400
      "gasPrice": "0x2540BE400", 
      "value": weitohex, // 2441406250
      "data": inputhex}],
      //from: web3.eth.accounts[0], // Provide the user's account to use.
      from: accounts[0],
    },function(err, transactionHash) {
      if (!err){
        console.log(transactionHash); 
        if(transactionHash.result !== undefined){
          document.getElementById('span_metalink').innerText="https://kovan.etherscan.io/tx/"+transactionHash.result;
          document.getElementById('span_metalink').href="https://kovan.etherscan.io/tx/"+transactionHash.result;
          document.getElementById('span_success').innerText = "Transaction Successfully Done!!!";
        }
        else{
          document.getElementById('span_success').innerText = "User denied transaction signature.";
        }
      }
    })

  } catch (error) {
    console.log(error === "User rejected provider access")
  }
}

 ```
## Connect with Chrome Extension

```
    var laserExtensionId = "oapeiebamdabkniagfepfndnachjoieg";

    var weibal = Number(document.getElementById('weiprice').value);
    var weitoether = weibal / 1000000000000000000;
    var SMB = document.getElementById('span_address').innerHTML;
    var inputhex = document.getElementById('span_inputhex').innerHTML;
    inputhex = inputhex.replace('0x','');
    SMB = SMB.replace('0x','');
    var sendtrdetails = [SMB,weitoether,inputhex];

    chrome.runtime.sendMessage(laserExtensionId, sendtrdetails,
    function(response) {
      
    });
```
