---
description: Practical strategies for securing the AI network
---

# AI Verification and Security

Since AI mining and validation were first discussed, the concept has remained vague.

At a high level, it all makes sense. Users say what they want; AI models figure it out. Great.

For projects that aren’t seriously building an AI network, this narrative may fly. We’re taking things a little bit more seriously.

In this post, I’ll explain a few core concepts that enable Nimble to process AI requests in the wild. That includes which types of requests we can and cannot handle and how we verify that the outcome we describe is achieved. We take user AI intents as an example to illustrate it.

<figure><img src="https://lh7-us.googleusercontent.com/u0CdEhtNd5T39SHCGA49BkADB24r2H8WIbJe6rKK-NaJocxMWfdNQcIIcvjE6ancyk5F32voDQVlUZrtI7NNMoA6_0oPyHyGBSUa_aOiFiHPt2I8cN5IjCH3fmmeso1K4pEMFxubVeWhS78YPFbKgco" alt=""><figcaption><p>Good intentions, poor execution</p></figcaption></figure>

### Entering the Network

To ensure Nimble can process AI requests that make their way into our network, we must ensure validity. Garbage in, garbage out, as they say. This is where Nimble is different from every other AI project.

AI requests to our network cannot be free-form.

Any good web developer can tell you - user input must be treated as garbage. Imagine the pentest results if someone fuzzed an AI network that accepted free-form input. Absolute chaos.

Web2 has well-established paradigms for users to submit their requests to a network. These are so good that even toddlers can use them.

