================================================================================
  Results Folder Contents Description
  (Benchmark Results for Truck-Drone Cooperative Delivery Optimization)
================================================================================

This folder contains computational experiment results organized by sections 
of the paper. The study focuses on truck-drone cooperative delivery using 
ALNS (Adaptive Large Neighborhood Search) and Gurobi solver, tested on 
Solomon benchmark instances (c101, c201, r101, rc101 variants).

================================================================================
  FOLDER STRUCTURE AND FILE DESCRIPTIONS
================================================================================

1. 6.2.1 Results on the Small-Scale Test Instances/
--------------------------------------------------------------------------------
   Comparison of ALNS heuristic vs. Gurobi exact solver on small instances.

   ALNS/
     Subfolders: 10/, 15/, 20/, 50/, 60/, 70/, 80/, 90/, 100/
       - Each contains CSV files (e.g., c101_10_result.csv) with ALNS results
       - Columns: Mean_Obj, Obj_std, Best_Obj, Mean_iter_num, Mean_same_num,
         Mean_insert_weight, Mean_remove_weight, Mean_init_obj, Mean_Time

   gurobi/
     Subfolders: 10/, 15/, 20/
       - Text files (e.g., result_C101_10.txt) with Gurobi exact solutions
       - Contains: best objective, best bound, optimality gap, variable values


2. 6.2.2 Results on the Large-Scale Test Instances/
--------------------------------------------------------------------------------
   ALNS results on large-scale instances (50-100 customers).

   Subfolders: 50/, 60/, 70/, 80/, 90/, 100/
     - CSV files per instance (e.g., c101_50_result.csv)
     - Same format as 6.2.1 ALNS results

   usual_heuristic_comparison.xlsx
     - Comparison of ALNS with other common heuristic methods


3. 6.2.3 Ablation Study on Coordination Mechanisms/
--------------------------------------------------------------------------------
   Evaluates the impact of removing specific coordination mechanisms.

   ALNS_constrained_results_small_12cases.xlsx
     - Sheet "Detailed Instance Comparison": Per-instance results comparing
       3 restricted models (sync-only, async-only, no-coordination) against 
       the full model
     - Sheet "Category Statistical Comparison": Aggregated statistics by 
       instance category (c101, c201, r101, rc101)
     - Key metrics: Mean/Best objective, Std Dev, Runtime, Best solution rate,
       Gap (%) between restricted and baseline models


4. 6.2.4 Demand Splitting Effect Validation/
--------------------------------------------------------------------------------
   Validates the benefit of allowing demand splitting across vehicles.

   result.xlsx
     - Sheet "Detailed Instance Comparison": Compares the non-split demand 
       model vs. the split-demand model per instance
     - Sheet "Category Statistical Comparison": Aggregated by instance 
       category with mean values
     - Key metrics: Mean/Best objective, Std Dev, Runtime, Best solution rate,
       Total service demand, System time, Gap (%) between models


5. 6.2.5 Validation of Objective Function Design/
--------------------------------------------------------------------------------
   Compares different denominator types in the objective function design.

   denominator_type_compare_10_15_20.xlsx
     - Sheet "Run-Level Result Records": Raw results per run for each 
       denominator type (Type 1: Sum of truck completion times, Type 2: 
       standard, Type 3: Fixed DK=600)
     - Columns: Instance, Customer count, Denominator type/name, Objective 
       value, Total demand, Resource consumption, Utilization rate, Per-truck 
       duration, Unbalanced utilization ratio, System completion time, 
       Iteration count, Initial objective, Runtime, Solution result
     - Sheet "Detailed Instance Comparison": Averaged results per instance
     - Sheet "Category Statistical Comparison": By instance category
     - Sheet "Category Instance Means": Summary means per category


6. 6.2.6 Solution Structure Analysis/
--------------------------------------------------------------------------------
   Analyzes the structure of solutions (coordination patterns, service splits).

   results_summary.xlsx
     - Sheet "detail": Per-instance analysis metrics
     - Columns: Mean truck/drone waiting time, Synchronous/Asynchronous 
       coordination counts, Customer split service ratio, Number of served 
       customers

   all_results/
     - Individual CSV files per instance and size (e.g., c101_10_result.csv 
       through c101_100_result.csv for all 4 instance types)
     - result_metrics_summary.xlsx: Aggregated metrics summary
     - data_collecting.py: Python script for processing raw results into 
       summary metrics (reads Solomon instance data, computes time matrices, 
       extracts route/sortie structures)

7. 6.2.7 Ablation Study of Core Algorithm Components/
--------------------------------------------------------------------------------
    Ablation study on ALNS algorithmic components.

    no_adaptive/
      - no_adaptive_n50_summary.csv, n70, n100: Results without adaptive 
        weight adjustment mechanism
    no_init/
      - no_init_all_sizes_summary.csv, n50, n70, n100: Results without 
        initialization heuristic
    no_sa/
      - no_sa_all_sizes_summary.csv, n50, n70, n100: Results without 
        simulated annealing acceptance criterion
    reduced_op/
      - reduced_op_all_sizes_summary.csv, n50, n70, n100: Results with 
        reduced set of neighborhood operators

    CSV columns: size, instance, baseline_best_obj_CALNS, Avg Obj, Gap(%), 
    Avg Convergence Iter, Avg Time(s), Best-of-3 Hit Count, best_obj

8. 6.3.1 Influence of Drone Capacity/
--------------------------------------------------------------------------------
   Sensitivity analysis on drone carrying capacity.

   drone_capacity_summary.xlsx
     - Sheet "detail": Results varying drone capacity parameter
     - Columns: Objective value, Total service demand, Total runtime, 
       Drone utilization rate, Mean sortie time, Improvement rate vs. initial


9. 6.3.2 Influence of Drone Endurance/
--------------------------------------------------------------------------------
   Sensitivity analysis on drone battery endurance (flight time limit).

   drone_endurance_summary.xlsx
     - Sheet "detail": Results varying drone endurance parameter
     - Columns: Drone endurance, Objective value, System runtime, 
       Improvement rate vs. initial solution


10. 6.3.3 Influence of Number of Drones per Truck/
--------------------------------------------------------------------------------
   Sensitivity analysis on the number of drones assigned to each truck.

   drone_num_summary.csv
     - Columns: instance, drone_num, Objective Value, optimal_obj, 
       Total Service Volume, Total Runtime, Drone Coverage Rate, 
       mean_sortie_time, sortie_count


11. 6.3.4 Influence of Launch/Retrieval Service Time/
--------------------------------------------------------------------------------
    Sensitivity analysis on drone launch and retrieval service durations.

    service_time_summary.xlsx
      - Sheet "detail": Results varying service time parameters
      - Columns: Objective value, Total service time, Drone utilization rate


12. 6.3.5 Influence of Number of Trucks/
--------------------------------------------------------------------------------
    Sensitivity analysis on the number of trucks in the fleet.

    truck_num_summary.xlsx
      - Sheet "detail": Results varying truck count
      - Columns: Objective value, Total service demand, Total time, 
        Drone utilization rate





