# Recommendation-System-Reinforcement-Learning

This repository contains a reproducible pipeline to train an Actor–Critic Reinforcement Learning agent for movie recommendation using Offline RL.

## Model architecture
A user’s interaction history is encoded with a GRU (128D). The Actor produces a candidate action vector (64D) that is mapped to real catalog items via Nearest-Neighbor retrieval (FAISS). The Critic evaluates state–action pairs to approximate long-term value. 

Training uses logged data only (no online exploration) and supports reward shaping for clicks, watch-time, or ratings.

We include off-policy evaluation (IPS/SNIPS/DR) and ranking metrics (NDCG@K, Recall@K), plus scripts for training, evaluation, and serving.

<p align="center"> <img src="assets/architecture.png" width="600" /> </p>
