# Offshore wind farm cable routing optimization project
- Optimized cable routing for large offshore wind farms with Mixed‑Integer Programming (MIP), using Gurobi.
- Considered 2 kinds of topology, "Branch topology" & "Balanced Radial topology"

## 1. Branched topology

### 1.1 MIP model
$$\min \qquad \sum_{(i, j) \in A} \sum_{t \in T} c_{i,\, j}^{t} \, x_{i,\, j}^t + \sum_{k \in V_{0}} a_{k} u_{k}$$ **(1)**

$$\text{s.t.} \qquad \sum_{t \in T} x_{i,\, j}^{t} = y_{i,\, j}, \quad \forall (i, j) \in A $$ **(2)**

$$\sum_{i \in V : i \ne h} \left( f_{h,\, i} - f_{i,\, h} \right) = P_{h}, \quad \forall h \in V_{T}  $$ **(3)**

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

### 1.2 Decision Variables
$x^t_{i,j}$: 1 if edge $(i, j)$ is connected with cable type $t$, 0 otherwise.  
$y_{i,j}$: $\sum_{t \in T} x^t_{i,j}$, a variable that indicates whether edge $(i, j)$ is connected regardless of cable type.  
$f_{i,j}$: Represents the energy flow from node $i$ to node $j$.  
$u_k$: A variable that indicates whether each of the 9 offshore substation candidates is selected. That is, if one substation is selected, its $u_k$ value is 1, otherwise 0  

### 1.3 Constraints  
(1): The objective function aims to minimize the cable cost.  
Here, $\sum_{(i,j) \in A} \sum_{t \in T} c^t_{i,j} x^t_{i,j}$ represents the cost between turbines and offshore substations, and $\sum_{k \in V_0} a_k u_k$ represents the cost between offshore substations and onshore substations.  
(2): Defines the $y_{i,j}$ variable and constrains that only one cable type can be selected.  
(3): A constraint ensuring that for each turbine, the difference between incoming flow and outgoing flow is preserved as 1. $(P_h = 1, \forall h \in V_T)$  
(4): A constraint ensuring that flow does not exceed the capacity of installed cables.  
(5): A constraint ensuring that the number of cables going out from one turbine is 1.  
(6): A constraint ensuring that there are no cables going out from substations.  
(7): A constraint ensuring that only one of the 9 substation candidates is selected.  
(8): A constraint ensuring that cables connecting from turbines to substations do not exceed $u_j, j \in V_0$.  
That is, if one of the 9 substation candidates is selected, only one cable enters that substation, and there are no cables entering other substation candidates.  


## 2. Balanced Radial
### 2.1 MIP model
$$\min \qquad \sum_{(i, j) \in A} \sum_{t \in T} c_{i,\, j}^{t} \, x_{i,\, j}^t + \sum_{k \in V_{0}} a_{k} u_{k}$$ **(1)**

$$\text{s.t.} \qquad \sum_{t \in T} x_{i,\, j}^{t} = y_{i,\, j}, \quad \forall (i, j) \in A$$ **(2)**

$$\sum_{i \in V : i \ne h} \left( f_{h,\, i} - f_{i,\, h} \right) = P_{h}, \quad \forall h \in V_{T}$$ **(3)**

$$\sum_{t \in T} k_t \ x_{i,\, j}^{t} \ge f_{i,\, j}, \quad \forall (i, j) \in A$$ **(4)**

$$\sum_{j \in V : j \ne h} y_{h,\, j} = 1, \quad \forall h \in V_{T}$$ **(5)**

$$\sum_{j \in V : j \ne h} y_{h,\, j} = 0, \quad \forall h \in V_{0}$$ **(6)**

$$\sum_{k \in V_{0}} u_{k} = 1$$ **(7)**

$$y_{i, j} \le u_j, \quad i \in V_T, \; j \in V_{0}$$ **(8)**

$$\sum_{i\in V} y_{i,\, h} = u_h s, \quad \forall h \in V_0$$ **(9)**

$$\sum_{i\in V:i\ne h} y_{i,\, h} \le 1, \quad \forall h \in V_T$$ **(10)**

$$f_{i,\, j} \le \left \lceil \frac{|V_T|}{s}\right \rceil, \quad \forall i, j \in V,\ i\ne j$$ **(11)**

$$x_{i, j}^t \in \{0, 1 \}, \quad (i, j) \in A, \; t \in T$$ **(12)**

$$y_{i,\, j} \in \{0, 1 \}, \quad (i, j) \in A$$ **(13)**

$$f_{i,\, j} \ge 0, \quad (i, j) \in A$$ **(14)**

$$u_{k} \in \{0, 1 \}, \quad k \in V_{0}$$ **(15)**

$$a_k = 180 \times dist(k,\ onshore\_sub), \quad k \in V_{0}$$ **(16)**

$$s = \text{(number of strings)}$$ **(17)**

### 2.2 Decision Variables
The decision variables are the same as in the Branched model.  

### 2.3 Constraints
(1) ~ (8) are the same as in the Branched model.  
(9): A constraint ensuring that $s$ cables enter the selected offshore substation candidate.  
(10): A constraint ensuring that the number of incoming cables to each turbine is at most 1.  
(11): A constraint ensuring that the flow from node $i$ to $j$ does not exceed $\lceil \frac{|V_T|}{s} \rceil$. Here, $\lceil \frac{|V_T|}{s} \rceil$ represents the number of turbines connected in one string.  
