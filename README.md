# Planet-Scale Public Cloud Evaluation of zeno, Vuvuzela, and Pung

This repository acts as the top-level list of pointers to all deployed Anonymous Communication
System (ACS), used configurations, and obtained results from our 2019 evaluation of
[zeno](https://github.com/numbleroot/zeno), [Vuvuzela](https://github.com/vuvuzela/vuvuzela),
and [Pung](https://github.com/pung-project/pung).


### Data Collection on Planet-Scale Public Cloud ACS Test Bed

In order to collect real-world data on the performance characteristics of the evaluated ACS,
we proposed and implemented an ACS test bed targeted for planet-scale experiments on public
clouds. It takes care of instance provisioning for each evaluated ACS and user base size,
conducts the experiments and collects the metrics of interest, and calculates statistics
and figures based on the collected data.

ACS test bed: [numbleroot/acs-test-bed](https://github.com/numbleroot/acs-test-bed).


### Prototype Fault-tolerant Mix-net zeno

We proposed a novel ACS based on the well-established mix-net architecture that is able to
remain available despite a large number of Byzantine failures. We implemented most components
of our proposal in prototype *zeno*, which is the first of three ACS we evaluate with the
help of our ACS test bed.

Prototype zeno: [numbleroot/zeno](https://github.com/numbleroot/zeno).


### Comparison System 1: Mix-net Vuvuzela

Mix-net [Vuvuzela](https://github.com/vuvuzela/vuvuzela) follows a conventional single-cascade
mix-net architecture. It was subsequently tightly integrated with metadata-private dialing
system [Alpenhorn](https://github.com/vuvuzela/alpenhorn), which made evaluation of core-Vuvuzela
difficult. Thus, we base our experiments of Vuvuzela on a fork of its source code as of late 2016
(right before integration of Alpenhorn) and with slight modifications that enabled scriptability
needed for such large-scale evaluation.

Fork of mix-net Vuvuzela on branch `vanilla-vuvuzela` with minor adjustments for evaluation
purposes: [numbleroot/vuvuzela](https://github.com/numbleroot/vuvuzela/tree/vanilla-vuvuzela).


### Comparison System 2: CPIR System Pung

Computational Private Information Retrieval (CPIR) system [Pung](https://github.com/pung-project/pung)
achieves its anonymity guarantees through the very different ACS foundation of PIR. Its basis on
the computational variant of this technique enables zerotrust deployments, i.e., a single untrusted
server that relays messages between clients via a highly optimized cryptographic protocol. Pung
also allows for anonymous group conversations and asynchronous retrievals, which neither zeno nor
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

Finally, we provide the full set of obtained measurements and collected log files for all failure
scenarios and user bases each of the ACS has been evaluated under. **Please mind:** the total size
of below repository is about 13GB, please only download it if you genuinely need the data.

2019 ACS evaluation measurements: [zeno-project/acs-eval-results](https://gitlab.tubit.tu-berlin.de/zeno-project/acs-eval-results).
