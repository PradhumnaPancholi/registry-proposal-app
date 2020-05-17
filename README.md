# Registry Proposal 

The Research Collective's Registry Proposal app allows users to create a vote which (will) request an Organization's NFT token
 in exchange for stake and a resource proposal (vendor info/research publication). 
 
For example a scientist may request an addition to the expert DAO's registry by submitting a new paper and staking ETH.
The request would require a vote to approve, if the vote is rejected the user would receive their payment back. If
the vote passes the stake would be converted into rDAI held in escrow until the listing is removed, with the interest 
payments directed to the DAO's vault and the scientist issued a NFT as payment.

#### 🚨 Security review status: Not audited

## How does it work

The Registry Proposal App should be granted the `Create Votes` permission on an instance of the Aragon `Voting` app. When a user makes a request they should transfer the payment to the Token Request app which will hold them in escrow while the vote is created and executed. If the vote duration passes and the payment is still in the Token Request app, the user should be able to claim **their** tokens. If the vote passes then executing the vote should transfer the users tokens from the Token Request app to the organizations vault, and mint tokens from the token manager for the user.

### Initialization

The Registry Proposal app is initialized by passing the address of a `token manager` instance, the address of a `_vault` instance, and an array of addresses `_acceptedDepositTokens`. The `_acceptedDepositTokens` array must be less than the `MAX_ACCEPTED_DEPOSIT_TOKENS` variable which is set to 100.

### Roles

The Registry Proposal application should implement the following roles:

- Finalise token requests
- Change Vault Address
- Change Token Manager Address
- Add/remove offered tokens to/from the accepted offered token list

### Interface

We do not need to provide an interface for changing parameters as this can be done by power users using the aragonCLI.

The interface allows users to request tokens, where they would specify the amount and the associated payment.
It also allows for withdrawing their requests at any time.

For a detailed view of the flow of the app check out our [user-guide](./docs/user-guide.md)

## How to run Registry Proposal app locally

First make sure that you have node, npm, and the aragonCLI installed and working. Instructions on how to set that up can be found [here](https://hack.aragon.org/docs/cli-intro.html). You'll also need to have [Metamask](https://metamask.io) or some kind of web wallet enabled to sign transactions in the browser.

In another terminal:
```sh
aragon devchain
```

Git clone this repo.

```sh
git clone https://github.com/1Hive/token-request-app.git
```

Navigate into the `token-request-app` directory.

```sh
cd token-request-app
```

Install npm dependencies.

```sh
npm i
```

Deploy a dao with Lock app installed on your local environment.

```sh
npm run start:template
```
