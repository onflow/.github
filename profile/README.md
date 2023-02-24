
## 🌊 Flow Blockchain
‍  
‍Flow is a fast, decentralized, and developer-friendly blockchain, designed as the foundation for a new generation of games, apps, and the digital assets that power them. It is based on a unique, multi-role architecture, and designed to scale without sharding, allowing for massive improvements in speed and throughput while preserving a developer-friendly environment.

Flow empowers developers to build thriving crypto- and crypto-enabled businesses. Applications on Flow can keep consumers in control of their own data; create new kinds of digital assets tradable on open markets accessible from anywhere in the world; and build open economies owned by the users that help make them valuable. 

-------------------------------

Our experience developing blockchain applications like CryptoKitties and the Dapper Smart Contract wallet has led us to incorporate a number of improvements to developer ergonomics directly into the protocol layer on Flow. Several are outlined below.

### **Cadence**

[Cadence](https://github.com/onflow/cadence) is the first ergonomic, resource-oriented smart contract programming language. 

While existing programming environments can be used to keep track of asset ownership, they are typically used in scenarios where they are _reflecting_ ownership rather than defining it directly. Public blockchains are unique in that they are explicitly designed to manage ownership of digital assets with scarcity and full access control. Digital assets on public blockchains behave like physical assets: they cannot be copied or counterfeited, only moved. 
 
‍[**Resource-oriented programming**](https://medium.com/dapperlabs/resource-oriented-programming-bee4d69c8f8e) is a new paradigm, designed to be secure and easy-to-use. For the first time, developers can create uniquely durable digital artifacts where ownership is tracked by the language itself, enabling a powerful new category of applications.

As the first high-level resource-oriented programming language, Cadence has a comfortable, ergonomic syntax making it very easy to read. It uses a strong, static type system to minimize runtime errors, and allows all methods, interfaces, and transactions to include pre- and post-conditions to enforce expected behaviour. This has resulted in a language that is easier to learn, significantly easier to audit, and ultimately much more productive than any current alternatives. You can start learning Cadence on Flow Playground: [play.onflow.org](https://play.onflow.org/)

### Open source tooling

The Flow team has open sourced a series of tools to help developers get started:

‍[**Flow Go SDK**](https://github.com/onflow/flow-go-sdk): the Go SDK is a great tool for developers looking for backend integration with scalability in mind. Go is one of the most popular backend programming languages when performance is a top priority, and has been the go-to choice for Dapper Labs.

‍[**Flow JavaScript SDK**](https://github.com/onflow/flow-js-sdk): for frontend developers, our JavaScript SDK will allow you to easily integrate and interact with Flow. Develop without using ABIs, construct composable interactions and create dapps that delight your users. We think you’re going to love building with our JavaScript SDK.

‍[**Visual Studio Code Extension**](https://github.com/onflow/flow/blob/master/docs/vscode-extension.md): interact with Flow and use the Cadence language natively in Visual Studio Code. Statically check your Cadence code for errors and test your smart contracts without leaving the comfort of this industry-leading IDE.

‍[**Flow Playground GUI**](https://github.com/onflow/flow-playground): the hosted, in-browser development environment where users can learn and try out Cadence smart contract language without any setup needed. We make it easy for any new developer to get a taste of Cadence, the powerful new language for smart contract development.

‍**Standards Proposals:** [FTs (Fungible tokens)](https://github.com/onflow/flow-FT) and [NFTs (Non-fungible tokens)](https://github.com/onflow/flow-NFT) are the Flow equivalent of Ethereum’s ERC-20 and ERC-721 tokens, respectively.

### Upgradable Smart Contracts

On Flow, we allow smart contracts to be deployed to the mainnet in a “beta state”, where the code can be incrementally updated by the original authors. Users will be alerted to the unfinished nature of this code, and can choose to wait until the code is finalized before trusting it. Once authors are confident that their code is safe, they can irrevocably release their control on the contract, and it becomes perfectly immutable for the rest of time.

### Built-in Logging Support

Flow recognizes that since all smart contract transactions are fully deterministic, there is no need to store the actual logs for every transaction inside the network. Instead, Flow simply marks which transactions would have produced log messages for which topics. If someone wants to “examine” the logs, they can query the blockchain for the subset of transactions tagged with a particular topic and then re-run the transactions locally to generate those logs for analysis. This technique also makes event logging dramatically more efficient.

## Consumer-Friendly Onboarding  

In addition to mainstream-ready payment on-ramps (from other crypto tokens as well as fiat currencies), the Flow network makes it easy to build applications that people want to use:  

### Human Readable Security  

On current networks, it’s nearly impossible for an app or wallet software to provide a human-readable message clearly outlining what permissions they’re giving when authorizing a transaction. The Flow transaction format makes very strong guarantees about what kinds of changes a transaction can and can not make. This makes it easy for the wallet to ensure users are making informed decisions about what they are approving. 

It will be up to wallet software to display this information to the users, but by making the Flow transaction format easy to statically analyze, we create the possibility for a more transparent transaction approval process.

### Smart User Accounts: no more seed words or lost keys  

Flow is designed with flexibility in mind. Over the past year, Dapper Labs has pioneered a variety of usability enhancements to the Ethereum account model as part of the Dapper Smart Contract Wallet. Those enhancements are part of the native account model on Flow:  

*   Optional, modular, smart contract functionality built into every Flow wallet
*   This supports automated processes or more sophisticated authorization controls, in turn enabling good user experience. For example, dapps can easily make sure consumers never lose their assets – or access to their accounts – with secure account recovery flows
*   Added security through optional multiple signature support, with the ability to cycle out old keys regularly to avoid security leaks
