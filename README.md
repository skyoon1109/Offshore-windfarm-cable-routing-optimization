# Offshore wind farm cable routing optimization project
- Optimized cable routing for large offshore wind farms with Mixed‑Integer Programming (MIP), using Gurobi.
- Considered 2 kinds of topology, "Branch topology" & "Balanced Radial topology"

## Branched topology
$$\min \qquad \sum_{(i, j) \in A} \sum_{t \in T} c_{i,\, j}^{t} \, x_{i,\, j}^t + \sum_{k \in V_{0}} a_{k} u_{k}$$ **(1)**

$$ \text{s.t.} \qquad \sum_{t \in T} x_{i,\, j}^{t} = y_{i,\, j}, \quad \forall (i, j) \in A $$ **(2)**

$$ \sum_{i \in V : i \ne h} \left( f_{h,\, i} - f_{i,\, h} \right) = P_{h}, \quad \forall h \in V_{T}  $$ **(3)**

$$\sum_{t \in T} k_t \ x_{i,\, j}^{t} \ge f_{i,\, j}, \quad \forall (i, j) \in A $$ **(4)**

$$\sum_{j \in V : j \ne h} y_{h,\, j} = 1, \quad \forall h \in V_{T} $$ **(5)**

$$\sum_{j \in V : j \ne h} y_{h,\, j} = 0, \quad \forall h \in V_{0}$$ **(6)**

$$\sum_{k \in V_{0}} u_{k} = 1$$ **(7)**

$$y_{i, j} \le u_j, \quad i \in V_T, \; j \in V_{0} $$ **(8)**


$$x_{i, j}^t \in \{0, 1 \}, \quad (i, j) \in A, \; t \in T$$ **(9)**

$$y_{i,\, j} \in \{0, 1 \}, \quad (i, j) \in A $$ **(10)**

$$f_{i,\, j} \ge 0, \quad (i, j) \in A  $$ **(11)**

$$u_{k} \in \{0, 1 \}, \quad k \in V_{0}  $$ **(12)**

$$a_k = 180 \times dist(k,\ onshore\_sub), \quad k \in V_{0} $$ **(13)**


## Balanced Radial
