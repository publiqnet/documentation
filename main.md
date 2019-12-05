### PUBLIQ

#### Introduction
The PUBLIQ ecosystem is designed as a decentralized reliable media open protocol. It consists of several layers abstracted from each other. At the core is the PUBLIQ blockchain, that primarily holds information on mined and transferred tokens, content metadata, content availability in distributed storage, and content popularity. PUBLIQ blockchain particularly supports content publishing/distribution and fair wealth distribution, it is designed for flexible business logic implementation.

The Distributed Storage operates on top of blockchain layer, all the files as a whole are stored on and served from the Distributed Storage.

More complex is the PUBLIQ Channel layer, which involves central components operating directly on Blockchain layer, core web components building the blockchain state relational database, as well as the actual channel web server that makes the channel web site, which implements the desired business logic.

#### PUBLIQ Blockchain
[publiq.pp](https://github.com/publiqnet/publiq.pp "publiq.pp") - repository is the core component, that includes blockchain layer, distributed storage layer implementations and important endpoints that the Channel layer operates with.

The publiq.pp [readme](https://github.com/publiqnet/publiq.pp/blob/master/README.md "publiq.pp") document describes how to build the blockchain node from source. The main product from this repository is the `publiqd` executable.

The publiq.pp [wiki](https://github.com/publiqnet/publiq.pp/wiki "wiki") covers more details on how to run the `publiqd` blockchain node, for different uses.

#### PUBLIQ Distributed Storage
[Storage node](https://github.com/publiqnet/publiq.pp/wiki/1.6-Storage-node "wiki") wiki page describes how to run a storage node for testnet.

This is the same publiqd executable configured in a special way to copy files to its own storage, and be a storage server. It is the `Channel layer's` duty to analyze storage nodes' activity information and to redirect file requests to storage nodes.

#### PUBLIQ Channel
[Channel node](https://github.com/publiqnet/publiq.pp/wiki/1.7-Channel-setup "wiki") wiki page of [publiq.pp](https://github.com/publiqnet/publiq.pp "publiq.pp") repository describes details how to configure PUBLIQ Channel core components with `publiqd` executable.

These define endpoints that are configured also for use by channel web components.
In particular
1. the _State node rpc endpoint_ is serving the action log to state component that maintains the relational database - the State DB.
1. the _Broadcast node rpc endpoint_ is used by channel back-end to broadcast any transactions to blockchain network.
1. the _Channel node rpc endpoint_ is used, again by channel back-end, to upload files to _Channel node storage_ or to report statistics.
1. the _Channel node storage endpoints_ to serve files over http or https protocol.
1. and the _Storage Order Token Generator endpoint_. This is a small utility, that is responsible for creating authorization tokens for storage nodes.

The next core component of _Channel layer_ is the **State DB and Backend**. [new-blockchain-state](https://github.com/publiqnet/new-blockchain-state "new-blockchain-state") is the repository responsible for this. The [readme](https://github.com/publiqnet/new-blockchain-state/blob/master/README.md "new-blockchain-state") describes how to setup and configure this component. In particular, it also covers the endpoints from above list.
The configuration variables rely on couple external components - the _OAuth_, and the _Language Detection_ services. The OAuth configuration default value refers to a working setup. And the language detection service will be explained later, for now it can be left empty as it is not essential for _State DB and Backend_. Configured cron jobs will build a MySQL DB with full information about the blockchain network state.
