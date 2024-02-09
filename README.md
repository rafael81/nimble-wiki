---
description: A short guide to mining NIM by hosting AI models
---

# How Does AI Mining Work?

{% embed url="https://www.youtube.com/watch?ab_channel=NimbleNetwork&v=wZEwBtonnDQ" %}

This guide describes how you can earn NIM tokens by running a miner on Nimble Network, and why you may want to do so.

As a miner, your machines will host AI models in whole or in part. The network composes the results of multiple miners to train models and to serve their inferences to network users.

You will earn NIM tokens when your machine generates an inference or trains a model.

To get started now, head over to the [Nimble Miner's Repository on GitHub](https://github.com/nimble-technology/nimble-miners).

### Heterogeneous Training

Not every miner has the means to procure high-end GPUs required to run state-of-the-art (SOTA) machine learning models. To make AI more accessible, we need to enable commodity machines to participate in serving and training these models.

Nimble addresses this issue through heterogeneous training. Through these techniques, low-end machines with various operating systems can run portions of machine learning models rather than the entire model.

### Model and Data Parallelism

Through parallelism, the protocol split each model into individual modules, allowing portions of the model to be trained on distributed hardware. Models with billions of parameters can be divided among 10s or 100s of machines, dramatically reducing the hardware requirements.

Running GPT3.5, for example, requires 750GB of vram and 8 A100 GPUs per user interface. At the time of writing, an NVIDIA A100 GPU costs approximately $10,000.&#x20;

Through parallelism, Nimble aims to enable relatively small machines to run portions of SOTA models like GPT3.5. The results from individual machines can be consolidated into a single prediction result.

### Hardware Support

When big tech companies train large models, powerful homogeneous hardware is used. Data centers containing 100s or 1000s of high-end GPUs (A100, H100, etc) are used

For small AI teams, access to such data centers is prohibitively expensive or outright inaccessible due to high demand.

Through heterogenous hardware support, Nimble will enable low-end and commodity machines to be used in training SOTA models. Regardless of the underlying hardware, models can be divided among network participants to achieve efficient training.

Network participants are compensated in proportion to the portion of the model they train.

### Environment Setup

To set up your environment, visit the Nimble Miner GitHub repository -

[https://github.com/nimble-technology/nimble-miners](https://github.com/nimble-technology/nimble-miners)

Complete the following steps to get your miner up and running. These steps are described in detail in the README file.

1. Clone the repository
2. Install the required packages
3. Create wallets to hold your tokens
4. Select a model to run
5. Run your miner

### Model Selection

<figure><img src="https://lh7-us.googleusercontent.com/qx4rQKmBX-2kzipJ9UfYN7QSdj5o9Mz19zsXKjO_kmUTnZsbVk0lWRRmdDdcdmmfZFDc_oyaVMXVrIo53Nkd95l3thW7ZBRoMn6derexZ51vP69Pu-3mDghlpNLPtD6ZLB5ftSLncYhhhCPaQleFBYE" alt=""><figcaption></figcaption></figure>

As a miner, you earn NIM tokens by either serving a pre-trained machine-learning model, or by supporting the training of an untrained (or partially trained) model.

During testnet, your machine must be powerful enough to run the model in its entirety. Each model has a set of hardware requirements. To begin mining, select a model that matches your machine’s hardware. The list of supported models is available on GitHub.

[https://github.com/nimble-technology/nimble-miners?tab=readme-ov-file#example-usage](https://github.com/nimble-technology/nimble-miners?tab=readme-ov-file#example-usage)

#### Token Rewards

You will earn NIM tokens when your mining hardware is used to train models or serve inferences. During testnet, prompts are automatically generated by the network, guaranteeing usage of your mining machine.

To manage your earned tokens, use the wallet commands of the Nimble CLI.

Earned tokens are staked by default. To withdraw them, use the unstake command -

`nbcli stake remove --wallet.name yourWalletName`\


Once the tokens are unstaked you can use the transfer command to send them to an external wallet -

`nbcli wallet transfer`

