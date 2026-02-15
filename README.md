# 📚 Recommendation System with Deep Reinforcement Learning

A reproducible end-to-end pipeline that trains an **Actor–Critic** agent to recommend books — learning entirely from logged user interactions on the [GoodBooks-10k](https://github.com/zygmuntz/goodbooks-10k) dataset, with **no online exploration required**. 

User histories are encoded through a GRU network into dense embeddings, enabling the agent to capture sequential reading preferences and generate personalized recommendations evaluated with ranking metrics (NDCG@K, Recall@K) and off-policy estimators.

<p align="center">
  <img src="images/repo_overview.png" width="700" alt="Project Overview" />
</p>

## What about Offline Reinforcement Learning?

Is a Reinforcement Learning techinique to train an agent only from logged interaction data.

Instead of train the agent based of it's own interaction with the environment, the agent learns from a dataset of 
_(state, action, reward, next-state)_ tuples collected by a logging policy, aiming to maximize long-term return while staying within the support of the data.

How to get aprroximate online feedbacks if the agents training do not come from environment interaction?

We follow the approach proposed in https://arxiv.org/pdf/1801.00209.pdf by building an Online Simulator Memory which also
led us to evalute the recommender perfomance before applying online.

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
