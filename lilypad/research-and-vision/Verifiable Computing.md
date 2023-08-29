# Verifiable Computing

## Verifiable Computing Basics

Verifiable computing is dedicated to ensuring that outsourced computations (that is, computations that are not done locally) are done correctly. In some scenarios, it cannot be assumed that the node to which a job is being outsourced will compute the result honestly, or that it is not faulty. Moreover, verifying the result should have less overhead than computing the result in the first place.

While blockchains provide safety and liveness, the massive replication of computation becomes too costly when that level of security is not needed. There is a difference between global consensus, which is necessary in blockchain environments, and local consensus, which is more suited for two-sided marketplaces. In global consensus, all nodes need to be convinced that every computation was done correctly. In contrast, in local consensus, only a small number of nodes - potentially only one node, the client - needs to be convinced that a computation was done correctly.

Ostensibly, for a two-sided marketplace, this implies that only a client really needs to be convinced that a computation was done correctly. However, these computations are not done in isolation, and the interrelation between a client choosing one node repeatedly versus many different nodes, and the mathematics behind those decisions, as well as the need to create a protocol that any client can come along to with no prior experience and trust that cheating is disincentivized, implies the creation of a global game that, while not requiring global consensus in the traditional sense, emulates it in some manner.


## Approaches to Verifiable Computing


### Cryptographic Approaches

One way to ensure that computations were done correctly is by using cryptographic methods. There are a number of cryptographic approaches for verifiable computation, including

#### Interactive Proof (IP)

  * In interactive proofs, verification of a statement is modeled as an interaction between a prover and a verifier. The goal of the prover is to convince the verifier that the statement is true, even when the verifier does not have the computation resources to do the computation itself.
  
  * The protocol must satisfy completeness (if the statement is true, an honest verifier will be convinced) and soundness (if the statement is false, the prover cannot convince the verifier except with some negligible probability).

#### Zero-Knowledge Proof (ZKP)

  * Zero-knowledge proofs are a type of interactive proof where the verifier learns nothing about private inputs of the computation, other than that the outputs were computed correctly from the all the inputs (some of which may be public/known to the verifier).

  * A ZKP can be made non-interactive, in which case it is called a Non-Interactive Zero-Knowlege Proof (NIZK). Two common variants of NIZKs are zk-SNARKs (zero-knowledge Succinct Non-interactive Argument of Knowledge) and zk-STARKs (zero-knowledge Scalable Transparent Argument of Knowledge).

  * Like IPs, ZKPs must also satisfy the requirements of completeness and soundness.

#### Multi-Party Computation (MPC)

  * Multi-party computation allows multiple parties to jointly compute a function over their individual inputs without any party revealing its input to other parties. The main objectives of MPC are privacy (parties should learn known about each others' inputs), security (some level of anti-collusion preventing malicious attempts to learn information), functionality (the ability to compute functions over data), and robustness (the protocol should work correctly even in the presence of malicious behavior or faults). 


### Trusted Execution Environment (TEE)

  * Trusted Execution Environments are secure and isolated enclaves, where code and data inside of the enclave are insulated from the rest of the system, including the operating system, applications, and other enclaves. The goal is to maintain both the confidentiality and the integrity of the code and data. 


### Verification-via-Replication

Verification-via-replication - often described using the adjective "optimistic" in the blockchain world - relies on recomputing the computation to check whether the end result is the same. The benefits of this method are that it is the easiest to understand, and in some sense, the easiest to implement.

In contrast to the other approaches, verification-via-replication often requires reliance on game-theoretic mechanisms such as collateral slashing, reputation, and other methods. This can become a bit complex when trying to counter collusion between the nodes that are computing the results.

One of the downsides of this approach is, of course, the extra effort expended on recomputing computations. However, with proper incentives, the overhead of this can be reduced dramatically. It is also important to keep in mind that the overhead of this approach is much lower that cryptographic methods, which usually have much higher overhead.



## Our Approach

We opt for verification-via-replication as a first approach, for the reasons that it is simple to understand, has less overhead than cryptographic approaches, and has an attack surface that can be economically modeled and analyzed.

This has the downside of making private computations difficult. While the inputs and outputs of jobs can be encrypted so that only the client and compute node can see the code and data, this still leaves the client vulnerable to having their information leaked. Future approaches can incorporate SLAs and eventually support for homomorphic encryption to deal with this issue.
