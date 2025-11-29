# NGCF (Neural Graph Collaborative Filtering)

# 1.Why NGCF?
Traditional recommendation algorithms like:
- Matrix Factorization (MF)
- Neural Collaborative Filtering (NCF)

treat user interactions independently and fail to capture:
- Graph structure
- High-order connectivity
- Similarities propagated through neighbors

NGCF was proposed to use **Graph Neural Networks** for recommendation systems by modeling interaction data as a **user–item bipartite graph**.

Goal:
Learn better user and item embeddings using **graph message passing**.

---

## 2. Core Idea of NGCF
Each node (user or item) updates its embedding by **aggregating information from its neighbors**.

Example: 
- U1 → [I1, I3]
- I1 → [U1, U2]

NGCF updates embeddings like: 
- New(U1) = Combine(old(U1), Embeddings(I1), Embeddings(I3))
- New(I1) = Combine(old(I1), Embeddings(U1), Embeddings(U2))

This helps the model understand:
- User similarity via shared items
- Item similarity via shared users

---

## 3. Layer-wise Propagation in NGCF

At each GCN layer:
1. Node receives messages from neighbors
2. Node combines neighbor messages with its own embedding
3. Nonlinear activation adds expressiveness

Mathematically:
E^(l+1) = nonlinear( A * E^(l) * W_l )


Where:
- E = embeddings of all nodes
- A = normalized adjacency matrix
- W = learnable weight matrix

The model stacks multiple GCN layers to include:
- 1-hop neighbors
- 2-hop neighbors
- … higher-order connections

---

## 4. High-Order Connectivity Example
Graph chain:
U1 → I1 → U2 → I2

Even though U1 and I2 are not directly connected,
NGCF at layer-2 can learn their relationship.

This improves:
- Generalization
- Cold-start scenario handling
- Long-range preference detection

---

## 5. Embedding Combination
NGCF collects embeddings from multiple layers and concatenates them:
Final_Embedding = [E^0 | E^1 | E^2 | ...]

This aggregates signals from:
- Direct interactions
- Indirect/high-order relations

---

## 6. Loss Function
NGCF uses **Bayesian Personalized Ranking (BPR) loss**:

Objective:
For each user:
Positive items should rank higher than negative items.


Encourages model to recommend relevant items at top positions.

---

## 7. Benefits of NGCF
| Advantage | Explanation |
|----------|-------------|
| Uses graph structure fully | Learns connectivity patterns |
| High-order propagation | Better personalized recommendations |
| More expressive embeddings | Combines self and neighbors’ signals |

---

## 8. Limitations of NGCF
Even though NGCF improved recommendations, it still has weaknesses:

| Limitation | Problem |
|------------|---------|
| Only graph adjacency used | Cannot distinguish nodes at same hop but far in structure |
| All neighbors treated similarly | Important neighbors not prioritized |
| No notion of spatial position in graph | Loses geometric relationships |

Example:
Two items both 1-hop from U1:
U1
|
I1 I2


They may belong to completely different categories, but NGCF fails to capture this.

These issues motivate the next advancement:
**Position-aware NGCF (PA-NGCF)**.
