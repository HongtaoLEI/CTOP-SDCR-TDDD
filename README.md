To the best of our knowledge, there is no existing test instance directly applicable to the proposed CTOP-SDCR-TDDD problem. We thus generate test instances based on the well-known Solomon benchmark instances (Solomon, 1987), which are widely used in vehicle routing and truck-drone collaborative optimization studies. The instances are divided into small-scale and large-scale groups: for small-scale instances, we use both the Gurobi 12.0.0 MIP solver and the proposed CALNS heuristic for solution; for large-scale instances, we only adopt the CALNS heuristic considering the computational limitation of exact methods. The proposed heuristic is coded in Python 3.9, and all experiments are run on a computer with an Intel(R) Core(TM) i7-13600k CPU @ 5.1 GHz and 64 GB RAM.

To rigorously validate the performance of the proposed model and algorithm, we set up seven comparison dimensions in the experiments, as detailed below:

1. Exact solver validation: Gurobi 12.0.0 is used for small-scale instances, with metrics including MIP gap, upper bound (UB), and lower bound (LB) to verify the solution accuracy of the linearized model.

2. Classical metaheuristic baselines: Four widely used algorithms in the TOP and VRPD fields are selected for large-scale instances: Genetic Algorithm (GA), Ant Colony Optimization (ACO), standard Large Neighborhood Search (S-LNS), and Particle Swarm Optimization (PSO). All algorithms use the same iteration number, population size, and termination criteria for fair comparison.

3. Ablation study on coordination mechanisms: Three restricted models are constructed to quantify the value of each coordination mechanism:
    - Limit1: No drone coordination (demand splitting is prohibited, only single drone or truck independent delivery is allowed);
    - Limit2: Only same-truck drone coordination (cross-truck asynchronous coordination is prohibited);
    - Limit3: Only cross-truck drone coordination (same-truck drone synchronization/asynchronization coordination is prohibited).
    
4. Demand splitting effect validation: A restricted model without demand splitting is constructed to verify the effectiveness of the split delivery mechanism.

5. Solution structure analysis: The solution structure analysis is implemented on the absolute and interpretability indicators, including total served demand, truck/drone waiting time, synchronization service count, cross-truck coordination count, and split customer ratio.

6. Sensitivity analysis of core parameters: Single-factor sensitivity analysis is conducted on five core parameters (drone capacity, drone endurance, number of drones per truck, number of trucks, launch/retrieval service time) to verify the robustness of the model.

7. Objective function design validation: Three denominator settings are compared to verify the rationality of using the sum of truck completion times as the denominator: sum of truck completion times (original setting), makespan (maximum truck completion time), and fixed planning horizon.

8. Ablation study of core algorithm components: We conduct a comprehensive ablation study to quantify the incremental contribution of each customized component in the proposed CALNS algorithm, including the two-phase initial solution construction, problem-specific operators, adaptive operator selection mechanism, and simulated annealing acceptance criterion.
