# Offshore wind farm cable routing optimization project
- Optimized cable routing for large offshore wind farms with Mixed‑Integer Programming (MIP), using Gurobi.


$$ \min \qquad \sum_{(i, j) \in A} \sum_{t \in T} c_{i,\, j}^{t} \, x_{i,\, j}^t + \sum_{k \in V_{0}} a_{k} u_{k}$$

$$ \text{s.t.} \qquad \sum_{t \in T} x_{i,\, j}^{t} = y_{i,\, j}, \quad \forall (i, j) \in A $$
$$ \sum_{i \in V : i \ne h} \left( f_{h,\, i} - f_{i,\, h} \right) = P_{h}, \quad \forall h \in V_{T}  $$
$$\sum_{t \in T} k_t \ x_{i,\, j}^{t} \ge f_{i,\, j}, \quad \forall (i, j) \in A $$
$$\sum_{j \in V : j \ne h} y_{h,\, j} = 1, \quad \forall h \in V_{T} $$
$$\sum_{j \in V : j \ne h} y_{h,\, j} = 0, \quad \forall h \in V_{0}$$
$$\sum_{k \in V_{0}} u_{k} = 1$$
$$y_{i, j} \le u_j, \quad i \in V_T, \; j \in V_{0} $$
\notag \\[10pt] 
$$x_{i, j}^t \in \{0, 1 \}, \quad (i, j) \in A, \; t \in T$$
$$y_{i,\, j} \in \{0, 1 \}, \quad (i, j) \in A $$
$$f_{i,\, j} \ge 0, \quad (i, j) \in A  $$
$$u_{k} \in \{0, 1 \}, \quad k \in V_{0}  $$
$$a_k = 180 \times dist(k,\ onshore\_sub), \quad k \in V_{0} $$

