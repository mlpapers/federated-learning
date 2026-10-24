# Federated Learning

## Data ownership, populations and objectives

- **Federated setting** - Clients train collaboratively while keeping raw training data decentralized. Kairouz et al. distinguish statistical, system and privacy challenges; retaining data locally does not prevent leakage through model updates. [Kairouz et al. 2021](<https://arxiv.org/abs/1912.04977> "Advances and Open Problems in Federated Learning; Foundations and Trends in Machine Learning").
- **Cross-device versus cross-silo** - Many intermittently available devices and a small set of participating organizations impose different participation, trust and resource constraints. State the deployment regime before comparing federated algorithms. [Kairouz et al. 2021](<https://arxiv.org/abs/1912.04977> "Advances and Open Problems in Federated Learning; Foundations and Trends in Machine Learning").
- **Vertical federated learning** - Parties hold different features for overlapping entities, rather than separate examples with a shared feature schema. Entity alignment, label ownership and intermediate-information leakage become central design questions. [Liu et al. 2024](<https://arxiv.org/abs/2211.12814> "Vertical Federated Learning: Concepts, Advances and Challenges; TKDE").

## Global-model optimization under heterogeneity

- **FedAvg** - Selected clients train locally and the server averages their models, typically weighted by local example counts. More local work reduces synchronization frequency but can amplify differences between client objectives. [McMahan et al. 2017](<https://proceedings.mlr.press/v54/mcmahan17a.html> "Communication-Efficient Learning of Deep Networks from Decentralized Data; AISTATS").
- **FedProx** - Adds a proximal penalty toward the current global model and permits variable local work. Li et al. analyze statistical and system heterogeneity; the penalty constrains local drift rather than making client data identical. [Li et al. 2020](<https://arxiv.org/abs/1812.06127> "Federated Optimization in Heterogeneous Networks; MLSys").
- **SCAFFOLD** - Uses control variates to correct client drift caused by heterogeneous local objectives. Karimireddy et al.'s convergence analysis distinguishes this correction from merely shortening each client's local training. [Karimireddy et al. 2020](<https://proceedings.mlr.press/v119/karimireddy20a.html> "SCAFFOLD: Stochastic Controlled Averaging for Federated Learning; ICML").
- **FedNova** - Normalizes client updates to address objective inconsistency caused by unequal amounts of local computation. Its target is aggregation bias, distinct from feature shift or adversarial clients. [Wang et al. 2020](<https://arxiv.org/abs/2007.07481> "Tackling the Objective Inconsistency Problem in Heterogeneous Federated Optimization; NeurIPS").
- **Adaptive federated optimization** - FedAdagrad, FedAdam and FedYogi apply adaptive updates at the server while clients perform local optimization. Reddi et al. analyze nonconvex heterogeneous objectives; client and server learning rates play different roles. [Reddi et al. 2021](<https://arxiv.org/abs/2003.00295> "Adaptive Federated Optimization; ICLR").

## Client participation and asynchronous updates

- **Power-of-Choice selection** - Prefers clients with high local loss. Cho et al. analyze a tradeoff between convergence speed and solution bias; selection changes the effective optimization process, so comparisons must state the target client weights. [Cho et al. 2020](<https://arxiv.org/abs/2010.01243> "Client Selection in Federated Learning: Convergence Analysis and Power-of-Choice Selection Strategies; arXiv").
- **Oort** - Selects training clients using estimated data utility and execution speed to improve time to accuracy. Its testing selector separately targets a requested data distribution; fast training participation and representative evaluation are different objectives. [Lai et al. 2021](<https://www.usenix.org/conference/osdi21/presentation/lai> "Oort: Efficient Federated Learning via Guided Participant Selection; OSDI").
- **FedBuff** - Buffers several asynchronous client updates before applying a server update. This reduces dependence on slow clients while allowing aggregated updates; buffer size, staleness and secure-aggregation protocol are distinct design choices. [Nguyen et al. 2022](<https://proceedings.mlr.press/v151/nguyen22b.html> "Federated Learning with Buffered Asynchronous Aggregation; AISTATS").

## Personalization and distributional objectives

- **MOCHA** - Learns related client-specific linear predictors with a multi-task regularizer. Its distributed optimizer accommodates variable local work and dropped updates; the convex task losses and learned task relationships distinguish it from shared-model FedAvg. [Smith et al. 2017](<https://arxiv.org/abs/1705.10467> "Federated Multi-Task Learning; NeurIPS").
- **Agnostic federated learning** - Optimizes performance against mixtures of client distributions rather than only their observed average. Mohri et al. derive bounds and convex optimization results; robustness is relative to the specified mixture family. [Mohri et al. 2019](<https://proceedings.mlr.press/v97/mohri19a.html> "Agnostic Federated Learning; ICML").
- **pFedMe** - Uses Moreau-envelope objectives to separate personalized optimization from global learning. Dinh et al. formulate a bilevel problem; a shared initialization and a personalized final model serve different objectives. [Dinh et al. 2020](<https://arxiv.org/abs/2006.08848> "Personalized Federated Learning with Moreau Envelopes; NeurIPS").
- **IFCA clustered federation** - Alternates client-to-cluster assignments with training one model per cluster. Convergence results assume suitable initialization and structured losses; neural experiments test a broader setting than the strongly convex theory. [Ghosh et al. 2020](<https://arxiv.org/abs/2006.04088> "An Efficient Framework for Clustered Federated Learning; NeurIPS").
- **FedBN** - Keeps batch-normalization components local while aggregating other model components. Li et al. target feature-distribution shifts across clients; local normalization is not a general solution to every form of non-IID data. [Li et al. 2021](<https://arxiv.org/abs/2102.07623> "FedBN: Federated Learning on Non-IID Features via Local Batch Normalization; ICLR").
- **Ditto** - Learns personalized models regularized toward a global model. Li et al. study fairness across devices and poisoning robustness; these depend on the client population and threat model used in evaluation. [Li et al. 2021](<https://proceedings.mlr.press/v139/li21h.html> "Ditto: Fair and Robust Federated Learning Through Personalization; ICML").

## Heterogeneous models and adapters

- **FedDF** - Distills client-model predictions on unlabeled server data into a central model. This permits different client architectures where weight averaging is undefined; the distillation data and server computation are additional resources. [Lin et al. 2020](<https://arxiv.org/abs/2006.07242> "Ensemble Distillation for Robust Model Fusion in Federated Learning; NeurIPS").
- **FLoRA** - Stacks low-rank adapter factors to aggregate their products, allowing different client ranks. Averaging the factors separately introduces cross-client terms; exact update aggregation here does not imply privacy or robustness to malicious clients. [Wang et al. 2024](<https://arxiv.org/abs/2409.05976> "FLoRA: Federated Fine-Tuning Large Language Models with Heterogeneous Low-Rank Adaptations; NeurIPS").

## Privacy mechanisms and integrity risks

- **Secure aggregation** - Bonawitz et al. let a server recover an aggregate without revealing individual client contributions under protocol assumptions. This protects individual updates; it does not itself limit information in the released aggregate or model. [Bonawitz et al. 2017](<https://research.google/pubs/practical-secure-aggregation-for-privacy-preserving-machine-learning/> "Practical Secure Aggregation for Privacy-Preserving Machine Learning; CCS").
- **User-level differential privacy** - McMahan et al. modify FedAvg with bounded client contributions, noise and privacy accounting. The protected unit is a user; record sampling and the privacy budget rather than labeling all federated training private. [McMahan et al. 2018](<https://arxiv.org/abs/1710.06963> "Learning Differentially Private Recurrent Language Models; ICLR").
- **Robust gradient aggregation** - Yin et al. analyze coordinate-wise medians and trimmed means against Byzantine workers. Guarantees assume independently sampled data from a common distribution; arbitrary non-IID client updates require additional analysis. [Yin et al. 2018](<https://proceedings.mlr.press/v80/yin18a.html> "Byzantine-Robust Distributed Learning: Towards Optimal Statistical Rates; ICML").
- **Gradient leakage** - Zhu et al. reconstruct inputs from shared gradients in studied vision and language settings. This demonstrates an attack surface; success depends on the information exposed and does not imply recovery from every aggregated update. [Zhu et al. 2019](<https://arxiv.org/abs/1906.08935> "Deep Leakage from Gradients; NeurIPS").
- **Model-replacement backdoors** - Bagdasaryan et al. show malicious clients can implant targeted behavior through submitted updates. Confidential aggregation and resistance to poisoning address different threats; one does not establish the other. [Bagdasaryan et al. 2020](<https://proceedings.mlr.press/v108/bagdasaryan20a.html> "How To Backdoor Federated Learning; AISTATS").

## Benchmarks and evaluation

- **LEAF** - Provides federated datasets, reference implementations and an evaluation framework emphasizing client heterogeneity. Real client partitions test different conditions from randomly dividing a centralized dataset. [Caldas et al. 2018](<https://arxiv.org/abs/1812.01097> "LEAF: A Benchmark for Federated Settings; arXiv").
- **FedScale** - Combines realistic client datasets with a runtime for system-aware FL evaluation. Lai et al. benchmark model and system performance together; communication rounds alone omit client speed and availability effects. [Lai et al. 2022](<https://proceedings.mlr.press/v162/lai22a.html> "FedScale: Benchmarking Model and System Performance of Federated Learning at Scale; ICML").
- **Motley personalization benchmark** - FedAvg plus fine-tuning has the best mean client accuracy on three of four cross-device datasets. Yet fine-tuning hurts 40% of clients on TedMulti-EnEs; average improvement and individual benefit are separate outcomes. [Wu et al. 2022](<https://arxiv.org/abs/2206.09262> "Motley: Benchmarking Heterogeneity and Personalization in Federated Learning; arXiv").

## Software

- **Flower** - Framework for federated experiments across simulated and heterogeneous real clients. Supports studying deployment differences; a simulation result does not measure performance on the intended device fleet. [Beutel et al. 2020](<https://arxiv.org/abs/2007.14390> "Flower: A Friendly Federated Learning Research Framework; arXiv").
- **TensorFlow Federated** - Provides federated computations and learning algorithms with simulation support. Client-data partitioning and aggregation are explicit components; privacy guarantees require an appropriate configured mechanism. [docs](<https://www.tensorflow.org/federated>).

## Related topics

- [Distributed learning](https://mlpapers.org/distributed-learning/)
- [Meta-learning](https://mlpapers.org/meta-learning/)
- [Multiview learning](https://mlpapers.org/multiview-learning/)
- [Optimization](https://mlpapers.org/optimization/)
- [Generalization](https://mlpapers.org/generalization/)
- [Evaluation](https://mlpapers.org/evaluation/)
