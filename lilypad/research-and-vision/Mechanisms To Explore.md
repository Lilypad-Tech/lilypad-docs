# Mechanisms to Explore

The following is a list of mechanisms that we are currently considering exploring in order to mitigate attacks. Note that some of these mechanisms clearly would not be able to deter cheating and collusion alone. However, in combination with other mechanisms, they may achieve the goals. In this sense, they should be thought of as modules, optionally composable with each other.


##  Mediation

Clients call upon a mediation protocol in order to verify the results of a node. There are several variations of the structure of the mediation protocol; the following parameters can be varied:

1. The number of nodes in the mediation protocol.

2. If more than two nodes in the mediation consortium, the consensus threshold that determines which result is the one considered to be correct.

3. How the nodes are chosen.

    * For example, we may want as a baseline the same constraint as in Modicum - that only mediators that both the client and the compute node mutually trust can be used for mediation.

      * Even with this baseline, there is still a question of how to choose the node(s) - it can be random, be determined by an auction, or any other method.

4. Recursive mediation - that is, if there is no consensus in the consortium, do another mediation.

    * There is a large space of possibilities regarding how to execute this.

    * There needs to be a limit to the number of nodes this recursive process can use. For example, the set of potential nodes can be the same as the set of mutually trusted mediators, as described above.

5. Other methods discussed here, such as taxes and jackpots, as well as staking and prediction markets, can be incorporated into the mediation protocol.


## Collateralization

There are a number of different types of collateral that need to be included in the protocol.

The client needs to deposit collateral so that the compute node knows that it can be paid. For computations where the cost is known up front, this is simple. However, it becomes complicated for arbitrary compute; the client might not have put up enough collateral initially, so there may have to be a back-and-forth between client and compute node where the latter halts the computation until the former deposits more collateral or simply cancels the computation and pays for the partially computed result. If the client does not pay, then the compute node can invoke a mediation process.

The compute node needs to deposit several types of collateral.

1. Collateral in case they timeout.

    * This is put up as part of the deal agreement - that is, when the deal is posted on-chain.


2. Collateral in case they cheat.

    * The way that the compute node will convey the amount of collateral they will deposit to indicate that they will not cheat is via a collateral multiplier. The compute node commits to a multiple of whatever they will charge the client ahead of time as part of the deal agreement. The actual collateral is put up after the result is computed and sent to the client. This simplifies immensely the task of determining how much collateral to deposit for arbitrary computations.


3. Collateral in case they don't do the computation at the rate they said they would. This is closely related to timeout collateral.

    * Ideally, this is a way of enforcing deadlines on jobs.

    * It is not necessary to make this collateral slashing binary - for example, a late result can be still be rewarded.

    * It is enforceable if, for example, the compute node says that they will do X WASM instructions/time. However, technical limitations may make this unrealistic, and it needs to be tested.

One possible way to overcome collusion is to require super high collateral for some particular nodes against each other that that even discount factors very favorable to collusion would not incentivize collusion, even when accounting for repeated games.

While this is not a part of anti-cheating mechanisms, collateral pooling could lower capital requirements for collateralization. High capital requirements are a second-order concern, but will become a higher priority once robust anti-cheating mechanisms are implemented.


## Taxes and Jackpots (inspiration from Truebit)

Taking inspiration from the taxes and jackpots scheme used in Truebit, deals can be taxed, with those taxes going to a jackpot that is then used to reward nodes via some distribution protocol determined by the mediation process. For this, we want to be able to take any fraction of the jackpot(s) and distribute it arbitrarily to arbitrary nodes (perhaps even those not involved in the mediation process).  

This is a particularly interesting approach because the taxation + jackpots mechanism inherently create a global game that impacts local outcomes. While it may lead to potential collusion attacks, the tool alone is very useful, especially in conjunction with some other the other methods mentioned here. Modeling it in simulation would also provide the opportunity to test some of the hypotheses in the Truebit paper.

This method may also be useful in creating a robust platform where some clients do not care to check their results. That is, if some clients do not check results in general, it may be difficult to assert that the network is secure. Taxes and jackpots may be a way to address this.  


## Prediction/Replication Markets

Prediction markets have been well-studied in a variety of different fields. More recently, a type of prediction market called a replication  market has been explored in the context of replicability in science. With this inspiration, it may be possible that allowing nodes to make bets regarding the replicability of the computations of nodes may be useful in mitigating cheating. For example, nodes with a low prediction for replicability may act as a signal for that node's reputation and encourage it to behave honestly.

It is possible to overlay this mechanism on top of taxes, allowing nodes to choose where their taxes go in the prediction market.

Additionally, since Automated Market Makers are closely related to prediction markets, we can leverage many DeFi tools in this context.


## Staking behind nodes

Allow users to stake behind nodes. This is similar to prediction markets, but with slightly different economics. Like with prediction markets, it may be possible to tax users and then allow them to choose which nodes they stake behind. Overall, this approach is similar to delegated Proof-of-Stake.


## Announcing successful cheating

Can a node announcing that it successfully cheated (and thereby receiving a reward) benefit the robustness of the protocol? How much would this node have to be rewarded?


## Frequency of checks

How often should a client check results? Clearly it is related to the amount of collateral that the other node deposits, how much they value getting true/false results, reputation, and so on. This is a parameter that the client would need to learn to maximize its own utility.

## Reputation

The ledger can maintain a record, for each compute node, of the number of jobs the compute node has completed, the number of times its results were checked, and the number of times those results were replicated successfully. All other nodes (client and compute) could locally run some arbitrary function over these numbers to determine how reputable they find that node.

## Storing Inputs/Outputs

Results can only be replicated for as long as the inputs are stored somewhere. The client, compute node, or some other entity can pay for storing the inputs/outputs of jobs. The longer they are stored, the more time there is to check the results, which affects things like collateralization, the frequency of checks, etc.

This is related to, but not totally overlapping with, the amount of time that a node might have to wait before getting paid, which is the same time interval that a client has to check a result. However, checking the result after the node gets paid and receives back its collateral may still be possible, with other penalty schemes (or reward schemes, for example, coming from jackpots).


## Anti-Collusion via Obfuscation

Colluding requires the following knowledge in order to enforce the parameters of the collusion.

1. The public keys of the nodes participating in collusion.
2. The results that were posted by those public keys.
3. The payouts to the public keys.

In order to sign a collusion contract to begin with, the public keys must be known. However, in a mediation protocol with enough nodes, it may be possible to obscure (2) and (3) by

1. Having nodes submit results to the mediation protocol in an obscured/anonymous way
2. Have nodes be paid out according to the results of the mediation protocol in an obscured/anonymous way

If these two criteria can be met, then a mediation protocol based on them might be capable of imitating the game-theoretic outcomes seen in the Smart Contract Counter-Collusion paper.

There have been many decades of cryptography and security research focusing on similar problems to these. It may be the case that it is already possible to do this; otherwise, there is a large amount of ongoing research on the topics of privacy-preserving transactions, and much prior work in the flavor of secret-sharing/MPC/Tor/Monero/ZKPs that could enable this.
