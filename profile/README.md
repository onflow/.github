
**Flow, the blockchain for open worlds  
‍  
‍**Flow is a fast, decentralized, and developer-friendly blockchain, designed as the foundation for a new generation of games, apps, and the digital assets that power them. It is based on a unique, multi-role architecture, and designed to scale without sharding, allowing for massive improvements in speed and throughput while preserving a developer-friendly, ACID-compliant environment.

Flow empowers developers to build thriving crypto- and crypto-enabled businesses. Applications on Flow can keep consumers in control of their own data; create new kinds of digital assets tradable on open markets accessible from anywhere in the world; and build open economies owned by the users that help make them valuable. 

Smart contracts on Flow can be assembled like Lego blocks to power apps serving billions of people, from basketball fans to businesses with mission-critical requirements.   
‍  
There are four pillars that make Flow unique among existing blockchains:

*   **Multi-role architecture:** Flow’s design is unique, allowing the network to scale to serve billions of users without sharding or reducing decentralization of consensus.
*   **Resource-oriented programming:** smart contracts on Flow are written in Cadence, an easier and safer programming language for crypto assets and apps.
*   **Developer ergonomics:** from upgradeable smart contracts and built-in logging support to the Flow Emulator, this network is designed for results.
*   **Consumer onboarding:** Flow was designed for mainstream consumers, with payment onramps catalyzing a safe and low-friction path from fiat to crypto.

