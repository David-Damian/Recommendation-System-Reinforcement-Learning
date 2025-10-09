# Recommendation-System-Reinforcement-Learning

This repository contains a reproducible pipeline to train an Actor–Critic Reinforcement Learning agent for movie recommendation using Offline RL.

```markdown
# Offline RL
Is a Reinforcement Learning techinique to train an agent only from logged interaction data.

Instead of train the agent based of it's own interaction with the environment, the agent learns from a dataset of 
_(state, action, reward, next-state)_ tuples collected by a logging policy, aiming to maximize long-term return while staying within the support of the data.
```

```markdown
How to get aprroximate online feedbacks if the agents training do not come from environment interaction?

We follow the approach proposed in https://arxiv.org/pdf/1801.00209.pdf by building an Online Simulator Memory which also
led us to evalute the recommender perfomance before applying online.
```

## MDP definition

- State ($s$): user history of watched movies in chronological order N items.

- Action ($a$): the recommendation decision (single item or slate of K items)

- Reward ($r$): feedback signals (rating for the movie)

- Next state ($s$’): updated user history after exposure/outcome


## Model architecture
A user’s interaction history is encoded with a GRU (128D). The Actor produces a candidate action vector (64D) that is mapped to real catalog items via Nearest-Neighbor retrieval (FAISS). The Critic evaluates state–action pairs to approximate long-term value. 

Training uses logged data only (no online exploration) and supports reward shaping for clicks, watch-time, or ratings.

We include off-policy evaluation (IPS/SNIPS/DR) and ranking metrics (NDCG@K, Recall@K), plus scripts for training, evaluation, and serving.

<p align="center"> <img src="assets/architecture.png" width="600" /> </p>