![](https://lh7-us.googleusercontent.com/NgaNEGhr0yn35aE56MJKYmaxInOrON1-15Ci2d969Jtxefz3ePMDaHnsTZ-SCnzXx2Ca5nXW0VaK8oAsd\_\_APfevx3lqUHwzhblJBrqhqG50aqEACuijInXEHy7aE5rDjPCVMN1XZNl-ZFRNMI6D-Nk)

What do you think “X” does?

AI requests are submitted to Nimble via an intermediate interaction layer. There are two currently available layers:

1. Apps developed by Web2 devs
2. Network internal models like LLM, trained by the Nimble miners ([read more](https://docs.nimble.technology/practical-intents/natural-language-intents))

In the case of apps, developers structure AI requests and present them to users as familiar interactive elements. The developer interface is comparable to common query languages like [JQL](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/).

The “AI magic” for developers comes from operators that abstract blockchain details away from devs entirely. Sending tokens, for example, is a single operator:

**Send**

* From
* To
* Amount

The developer collects the required fields from the users or the context already available in the application. Then, they create the AI command and submit it to the network. The Nimble AI network receives the AI operation and identifies the optimal path to resolution through the available miner network.

Miners join auctions for individual AI operations they are capable of fulfilling.  Solutions will be validated and compared with each other in the auction. Nevertheless, the winning solution would also be checked on the contract to ensure it was fulfilled.

In this way, Nimble AI requests are both concrete and deterministic without losing any functionality.

#### **LLM-sourced Requests**

While most requests will enter the network via developer-sourced components like buttons/widgets, etc, some may enter via our LLM.&#x20;

LLM hallucinations are a known issue, and non-deterministic behavior cannot be allowed in financial systems.

To avoid issues with LLMs, we introduce an intermediate step between user input and request submission. In this step, the output of the LLM is presented to the user prior to submission. The user verifies that the LLM has properly captured the desired outcome. Only after confirmation is the intent submitted to the network.

#### Extensibility

AI operations are composable and extensible. At the time of network launch, we will support the operations needed to hide the complexity of the most common use cases. These include any combination of swaps, transfers, and bridges.

The community may propose new AI operations that support more complex use cases. These may include compound operations or entirely new operations.&#x20;

Our goal at launch is to enable one-click compound operations.&#x20;

<figure><img src="https://lh7-us.googleusercontent.com/lVb3xkloBU8WH1XXBlSM8QPyb1q6znnkO4jGBahlvzxaMru2v6wt4r7e0wo6uxHyE65pijS_JbRU8CrEDQTUSuxcENPNwXbDnNCVqkjFz9Dx6CsSf3INSCSF_2H7hq1asYEQPLRRXbEaXmskWLOwpAs" alt=""><figcaption><p>No bridge - only AI.</p></figcaption></figure>



Bridges are still used within the network as miners but leveraged as infrastructure only. Users no longer need to use bridges directly.

### Verification

An adversarial miner could submit low-ball bids to auctions to win mining rewards, then fail to submit the transactions. The network solves this issue internally.

Each request a user creates has a set of requirements that must be fulfilled. When the network accepts a solution, it will check to see if the requirements are met. If not, the miner's reputation will be penalized.

There are two types of requests. Solution verification is based on the AI operation type:

#### On-chain AI Operations

On-chain operation verification can be easily performed through DeFi operations. When miners submit a solution proposal to on-chain contracts, they describe the specific steps that will be taken to solve the intent.

The network can verify that the transactions were executed by checking the public ledger.

For example, imagine a miner proposes a solution that swaps Token A for Token B at a 1:1 ratio. The swap operation was only successful if completed within the described parameters.

Network rewards are processed after a successful transaction (or set of transactions). Bundlers only receive network token rewards when they return the profits to users and pay network fees, if any.

#### Off-chain AI Operations

Consider an AI network built on Nimble. A user submits an LLM request for an interactive, chatbot-like experience. GPT models from numerous developers compete to fulfill the operation. For chat requests, there will be a standardized evaluation function used to compare intents and evaluate them. Users rate GPT model responses. A reputation system built by user feedback is raw data for model evaluations.

In this way, for off-chain operations, a positive feedback loop between users and miners is achieved. Such feedback dynamics lay the foundation for network health.

### Attack Management

As a piece of public infrastructure, Nimble will be subject to dishonest and fraudulent behavior. This section details how the system responds to a variety of attacks.

#### Miner Reputation

For non-DeFi operations, a reputation system is required to ensure high-quality miner selection.&#x20;

As an orchestration layer, the network needs signals from the community in order to select truthful miners. For this purpose, we aim to implement miner reputations. Reputation is built as a weighted sum of staking (optional, yet critical), and a history of user feedback. In this way, low-quality miners are selected out of the network automatically, and high-quality miners are chosen more often.

Solutions proposed by miners who repeatedly provide invalid solutions will be rejected automatically.

#### Sybil Attacks

Sybil attacks are a type of fraud where many identities are created by one or a few individuals. It happens mostly for new identities and nodes. Nimble employs three strategies to prevent Sybil attacks:

* New nodes (e.g., users, miners, and validators) without existing reputations are likely Sybil nodes. As a result, they are placed under suspicion by other nodes on the network. They can prove their honesty with more network token stakes and a history of interactions with other nodes.
* Each node locally maintains social trust (decentralized, and nodes may have different social trust scores for the same node). To minimize the cost of the social trust-building process, nodes can exchange social trust scores. In this way, a good player can establish its reputation faster, while low reputation nodes find it hard to build reputations.
* The social trust system has another good side effect. It rewards early contributors to the network (e.g., miners, users, and validators). This is helpful for the network jumpstart and the philosophy that the network rewards early contributions.

#### DDoS Attacks

DDoS attacks happen when users and miners send bulk requests for the purpose of overwhelming the system. Attackers may create large amounts of spam operations (or solutions) that are invalid and make it difficult to select legitimate requests or solutions.

To prevent this, there are two things to be implemented:&#x20;

* Introducing fee markets by charging a fee for operations
* The miner with a high reputation can rate the operations and, thus, users. Low-rated requests should be dropped by the network

The above is just a list of critical security and verification considerations of operation. There are more considerations in the code.\