While we originally started building Flow for our own use-cases, it has quickly become far bigger than us. Hundreds of developers in our [discord](http://chat.onflow.org/) and thousands around the world agree: we’re being something special here. Let’s build the future together!   
‍  

### Multi-Node Architecture  

In a traditional blockchain, every node stores the entire state (account balances, smart contract code, etc.) and performs all of the work associated with processing every transaction in the chain. This is analogous to having a single worker build an entire car. 

From manufacturing to CPU design, pipelining is a common technique for dramatically scaling up productivity. Flow applies pipelining to blockchains by separating the jobs of a validator node into four different roles: Collection, Consensus, Execution, and Verification. This separation of labor between nodes is vertical (across the different validation stages for each transaction) rather than horizontal (across different transactions, as with sharding). 

In other words, every validator node still participates in the validation of every transaction, but they do so only at one of the stages of validation. They can therefore specialize for — and greatly increase the efficiency of — their particular stage of focus. 

This allows Flow to scale to thousands of times higher throughput and lower cost while maintaining a shared execution environment for all operations on the network. In database terms, smart contracts and user accounts on Flow can always interact with each other in one atomic, consistent, isolated, and durable (ACID) transaction. This ensures good user experience and full composability, letting developers easily build on each other’s work.

### Problems with Sharding

Most proposals aim to improve the scalability of blockchains by fragmenting them into inter-connected networks: commonly shards, although sidechains have the same issues. These approaches remove serializability (“ACID”) guarantees common in database systems. 

Loss of ACID guarantees makes building an  app that needs to access data across fragments far more difficult and error-prone. Interactions between smart contracts become very complicated, and even individual large-scale applications would have to resort to complex mechanics to scale across shards due to latency issues and higher transaction failure rates. The combination dramatically limits the kinds of applications possible on the network as well as their network effects. **Sharding effectively saddles the hardest part of scaling the blockchain onto application developers rather than solving it at the protocol level.**

**‍**

A simple user action (purchasing a hat for a CryptoKitty using a stablecoin like TUSD) can take twelve transactions and seven blocks on a sharded blockchain. In an unsharded, ACID-compliant environment like Flow, the same action, and many more complex than it, can be handled by one atomic transaction in a single block.

Worse than the additional time and cost is the increased attack surface and complexity: it will be much harder to design, test, and harden the smart contract code on a sharded blockchain.

### Separating Consensus from Compute  

The core insight that led to architecture of Flow is that we can separate non-deterministic processes from deterministic ones and assign each to different types of nodes based on their technical capabilities to dramatically increase the blockchain throughput and solve several  user- and developer experience problems with existing networks at the same time. Our realization was that tasks within a blockchain can be divided into two types:   

*   Non-deterministic (or “subjective”) tasks, such as determining the presence and order of transactions in the blockchain
*   Deterministic (or “objective”) tasks, such as computing the result of those ordered transactions once it has been determined

Non-deterministic tasks require a coordinated consensus process (like Proof of Work or Proof of Stake). Deterministic tasks, on the other hand, always have a single, objectively-correct outcome. The critical insight behind Flow’s architecture was that the single biggest bottleneck to blockchain performance is the deterministic task of executing transactions after they’ve already been included into a block, and not the subjective process that requires consensus, i.e. the formation of the block itself. This insight is outlined in our first technical paper: [Separating Consensus and Compute](https://arxiv.org/pdf/1909.05821.pdf).  

### Flow Multi-Role Architecture

Flow pipelines the work of a blockchain miner or validator across four different roles that all require staking; a separation of concerns that significantly reduces redundant effort:

*   Consensus Nodes decide the presence and order of transactions on the blockchain
*   Verification Nodes are responsible for keeping the Execution Nodes in check
*   Execution Nodes perform the computation associated with each transaction
*   Collection Nodes enhance network connectivity and data availability for dapps

**Flow is designed such that even a single honest node, of any role, can punish and trigger recovery from invalid data introduced by dishonest Collection or Execution Nodes.   
‍  
‍**Consensus and Verification Nodes together are the foundation of security in the Flow network and leverage cryptoeconomic incentives to hold the rest of the network accountable.  These validators can optimize for security and decentralization: the roles of Consensus and Verification are streamlined to allow high levels of participation, even by individuals with consumer-grade hardware running on home internet connections. Consensus nodes run a variant of HotStuff, one of the most proven proof of stake algorithms.  

![proof of stake](https://assets-global.website-files.com/5f734f4dbd95382f4fdfa0ea/62f0de4b2f210850a33fd2c7_Flow-primer1.png)

  
Execution and Collection Nodes, on the other hand, do work that is fully deterministic – making them less vulnerable to attack. The work of these nodes is also verified and held accountable by the other node types. These node roles can therefore safely optimize for security and scalability, allowing the network to scale. Operating these nodes requires dedicated server hardware in a professionally managed data center.  

### Specialized Proofs of Confidential Knowledge (SPoCKs)

Specialized Proofs of Confidential Knowledge (SPoCKs) are a new cryptographic technique developed by the Flow team and formally defined in our [Technical Papers](https://www.onflow.org/technical-paper). SPoCKs allow any number of provers to demonstrate to a third-party observer that they each have access to the same _confidential knowledge_. These proofs are non-interactive and don't reveal the confidential knowledge. Each prover’s SPoCK is _specialized_ to them, and can’t be copied or forged by any other prover.   

Developer-First Experience
--------------------------

Our experience developing blockchain applications like CryptoKitties and the Dapper Smart Contract wallet has led us to incorporate a number of improvements to developer ergonomics directly into the protocol layer on Flow. Several are outlined below.

### **Cadence**

[Cadence](https://github.com/onflow/cadence) is the first ergonomic, resource-oriented smart contract programming language. 

While existing programming environments can be used to keep track of asset ownership, they are typically used in scenarios where they are _reflecting_ ownership rather than defining it directly. Public blockchains are unique in that they are explicitly designed to manage ownership of digital assets with scarcity and full access control. Digital assets on public blockchains behave like physical assets: they cannot be copied or counterfeited, only moved. 

Last year, the Flow team was investigating the use of [Linear Types](https://wiki.c2.com/?LinearTypes) in the context of blockchains, following [academic](https://src.acm.org/binaries/content/assets/src/2018/michael-coblenz.pdf) [research](http://www.cs.cmu.edu/~balzers/publications/digital_contracts_as_session_types.pdf) into better smart contract languages. At just about the same time, the Libra team defined a new programming model for [Move](https://developers.libra.org/docs/assets/papers/libra-move-a-language-with-programmable-resources/2019-09-26.pdf) based around a new ownership model inspired by Linear Types: resources. Resources are a new way of representing asset ownership and the properties of crypto-enabled digital assets directly in the programming language. From the Move paper’s introduction:  
‍_The key feature of Move is the ability to define custom resource types. Resource types are used to encode safe digital assets with rich programmability.__  
‍_We were so struck by the power of Resource-Oriented Programming that it’s one of the defining features of Cadence, a programming language designed specifically for the new paradigm of crypto-enabled applications. 

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

One of the most important promises made by smart contract platforms is that users can trust the smart contract code instead of trusting the smart contract authors. This aspect of blockchains unlocks use cases that we are only beginning to explore, the most impactful of which might be the concept of [open services and composability](https://jessewalden.com/4-eras-of-blockchain-computing-degrees-of-composability/).

In their first incarnation, smart contract platforms were designed such that contract code could never be changed after it is released. This is the most straightforward method to achieve the goal: If the code can’t be changed, even by the original authors, you clearly don’t need to trust the authors after the code is launched.

Unfortunately, software is hard to get right the first time. There are no shortage of examples of smart contracts that – even with incredibly talented teams and motivated communities – had subtle problems that led to a massive loss of funds.

Many developers have expressed the desire to fix or improve a smart contract after it has been deployed, and several have gone to a lot of time and trouble to build some mechanism into their smart contract to allow for upgrades or migrations. But having each developer “roll their own” mechanism for upgradability adds complexity, and makes those smart contracts harder to trust.

On Flow, we allow smart contracts to be deployed to the mainnet in a “beta state”, where the code can be incrementally updated by the original authors. Users will be alerted to the unfinished nature of this code, and can choose to wait until the code is finalized before trusting it. Once authors are confident that their code is safe, they can irrevocably release their control on the contract, and it becomes perfectly immutable for the rest of time.

This system balances the needs of users to be informed about what kind of code they are dealing with – whether or not an application or smart contract is truly trustless – while allowing developers the flexibility to tweak their code for a limited time after shipping.

### Fast, Deterministic Finality

From the standpoint of end users, the speed of a blockchain is most practically measured by the time it takes before they (or their client software) can be confident their transaction is permanently included in the chain. This is commonly referred to as “finality”. In Bitcoin, most people define finality as six block confirmations which can take more than an hour. Ethereum improves on this by achieving  [probabilistic finality](https://blog.ethereum.org/2016/05/09/on-settlement-finality/) after about 6 minutes. 

On Flow, deterministic finality is achieved within seconds: once Consensus Nodes determine which block a transaction will be a part of, user agents can in most cases execute the transaction locally and give feedback to the user almost immediately. In cases where results may be influenced by other transactions in the network, users will either choose to trust an execution node, using modern APIs to get feedback within a couple of seconds, or wait until the results of the transaction are sealed into the blockchain along with all the relevant execution and verification receipts. This process of block sealing and formal observation takes around 10  blocks; about ten seconds at launch.

### Built-in Logging Support

Sometimes, the only way to be sure that a complicated piece of software is working as expected is to log its behaviour, in detail, over a long period of time. Existing smart contract platforms don’t include a logging facility for the simple fact that storing a complete log record of the entire blockchain is completely intractable. Too much data!

Flow recognizes that since all smart contract transactions are fully deterministic, there is no need to store the actual logs for every transaction inside the network. Instead, Flow simply marks which transactions would have produced log messages for which topics. If someone wants to “examine” the logs, they can query the blockchain for the subset of transactions tagged with a particular topic and then re-run the transactions locally to generate those logs for analysis. This technique also makes event logging dramatically more efficient.

Consumer-Friendly Onboarding  

-------------------------------

In addition to mainstream-ready payment on-ramps (from other crypto tokens as well as fiat currencies), the Flow network makes it easy to build applications that people want to use:  

### Human Readable Security  

On current networks, it’s nearly impossible for an app or wallet software to provide a human-readable message clearly outlining what permissions they’re giving when authorizing a transaction. The Flow transaction format makes very strong guarantees about what kinds of changes a transaction can and can not make. This makes it easy for the wallet to ensure users are making informed decisions about what they are approving. 

It will be up to wallet software to display this information to the users, but by making the Flow transaction format easy to statically analyze, we create the possibility for a more transparent transaction approval process.

### Smart User Accounts: no more seed words or lost keys  

Flow is designed with flexibility in mind. Over the past year, Dapper Labs has pioneered a variety of usability enhancements to the Ethereum account model as part of the Dapper Smart Contract Wallet. Those enhancements are part of the native account model on Flow:  

*   Optional, modular, smart contract functionality built into every Flow wallet
*   This supports automated processes or more sophisticated authorization controls, in turn enabling good user experience. For example, dapps can easily make sure consumers never lose their assets – or access to their accounts – with secure account recovery flows
*   Added security through optional multiple signature support, with the ability to cycle out old keys regularly to avoid security leaks
