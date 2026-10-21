# Federated Learning

## Data ownership, populations and objectives

- **[Federated setting](https://arxiv.org/abs/1912.04977)** — 2019. Clients train collaboratively while keeping raw training data decentralized. Kairouz et al. distinguish statistical, system and privacy challenges; retaining data locally does not prevent leakage through model updates.
- **[Cross-device versus cross-silo](https://arxiv.org/abs/1912.04977)**. Many intermittently available devices and a small set of participating organizations impose different participation, trust and resource constraints. State the deployment regime before comparing federated algorithms.
- **[Vertical federated learning](https://arxiv.org/abs/2211.12814)** — 2022. Parties hold different features for overlapping entities, rather than separate examples with a shared feature schema. Entity alignment, label ownership and intermediate-information leakage become central design questions.

## Global-model optimization under heterogeneity

- **[FedAvg](https://proceedings.mlr.press/v54/mcmahan17a.html)** — 2017. Selected clients train locally and the server averages their models, typically weighted by local example counts. More local work reduces synchronization frequency but can amplify differences between client objectives.
- **[FedProx](https://arxiv.org/abs/1812.06127)** — 2018. Adds a proximal penalty toward the current global model and permits variable local work. Li et al. analyze statistical and system heterogeneity; the penalty constrains local drift rather than making client data identical.
- **[SCAFFOLD](https://proceedings.mlr.press/v119/karimireddy20a.html)** — 2020. Uses control variates to correct client drift caused by heterogeneous local objectives. Karimireddy et al.’s convergence analysis distinguishes this correction from merely shortening each client’s local training.
- **[Adaptive federated optimization](https://arxiv.org/abs/2003.00295)** — 2020. FedAdagrad, FedAdam and FedYogi apply adaptive updates at the server while clients perform local optimization. Reddi et al. analyze nonconvex heterogeneous objectives; client and server learning rates play different roles.
- **[FedNova](https://arxiv.org/abs/2007.07481)** — 2020. Normalizes client updates to address objective inconsistency caused by unequal amounts of local computation. Its target is aggregation bias, distinct from feature shift or adversarial clients.

## Client participation and asynchronous updates

- **[Oort](https://www.usenix.org/conference/osdi21/presentation/lai)** — 2021. Selects training clients using estimated data utility and execution speed to improve time to accuracy. Its testing selector separately targets a requested data distribution; fast training participation and representative evaluation are different objectives.
- **[Power-of-Choice selection](https://arxiv.org/abs/2010.01243)** — 2020. Prefers clients with high local loss. Cho et al. analyze a tradeoff between convergence speed and solution bias; selection changes the effective optimization process, so comparisons must state the target client weights.
- **[FedBuff](https://proceedings.mlr.press/v151/nguyen22b.html)** — 2022. Buffers several asynchronous client updates before applying a server update. This reduces dependence on slow clients while allowing aggregated updates; buffer size, staleness and secure-aggregation protocol are distinct design choices.

## Personalization and distributional objectives

- **[FedBN](https://arxiv.org/abs/2102.07623)** — 2021. Keeps batch-normalization components local while aggregating other model components. Li et al. target feature-distribution shifts across clients; local normalization is not a general solution to every form of non-IID data.
- **[Ditto](https://proceedings.mlr.press/v139/li21h.html)** — 2021. Learns personalized models regularized toward a global model. Li et al. study fairness across devices and poisoning robustness; these depend on the client population and threat model used in evaluation.
- **[pFedMe](https://arxiv.org/abs/2006.08848)** — 2020. Uses Moreau-envelope objectives to separate personalized optimization from global learning. Dinh et al. formulate a bilevel problem; a shared initialization and a personalized final model serve different objectives.
- **[Agnostic federated learning](https://proceedings.mlr.press/v97/mohri19a.html)** — 2019. Optimizes performance against mixtures of client distributions rather than only their observed average. Mohri et al. derive bounds and convex optimization results; robustness is relative to the specified mixture family.
- **[MOCHA](https://arxiv.org/abs/1705.10467)** — 2017. Learns related client-specific linear predictors with a multi-task regularizer. Its distributed optimizer accommodates variable local work and dropped updates; the convex task losses and learned task relationships distinguish it from shared-model FedAvg.
- **[IFCA clustered federation](https://arxiv.org/abs/2006.04088)** — 2020. Alternates client-to-cluster assignments with training one model per cluster. Convergence results assume suitable initialization and structured losses; neural experiments test a broader setting than the strongly convex theory.

## Heterogeneous models and adapters

- **[FedDF](https://arxiv.org/abs/2006.07242)** — 2020. Distills client-model predictions on unlabeled server data into a central model. This permits different client architectures where weight averaging is undefined; the distillation data and server computation are additional resources.
- **[FLoRA](https://arxiv.org/abs/2409.05976)** — 2024. Stacks low-rank adapter factors to aggregate their products, allowing different client ranks. Averaging the factors separately introduces cross-client terms; exact update aggregation here does not imply privacy or robustness to malicious clients.

## Privacy mechanisms and integrity risks

- **[Secure aggregation](https://research.google/pubs/practical-secure-aggregation-for-privacy-preserving-machine-learning/)** — 2017. Bonawitz et al. let a server recover an aggregate without revealing individual client contributions under protocol assumptions. This protects individual updates; it does not itself limit information in the released aggregate or model.
- **[User-level differential privacy](https://arxiv.org/abs/1710.06963)** — 2017. McMahan et al. modify FedAvg with bounded client contributions, noise and privacy accounting. The protected unit is a user; record sampling and the privacy budget rather than labeling all federated training private.
- **[Gradient leakage](https://arxiv.org/abs/1906.08935)** — 2019. Zhu et al. reconstruct inputs from shared gradients in studied vision and language settings. This demonstrates an attack surface; success depends on the information exposed and does not imply recovery from every aggregated update.
- **[Model-replacement backdoors](https://proceedings.mlr.press/v108/bagdasaryan20a.html)** — 2020. Bagdasaryan et al. show malicious clients can implant targeted behavior through submitted updates. Confidential aggregation and resistance to poisoning address different threats; one does not establish the other.
- **[Robust gradient aggregation](https://proceedings.mlr.press/v80/yin18a.html)** — 2018. Yin et al. analyze coordinate-wise medians and trimmed means against Byzantine workers. Guarantees assume independently sampled data from a common distribution; arbitrary non-IID client updates require additional analysis.

## Benchmarks and evaluation

- **[LEAF](https://arxiv.org/abs/1812.01097)** — 2018. Provides federated datasets, reference implementations and an evaluation framework emphasizing client heterogeneity. Real client partitions test different conditions from randomly dividing a centralized dataset.
- **[FedScale](https://proceedings.mlr.press/v162/lai22a.html)** — 2022. Combines realistic client datasets with a runtime for system-aware FL evaluation. Lai et al. benchmark model and system performance together; communication rounds alone omit client speed and availability effects.
- **[Motley personalization benchmark](https://arxiv.org/abs/2206.09262)** — 2022. FedAvg plus fine-tuning has the best mean client accuracy on three of four cross-device datasets. Yet fine-tuning hurts 40% of clients on TedMulti-EnEs; average improvement and individual benefit are separate outcomes.
- **[Personalization evaluation](https://proceedings.mlr.press/v139/li21h.html)**. Separate participating clients with held-out examples from entirely new clients. Report local-only, global and personalized baselines, adaptation data and per-client performance; one pooled score can hide disparate outcomes.
- **[Systems and privacy reporting](https://proceedings.mlr.press/v162/lai22a.html)**. Specify client sampling, local steps, dropout, bytes, time and privacy assumptions. Compare at matched quality and label access; fewer rounds can conceal more client computation or a different privacy budget.

## Software

- **[Flower](https://arxiv.org/abs/2007.14390)** — 2020. Framework for federated experiments across simulated and heterogeneous real clients. Supports studying deployment differences; a simulation result does not measure performance on the intended device fleet.
- **[TensorFlow Federated](https://www.tensorflow.org/federated)**. Provides federated computations and learning algorithms with simulation support. Client-data partitioning and aggregation are explicit components; privacy guarantees require an appropriate configured mechanism.

## Related topics

[Distributed learning](https://mlpapers.org/distributed-learning/) · [Meta-learning](https://mlpapers.org/meta-learning/) · [Multiview learning](https://mlpapers.org/multiview-learning/) · [Optimization](https://mlpapers.org/optimization/) · [Generalization](https://mlpapers.org/generalization/) · [Evaluation](https://mlpapers.org/evaluation/).
