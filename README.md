# Epiplexity Selection

Model selection for reinforcement learning via [epiplexity](https://arxiv.org/abs/2601.03220) — a measure of the structural information a computationally-bounded learner extracts from data.

This repository implements an **Epiplexity Duel** RL training approach: two candidate models compete during each episode, and the one that learns more (higher epiplexity) is retained. This provides an automated, principled criterion for model selection in challenging RL benchmarks.

![Crafter Comparison](crafter_comparison_vid.gif)

## Environments

| Environment | Description | Source |
|---|---|---|
| [DeepMind Alchemy](https://github.com/google-deepmind/dm_alchemy) | Symbolic meta-RL benchmark ([Wang et al., 2021](https://arxiv.org/abs/2102.02926)) | `DeepmindAlchemy_A2C_EPN_Epiplexity_Public.ipynb` |
| [Crafter](https://github.com/danijar/crafter) | Procedurally-generated environment with 22 achievement tasks | `Crafter_Epiplexity_Selection.ipynb` |

## Method

1. Run two candidate models (A and B) in parallel on the environment
2. Compute epiplexity for each: `epiplexity = value_loss_before - value_loss_after` on a reference minibatch
3. Keep the model with higher epiplexity; discard the other
4. Repeat for thousands of episodes

### Usage

Both implementations are Jupyter notebooks designed for Google Colab or local environments. Open the relevant notebook, install dependencies, and run the `main(config)` function. Training progress is logged to TensorBoard.

## Base Models

The RL agent architectures are adapted from (but not identical to) the following codebases:

| Environment | Base | Notes |
|---|---|---|
| Alchemy | [BKHMSI/alchemist](https://github.com/BKHMSI/alchemist) | A2C with Episodic Proxy Network (transformer-based episodic memory) |
| Crafter | [snu-mllab/Achievement-Distillation](https://github.com/snu-mllab/Achievement-Distillation) | PPO with IMPALA-style ResNet; auxiliary achievement distillation loss is not used |

## References

- Finzi et al., "From Entropy to Epiplexity", 2026 — [arXiv:2601.03220](https://arxiv.org/abs/2601.03220)
- Wang et al., "Alchemy: A benchmark and analysis for meta-reinforcement learning agents", 2021 — [arXiv:2102.02926](https://arxiv.org/abs/2102.02926)
- Benchmarking the Spectrum of Agent Capabilities - [arXiv:2109.06780](https://arxiv.org/abs/2109.06780)
- Discovering Hierarchical Achievements in Reinforcement Learning via Contrastive Learning - [arXiv:2307.03486](https://arxiv.org/abs/2307.03486)
- How to Learn and Represent Abstractions: An Investigation using Symbolic Alchemy - [arXiv:2112.08360](https://arxiv.org/abs/2112.08360)