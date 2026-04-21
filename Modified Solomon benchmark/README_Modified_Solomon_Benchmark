================================================================================
  Solomon Benchmark Instances: Usage & Parameter Settings
================================================================================

Solver:  ALNS (heuristic) + Gurobi (exact, small-scale only)


================================================================================
  1. Instance Files (In/)
================================================================================

  c101.txt  — Clustered customers, narrow time windows
  c201.txt  — Clustered customers, wide time windows
  r101.txt  — Random customers, narrow time windows
  rc101.txt — Random-clustered customers, narrow time windows

Each file: 1 depot (node 0) + 100 customers (nodes 1–100).

File structure (110 lines):
  Lines 1–9:    Header (name, vehicle info, column labels)
  Lines 10–110: Node data

Columns: CUST_NO | XCOORD | YCOORD | DEMAND | READY_TIME | DUE_DATE | SERVICE_TIME

  Instance  Vehicles  Capacity  Depot TW      Svc Time
  c101      25        200       [0, 1236]     90
  c201      25        700       [0, 3390]     90
  r101      25        200       [0, 230]      10
  rc101     25        200       [0, 240]      10

NOTE: Only XCoord, YCoord, Demand are used. Time windows and service times
from the original Solomon data are NOT used — replaced by model parameters.


================================================================================
  2. Data Usage
================================================================================

Reading:
  pd.read_csv(file, delim_whitespace=True, skiprows=9,
              names=["Customer","XCoord","YCoord","Demand",
                     "ReadyTime","DueDate","ServiceTime"])

Scaling: First N+1 nodes selected (depot + N customers).
  Sizes tested: N = 10, 15, 20, 50, 60, 70, 80, 90, 100
  Depot duplicated at end as return depot.

Travel time computation (Euclidean, truncated to integer minutes):
  Truck: tij_k[i,j]  = int(dist(i,j) / 30 * 60)
  Drone: tij_kv[i,j] = int(dist(i,j) / 40 * 60)


================================================================================
  3. Model Parameters
================================================================================

  Parameter          Symbol   Value    Unit
  ─────────────────────────────────────────
  Truck speed        speed1   30       km/h
  Drone speed        speed2   40       km/h
  Truck service time TSK      3        min
  Drone service time TSD      3        min
  Drone launch time  LTD      2        min
  Drone retrieval    RTD      2        min
  Truck endurance    DK       600      min
  Drone endurance    DD       100      min
  Big-M              M        1000     —

Per-size parameters (from paper Table 6):
  Size   q (removal)   TQ   DQ   |K|  Drones/Truck
  10     [1,2]         40    5    2   {1,2},{1}
  15     [1,3]         90    8    2   {1,2,3}
  20     [2,3]         90    8    2   {1,2,3}
  50      5            90    8    2   {1,2,3}
  60      6            90    8    4   {1,2,3}
  70      7            90    8    4   {1,2,3}
  80      8            90    8    5   {1,2,3}
  90      9            90    8    5   {1,2,3}
  100    10            90    8    5   {1,2,3}

Objective function (maximize throughput efficiency):
  max Z = sum(d_i * served_i) / sum(T_k)
  Numerator:   total demand served (trucks + drones, split allowed)
  Denominator: sum of all truck completion times (NOT makespan)

