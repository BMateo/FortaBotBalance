# Forta bot to track balance and emit alerts for polygon

 This document will explain how to initialize a repo and the modifications to the forta bot template to run in polygon.
 We use hardhat and the forta hardhat plug in.
 
 From an empty project:
 Run:
```
        npx hardhat init	
```
 	
 Select:  Create an empty hardhat.config.js
 Then follow the steps in the Cli to install all necesary dependencies.
 
 After that install the Forta Hardhat plugin with the following command:
```
        npm install -D hardhat-forta	
```

Remember to import the plugin in your hardhat.config.js with the line:
    ```
        require("hardhat-forta");
    ```

 The next step is:
 ```
        npx hardhat forta:init:template	
```
And select account-balance to init the template.

In the package.json add the following line to indicate the network
    ```
      "chainIds": [137]
    ```

Inside the agents folder add the next line in the forta.config.json file 
    ```
        "jsonRpcUrl": "https://polygon-rpc.com"
    ```
    
Then, in the agent-config.json file do the following changes:
- Set the developerAbbreviation, protocolName and protocolAbbreviation.
- Set the address/es to keep track of.
- Choose the threshold of MATIC balance to emit an alert if the account balance is lower.
- Then set the type and severity of the alert. Example: "type": "severity", "severity": "HIGH".
- Lastly set the minimun interval in seconds to receive alerts.

In agent.js:
Add the following
    ```
      const initializeData = {
      provider: new ethers.providers.JsonRpcProvider("https://polygon-rpc.com"),
      };
    ```
Then, inside the initialize function change: 
    ```
      data.provider = getEthersProvider();
    ```
For 
    ```
      data.provider = initializeData.provider;
    ```

For testing your bot locally run: 
```
npx hardhat forta:run
```

And you should see the bot running and the alerts appearing if the balance is less than the threshold
