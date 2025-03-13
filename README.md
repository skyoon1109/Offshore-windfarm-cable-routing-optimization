# Offshore wind farm cable routing optimization project
- Optimized cable routing for large offshore wind farms with Mixed‑Integer Programming (MIP), using Gurobi.

$$
    \min \qquad &\sum_{(i, j) \in A} \sum_{t \in T} c_{i,\, j}^{t} \, x_{i,\, j}^t + \sum_{k \in V_{0}} a_{k} u_{k} \tag{1}\\
    \text{s.t.} \qquad &\sum_{t \in T} x_{i,\, j}^{t} = y_{i,\, j}, \quad \forall (i, j) \in A \tag{2} \\
    & \sum_{i \in V : i \ne h} \left( f_{h,\, i} - f_{i,\, h} \right) = P_{h}, \quad \forall h \in V_{T} \tag{3} \\
    &\sum_{t \in T} k_t \ x_{i,\, j}^{t} \ge f_{i,\, j}, \quad \forall (i, j) \in A \tag{4} \\
    &\sum_{j \in V : j \ne h} y_{h,\, j} = 1, \quad \forall h \in V_{T} \tag{5} \\
    &\sum_{j \in V : j \ne h} y_{h,\, j} = 0, \quad \forall h \in V_{0} \tag{6} \\
    &\sum_{k \in V_{0}} u_{k} = 1 \tag{7} \\
    &y_{i, j} \le u_j, \quad i \in V_T, \; j \in V_{0} \tag{8} \\
    \notag \\[10pt] 
    &x_{i, j}^t \in \{0, 1 \}, \quad (i, j) \in A, \; t \in T \tag{9} \\
    &y_{i,\, j} \in \{0, 1 \}, \quad (i, j) \in A \tag{10} \\
    &f_{i,\, j} \ge 0, \quad (i, j) \in A \tag{11} \\
    &u_{k} \in \{0, 1 \}, \quad k \in V_{0} \tag{12} \\
    &a_k = 180 \times dist(k,\ onshore\_sub), \quad k \in V_{0} \tag{13}
$$
