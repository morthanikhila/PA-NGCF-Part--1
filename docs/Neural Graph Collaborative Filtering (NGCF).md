## Neural Graph Collaborative Filtering (NGCF)

---

NGCF is a **graph-based recommendation model** that learns user and item embeddings by **propagating information through the user–item graph**.  
It was the first neural architecture to successfully use **high-order connectivity** (beyond direct neighbors) in collaborative filtering.

---

### 1. Why NGCF was introduced
Traditional models (MF, basic GCN-CF) have limitations:
- Learn only from **direct interactions**
- Cannot capture **multi-hop relationships**
- Cannot represent **complex preference patterns**

NGCF solves these by:
- Propagating embeddings across multiple graph layers
- Enriching embeddings with **non-linear neural transformations**
- Explicitly modeling **user–item–user high-order signals**

---

### 2. Core Design of NGCF
NGCF updates embeddings by combining 3 sources of information:

| Source | Meaning |
|--------|---------|
| Self-connection | Original user/item embedding |
| First-order neighbors | Direct interacted nodes |
| High-order neighbors | Neighbors of neighbors through multiple hops |

Mathematically:

new_embedding(u) = function(self + first_order_info + high_order_info)



---

### 3. Message Passing in NGCF
For every edge (u, i):
- User u sends messages to item i
- Item i sends messages to user u

Meaning:

U influences representation of I

I influences representation of U


After every propagation layer:
- Users become more aware of similar users via shared items
- Items become more aware of related items via shared users

Example:
- User A watched Movie X
- User B also watched Movie X
→ NGCF learns A and B are similar even without explicit connection


---

### 4. High-Order Connectivity
NGCF stacks multiple graph propagation layers.

| Layer depth | Captures |
|-------------|----------|
| 1-hop | Direct interactions (User → Item) |
| 2-hop | Shared neighbors (User → Item → User) |
| 3-hop | Abstract taste relations (User → Item → User → Item) |

Final embedding = sum of embeddings from all layers.

---

### 5. Non-Linear Embedding Transformation
NGCF applies MLP-style neural transformations after message passing.

Benefits:
- Learns **complex, non-linear preference patterns**
- More expressive than simple aggregation

---

### 6. Long-Range Dependency Example
Consider:

U1 → I2 → U5 → I9

U1 and I9 never interacted.  

NGCF still models their **latent connection** through the graph path.

Therefore NGCF becomes strong at:
- Discovering hidden interests
- Improving recommendation accuracy even with sparse data

---

### 7. Summary Table

| NGCF Feature | Purpose |
|--------------|---------|
| Graph structure | Models collaborative filtering as a graph |
| Message passing | Exchanges information between connected nodes |
| High-order propagation | Learns from multi-hop relations |
| Non-linear transformation | Captures complex preference signals |
| Layer-wise embedding concatenation | Preserves signals from each depth |

---

### 8. Strengths of NGCF

| Advantage | Impact |
|-----------|--------|
| Uses high-order connectivity | More accurate recommendations |
| Handles sparse data | Reduces cold-start and missing interactions |
| Neural architecture | More expressive than MF & GCN-CF |

---

### 9. Weakness (important for next topic)
NGCF **treats all neighbors equally** and does not know:
- Which neighbor is semantically close
- Which group/region of the graph the user belongs to

This leads to **information mixing**, especially when a user has **multiple taste clusters**.

This limitation directly motivates **PA-NGCF**, which fixes this issue using **position awareness**.

---
