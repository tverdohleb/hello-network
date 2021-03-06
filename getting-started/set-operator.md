# Set an operator

## Who is the operator and what does he do?

The operator is the entity mainly responsible for producing, delivering and installing the asset. The operator receives the crowdsale funds in exchange for producing the asset. In our case, the operator receives funds to deliver coffees to investors that signed up to our platform. 

In this simple "hello world" example we are setting the operator to be the same entity as the broker. In reality, these roles can be played by different entities. See [roles in the MyBit network SDK](https://developer.mybit.io/network/#roles). 

## Adding the operator to the platform

### Get list of accounts 

Set a `const` to get a list of accounts controlled by the node. It uses the Web3 API to return an array of ethereum addresses. 

```javascript
const accounts = await web3.eth.getAccounts()
```

### Assign an account to an operator

Assign the second address in the array to be the operatorAddress.

```javascript
const [platformOwner, operatorAddress] = accounts
```

### Create operator ID variable 

```javascript
  var operatorID
```

### Set the operator

At this stage, we set an asynchronous `function setOperator()`. It will check whether an operator is already set or not in the platform. First, check the operator is already set: 

```javascript
  //Check if operator is already set
    var operatorURI = 'Mac the Operator';
    var id = await api.generateOperatorID(operatorURI);
    var currentAddress = await api.getOperatorAddress(id);
    if (currentAddress == '0x0000000000000000000000000000000000000000')
```

If all set then:

```javascript
console.log('Operator already set')
```

If the operator is not set, it will add a new operator to the platform, with an associated ID value, by parsing `operatorAddress`, `operatorURI` and `platformOwner`.

```javascript
      //If not set
      id = await Network.addOperator(
        operatorAddress,
        operatorURI,
        platformOwner
      );
```

The application will also make sure the operator accepts to receive payments in ether.

```javascript
    await Network.acceptEther(id, operatorAddress);
```

Only then the application  returns the set ID value for the operator in the platform. 

```javascript
    return id;
```

Under the hood, setting up the operator involves interacting with `network.js` and the APIs to interact with MyBit SDK contracts.  





