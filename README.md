# Planet-Scale Public Cloud Evaluation of FTMix, Vuvuzela, and Pung

Related publication: ["Strong Anonymity is not Enough: Introducing Fault Tolerance to Planet-Scale Anonymous Communication Systems"](https://dl.acm.org/doi/10.1145/3465481.3469189).

This repository lists the Anonymous Communication Systems (ACS), used configurations, and
obtained results from our 2019 evaluation of [FTMix](https://github.com/numbleroot/zeno)
(formerly *zeno*), [Vuvuzela](https://github.com/vuvuzela/vuvuzela), and
[Pung](https://github.com/pung-project/pung).


### Data Collection on Planet-Scale Public Cloud ACS Test Bed

In order to collect real-world data on the performance characteristics of the evaluated ACS,
we proposed and implemented an ACS test bed targeted for planet-scale experiments on public
clouds. It takes care of instance provisioning for each evaluated ACS and user base size,
conducts the experiments and collects the metrics of interest, and calculates statistics
and figures based on the collected data.

ACS test bed: [numbleroot/acs-test-bed](https://github.com/numbleroot/acs-test-bed).


### Prototype Fault-tolerant Mixnet FTMix

We integrated straightforward fault tolerance measures into a cascade-based, pool-style mixnet
called [FTMix](https://github.com/numbleroot/zeno), enabling it to remain available despite a
large number of Byzantine failures.

**Mind:** At the time of our experiments, [our proof-of-concept fault-tolerant mixnet was still
called *zeno*](https://github.com/numbleroot/zeno#note-on-name-and-scope-of-repository). We renamed
it to *FTMix* (**f**ault-**t**olerant **mix**net) due to scope change and to make its purpose
immediately clear through its name. In order not to create inconsistencies in the data sets,
however, we have not replaced 'zeno' with 'FTMix' in any of the GCP configuration files or result
logs. Please keep that in mind when you look at these files.


### Comparison System 1: Mixnet Vuvuzela

Mixnet [Vuvuzela](https://github.com/vuvuzela/vuvuzela) follows a conventional single-cascade
mixnet architecture. It was subsequently tightly integrated with metadata-private dialing
system [Alpenhorn](https://github.com/vuvuzela/alpenhorn), which made evaluation of core-Vuvuzela
difficult. Thus, we base our experiments of Vuvuzela on a fork of its source code as of late 2016
(right before integration of Alpenhorn) and with slight modifications that enabled scriptability
needed for such large-scale evaluation.

Fork of mixnet Vuvuzela on branch `vanilla-vuvuzela` with minor adjustments for evaluation
purposes: [numbleroot/vuvuzela](https://github.com/numbleroot/vuvuzela/tree/vanilla-vuvuzela).


### Comparison System 2: CPIR System Pung

Computational Private Information Retrieval (CPIR) system [Pung](https://github.com/pung-project/pung)
achieves its anonymity guarantees through the very different ACS foundation of PIR. Its basis on
the computational variant of this technique enables zerotrust deployments, i.e., a single untrusted
server that relays messages between clients via a highly optimized cryptographic protocol. Pung
also allows for anonymous group conversations and asynchronous retrievals, which neither FTMix nor
Vuvuzela provide. Again, we deployed a minimally adjusted fork of the Pung source code that integrates
into our ACS test bed.

Fork of CPIR system Pung with minimal adjustments for evaluation purposes:
[numbleroot/pung](https://github.com/numbleroot/pung).


### GCP Instance Configurations Used to Run the Experiments

As part of this repository, we provide the Google Cloud Platform (GCP) instance configurations that
we deployed in order to conduct our experiments. The files define the system to deploy, which zones
should experience failures if so indicated, a list of servers with precise configuration, and a list
of clients with precise configurations. In our evaluation, we deployed 1,000, 2,000, and 3,000 logical
users per ACS and failure scenario, respectively. The files can be parsed and applied by util
[`runexperiments`](https://github.com/numbleroot/acs-test-bed/blob/master/cmd/runexperiments/main.go).

* GCP configurations for 1,000 clients:
  [./gcloud-configs_clients-1000](https://github.com/numbleroot/acs-eval-2019/tree/master/gcloud-configs_clients-1000).
* GCP configurations for 2,000 clients:
  [./gcloud-configs_clients-2000](https://github.com/numbleroot/acs-eval-2019/tree/master/gcloud-configs_clients-2000).
* GCP configurations for 3,000 clients:
  [./gcloud-configs_clients-3000](https://github.com/numbleroot/acs-eval-2019/tree/master/gcloud-configs_clients-3000).


### Results

We provide the full set of obtained measurements and collected log files for all failure scenarios
and user bases each of the ACS has been evaluated under as an `xz`-compressed archive. After having
downloaded it, unpack and decompress it using `tar` with `xz`.

2019 ACS evaluation measurements (size: 463 MB): [https://osf.io/nfzy5](https://osf.io/nfzy5/).
