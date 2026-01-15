# TwitterGraphDataset

## Repository contents

This release provides a single archive, **`dataset.zip`**, containing **four files**.  
Each file is a **node-level table** with **community assignments** computed using the **Leiden** community detection algorithm (optimizing **CPM**) on a specific underlying graph.

### `dataset.zip` files

- **`rt_nodes_with_communities`**  
  Community assignments computed on the **retweet graph** (user–user interaction network).

- **`reply_nodes_with_communities`**  
  Community assignments computed on the **reply graph** (user–user interaction network).

- **`rt_and_hashtags_nodes_with_communities`**  
  Community assignments computed on the **retweet + hashtag graph**, a mixed network that includes:
  - the **retweet interaction network**, and
  - **user–hashtag links**, where hashtags are those **used in retweeted content**.

- **`reply_and_hashtags_nodes_with_communities`**  
  Community assignments computed on the **reply + hashtag graph**, a mixed network that includes:
  - the **reply interaction network**, and
  - **user–hashtag links**, where hashtags are those **used in replied-to content**.

> In the interaction-only graphs (`rt_nodes_with_communities`, `reply_nodes_with_communities`), nodes are **users only**.  
> In the mixed graphs (`rt_and_hashtags_nodes_with_communities`, `reply_and_hashtags_nodes_with_communities`), nodes include **users and hashtags**.

---

## File format

All four files share the same schema. Each row represents a node (user or hashtag, depending on the file).

Each file contains:
- **`id`**: a sequential identifier for each node  
- **`name`**: the unique identifier of the node  
- **`type`**: node type  
  - `u` = user node  
  - `h` = hashtag node  
- **`0.1, 0.2, …, 1.0`**: community assignments (community IDs) produced by **Leiden (CPM)** for different values of the **resolution** parameter

### Community assignment columns (Leiden + CPM)

For each resolution column:
- the value is an integer **community ID** assigned to that node at that resolution
- community IDs are **only meaningful within the same resolution** (e.g., community `3` at `0.2` is not necessarily related to community `3` at `0.8`)
