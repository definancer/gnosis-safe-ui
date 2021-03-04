# Gnosis Safe Multisig

The most trusted platform to store digital assets on Ethereum

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system. 

### Prerequisites

What things you need to install the software and how to install them

```
yarn add truffle // recommended usage of -g flag
yarn add ganache-cli // recommended usage of -g flag
yarn add flow-type // recommended usage of -g flag
```

We use [yarn](https://yarnpkg.com) in our infrastacture, so we decided to go with yarn in the README

### Installing and running

A step by step series of examples that tell you have to get a development env running

Install dependencies for the project:
```
yarn install
```

For using the Rinkeby services:
```
yarn start
```

If you prefer using Mainnet ones:
```
yarn start-mainnet
```

### Building
For Rinkeby:
```
yarn build
```


For Mainnet:
```
yarn build-mainnet
```

### set Networks
[safeContracts](./src/logic/contracts/safeContracts.ts)
``` javascript
/**
 * Creates a Contract instance of the GnosisSafeProxyFactory contract
 * @param {Web3} web3
 * @param {ETHEREUM_NETWORK} networkId
 */
const getProxyFactoryContract = (web3: Web3, networkId: ETHEREUM_NETWORK): GnosisSafeProxyFactory => {
  const networks = ProxyFactorySol.networks
  // TODO: this may not be the most scalable approach,
  //  but up until v1.2.0 the address is the same for all the networks.
  //  So, if we can't find the network in the Contract artifact, we fallback to MAINNET.
  const contractAddress = networks[networkId]?.address ?? networks[ETHEREUM_NETWORK.MAINNET].address
  return (new web3.eth.Contract(ProxyFactorySol.abi as AbiItem[], contractAddress) as unknown) as GnosisSafeProxyFactory
}
```
```
export const SENTINEL_ADDRESS = '0x0000000000000000000000000000000000000001'
export const MULTI_SEND_ADDRESS = '0x8d29be29923b68abfdd21e541b9374737b49cdad'
export const SAFE_MASTER_COPY_ADDRESS = '0x34CfAC646f301356fAa8B21e94227e3583Fe3F5F'
export const DEFAULT_FALLBACK_HANDLER_ADDRESS = '0xd5D82B6aDDc9027B22dCA772Aa68D5d74cdBdF44'
export const SAFE_MASTER_COPY_ADDRESS_V10 = '0xb6029EA3B2c51D09a50B53CA8012FeEB05bDa35A'
``` 


## Running the tests

1. Run `transaction-history-service`
```
git clone https://github.com/gnosis/safe-transaction-service.git
cd safe-transaction-service
git checkout develop
docker-compose build
# it comes enabled by default in docker-compose
sudo service postgresql stop
docker-compose up -d
```
Check that the service is running at https://localhost:8000

2. Migrate Safe Contracts:
```
git clone https://github.com/gnosis/safe-contracts.git
cd safe-contracts
yarn
npx truffle migrate
```
3. Migrate Token Contracts for the tests:
Inside `safe-react` directory
```
npx truffle migrate
```
4. Run the tests:
```
yarn test
```


### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Configuring the app for running on different networks

[Please check the network configuration documentation](./docs/networks.md)

## Built With

* [Truffle React Box](https://github.com/truffle-box/react-box) - The web framework used
* [Ganache](https://github.com/trufflesuite/ganache-cli) - Fast Ethereum RPC client
* [React](https://reactjs.org/) - A JS library for building user interfaces
* [Material UI 4.X](https://material-ui.com/) - React components that implement Google's Material Design
* [redux, immutable, reselect, final-form](https://redux.js.org/) - React ecosystem libraries
* [Flow](https://flow.org/) - Static Type Checker

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/gnosis/gnosis-team-safe/tags). 

## Authors

- Germán Martínez([germartinez](https://github.com/germartinez))
- Mikhail Mikheev([mikheevm](https://github.com/mikheevm))

See the full list of [contributors](https://github.com/gnosis/gnosis-team-safe/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Thanks for Gnosis Team for providing the Safe contracts.
