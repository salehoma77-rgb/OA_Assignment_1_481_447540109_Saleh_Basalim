# My Answers - Assignment 1 (CFLP: VNS vs Gurobi)

**Student Information:**
- **Student ID:** 447540109
- **Student Name:** Saleh Basalim
- **Gurobi Version Used:** [x] Academic [ ] Free
- **Date Completed:** November 5, 2026

---

## Section A: Solution Quality Analysis (4 marks)

### A.1 (2 marks) - Gap Analysis by Categories

**Analysis of Plot 01:**

Based on Plot 01 and the Excel results, the average optimality gap increases with problem size: 12.81% for Small, 14.18% for Medium, and 15.20% for Large instances. The Moderate difficulty category consistently has the highest average gap across all sizes, with 14.48%, 17.47%, and 18.82%, respectively. The Large–Easy category has the lowest average gap at 11.54%.

**Specific Observations:**
- Highest median gap size: Large (Moderate difficulty)
- Median gap value: Approximately 18%
- Effect of difficulty on gap: Moderate instances have the highest average gap (16.91%), followed by Expensive (13.56%) and Easy (11.87%).

**Outliers identified:**

The highest optimality gap was observed in instance 79 (Medium–Moderate), reaching 31.14%. Other unusually high gaps include instance 137 (Large–Expensive) at 26.33% and instance 32 (Small–Moderate) at 25.84%. These high-gap cases suggest that VNS may become trapped in local optima or fail to explore sufficiently diverse solutions. Facility capacity constraints and differences in cost structures may also contribute to these results.

**Interpretation:**

These patterns may occur because VNS is a heuristic algorithm that does not guarantee finding the optimal solution. As problem size and difficulty increase, the search space becomes more complex, making it harder to identify high-quality solutions. The algorithm may also become trapped in local optima when its neighborhood exploration is insufficient. Moderate instances showed higher average gaps, possibly because their facility costs and capacity constraints create more challenging combinations for the search process.

---

### A.2 (2 marks) - Overall Solution Quality Statistics

**From Excel File (Sheet "All Results"):**

- Total instances analyzed: 144
- Instances with gap < 5%: 4 (2.78%)
- Instances with gap < 10%: 26 (18.06%)
- Mean gap across all instances: 14.06%
- Standard deviation of gap: 4.77%

**Interpretation:**

The results show that VNS provides solutions with an average optimality gap of 14.06% and a standard deviation of 4.77%. Only 4 out of 144 instances (2.78%) achieved a gap below 5%, while 26 instances (18.06%) achieved a gap below 10%. This indicates that VNS has moderate variation in solution quality, but its solutions are generally not very close to the optimal results obtained by Gurobi.

Overall, VNS does not consistently provide near-optimal solutions. Although it can produce relatively good results for some instances, most solutions have noticeable gaps. Therefore, VNS may be useful when faster computation is preferred over optimal solution quality.

---

## Section B: Computational Efficiency Analysis (4 marks)

### B.1 (2 marks) - Time Comparison

**Analysis of Plot 02:**

**Size at which VNS becomes significantly faster:**

VNS becomes significantly faster than Gurobi for expensive instances, especially in the Small and Medium categories. For Small-Expensive instances, Gurobi takes an average of 47.06 seconds compared to 0.72 seconds for VNS. For Medium-Expensive instances, Gurobi takes 34.88 seconds compared to 0.67 seconds for VNS. This shows that VNS offers a substantial computational speed advantage for these configurations.

**Most challenging configurations:**
- For VNS: Large-Moderate (size-difficulty) with time: 0.80 seconds
- For Gurobi: Small-Expensive (size-difficulty) with time: 47.06 seconds

**Detailed Comparison:**

The results show that VNS generally requires less computation time than Gurobi, especially for expensive instances. For example, in Small-Expensive problems, Gurobi takes 47.06 seconds on average, while VNS takes only 0.72 seconds. This is because Gurobi searches for and verifies optimal solutions, whereas VNS uses a heuristic search approach to find feasible solutions more quickly. However, this speed advantage comes at the cost of solution quality, as VNS has an average optimality gap of 14.06%. Therefore, VNS is more suitable when fast solutions are needed, while Gurobi is preferable when optimality is the main priority.

---

### B.2 (2 marks) - Speedup Analysis

**Analysis of Plot 03:**

**Average speedup factors:**
- Small instances: 39.33x faster
- Medium instances: 18.98x faster
- Large instances: 5.96x faster

**Instances where Gurobi is faster (speedup < 1):**

Gurobi was faster than VNS in 15 out of 144 instances (10.42%). These cases were evenly distributed across problem sizes, with 5 Small, 5 Medium, and 5 Large instances. Most of them (14 instances) belonged to the Easy difficulty category, while only one was Moderate. No Expensive instances were observed. This suggests that Gurobi can outperform VNS on relatively easy problems, where the exact solver can find the optimal solution quickly without requiring extensive computation.

**Practical Implications:**

The speedup results demonstrate that VNS can be useful in real-world applications where quick decisions are important. On average, VNS achieved speedup factors of 39.33× for Small instances, 18.98× for Medium instances, and 5.96× for Large instances. This makes VNS suitable for situations requiring frequent or time-sensitive facility location decisions. However, the average optimality gap of 14.06% indicates a trade-off between computational speed and solution quality. Therefore, VNS is preferable when obtaining a feasible solution quickly is more important, while Gurobi is more appropriate when minimizing total cost and achieving optimality are the main priorities.

---

## Section C: Scalability Analysis (3 marks)

### C.1 (1.5 marks) - Scalability Behavior

**Analysis of Plot 04:**

**VNS Scalability:**

VNS demonstrates relatively stable computational performance as problem size increases. The computation time generally increases slightly for larger instances, but most execution times remain below approximately 1 second. Unlike Gurobi, VNS does not show large increases in runtime for more complex instances. This suggests that VNS scales relatively well and is suitable for solving larger facility location problems when fast computation is required.

**Gurobi Scalability:**

Gurobi shows greater variability in computation time as problem size increases. Although it solves many instances quickly, its runtime can increase significantly for more challenging problems, with some instances requiring more than 100 seconds. This occurs because Gurobi uses an exact optimization approach to find and verify optimal solutions. As the problem becomes more complex, the computational effort required may increase substantially. Therefore, Gurobi generally exhibits less predictable runtime performance than VNS, particularly for difficult instances.

**Comparison:**

VNS demonstrates better runtime scalability than Gurobi in the tested instances. Its computation time remains relatively stable as problem size increases, while Gurobi shows greater variability and occasionally requires substantially longer execution times. This is because VNS uses a heuristic search strategy, whereas Gurobi must find and verify optimal solutions. Therefore, VNS is more suitable for larger or time-sensitive facility location problems when fast computation is the priority. However, Gurobi remains preferable when obtaining an optimal solution is more important than execution speed.

---

### C.2 (1.5 marks) - Growth Rate and Predictions

**Observed Growth of Average Runtime (from your results):**

| Algorithm | Small | Medium | Large | Small -> Medium (x) | Medium -> Large (x) |
|---|---:|---:|---:|---:|---:|
| VNS avg time (s) | 0.45 | 0.45 | 0.67 | 1.00 | 1.49 |
| Gurobi avg time (s) | 17.13 | 12.54 | 2.65 | 0.73 | 0.21 |

**Shape of growth in Plot 04:**
- VNS: [X] Roughly steady [ ] Steadily increasing [ ] Sharply increasing
- Gurobi: [X] Roughly steady [ ] Steadily increasing [ ] Sharply increasing

**Justification:**

The results show that VNS has relatively stable computation times as problem size increases. Its average runtime remains 0.45 seconds for both Small and Medium instances and increases to 0.67 seconds for Large instances, representing a growth factor of 1.49. In contrast, Gurobi's average runtime decreases from 17.13 seconds for Small instances to 12.54 seconds for Medium instances and 2.65 seconds for Large instances. Therefore, the observed averages do not show increasing runtime for Gurobi, although Plot 04 reveals substantial variability and some very long execution times. These results suggest that runtime depends on problem difficulty as well as size.

**Rough Prediction for Extra Large Instance (n=50, m=20):**
- Predicted VNS time: 1.00 seconds
- Predicted Gurobi time: 0.56 seconds
- How I computed it: I multiplied the Large-instance average runtime by the Medium-to-Large growth ratio again (VNS: 0.67 × 1.49 ≈ 1.00; Gurobi: 2.65 × 0.21 ≈ 0.56).
**Suitability for Very Large Instances:**

Yes, I would recommend VNS for very large facility location problems when computational speed is more important than obtaining the exact optimal solution. The experimental results show that VNS maintains relatively stable execution times, averaging 0.67 seconds for Large instances, compared with 2.65 seconds for Gurobi. However, VNS has an average optimality gap of 14.06%, meaning that its solutions are generally more expensive than the optimal solutions. Therefore, VNS is suitable for time-sensitive applications where approximate solutions are acceptable, while Gurobi is preferable when minimizing cost and guaranteeing optimality are the main priorities. Performance on very large instances should still be validated through additional experiments.

---

## Section D: Quality-Time Tradeoff Analysis (3 marks)

### D.1 (1.5 marks) - Sweet Spot Identification

**Analysis of Plot 05:**

**Sweet Spot:**

Based on Plot 05, a reasonable sweet spot is where VNS achieves an optimality gap of approximately 5–10% with a computation time below 1 second. This region provides relatively high-quality solutions while maintaining fast execution. However, many VNS solutions have larger gaps, indicating that the algorithm does not consistently achieve this balance. Therefore, this sweet spot represents a desirable practical trade-off rather than a guaranteed outcome.

**Time Savings for High-Quality Solutions (gap < 5%):**
- Average VNS time: 0.34060 seconds
- Average Gurobi time: 0.18616 seconds
- Absolute savings: -0.15444 seconds
- Relative savings: -82.96%

**Interpretation:**

For high-quality solutions with an optimality gap below 5%, Gurobi was faster than VNS in the four observed instances. VNS required an average of 0.34060 seconds, compared with 0.18616 seconds for Gurobi, resulting in negative time savings of 82.96%. This indicates that VNS does not always provide a computational advantage, particularly for relatively easy instances where Gurobi can quickly find the optimal solution. Practitioners should therefore consider both solution quality and execution time when selecting an optimization algorithm.

---

### D.2 (1.5 marks) - Practical Decision Making

**Scenarios Justifying 10-15% Gap:**

1. Time-Critical Delivery Planning: In a logistics company, delivery routes may need to be updated immediately due to traffic congestion or unexpected customer requests. In such situations, accepting a 10–15% higher transportation cost can be justified if VNS provides a feasible solution much faster than Gurobi, allowing deliveries to continue without significant delays.

2. Emergency Facility Relocation: When a logistics company must quickly relocate a distribution facility because of an unexpected disruption, such as flooding or a warehouse closure, rapid decision-making becomes essential. Accepting a 10–15% higher operating cost may be reasonable if VNS finds a feasible facility location significantly faster than Gurobi, helping the company restore operations and minimize service interruptions.

3. Rapid Evaluation of Multiple Facility Locations: A logistics company may need to evaluate several potential warehouse locations under different demand scenarios. Accepting a 10–15% higher operating cost can be justified when VNS generates feasible solutions quickly, allowing managers to compare alternatives and respond to changing business conditions. This is particularly useful when decisions must be made frequently and obtaining an exact optimal solution is less important than timely planning.

**Recommendation for Real-World Logistics Company:**

For a real-world logistics company, I recommend using a hybrid approach that combines VNS and Gurobi depending on the situation. VNS is suitable for time-sensitive decisions and larger or more difficult instances because it generally provides feasible solutions quickly. In our experiments, VNS achieved an average speedup of 19.88× for Medium instances, although its average optimality gap was 14.06%. However, Gurobi is preferable for strategic decisions such as establishing permanent distribution centers, where minimizing long-term operating costs and obtaining an optimal solution are more important. Gurobi was also faster in some easy instances. Therefore, the company should use VNS for rapid operational planning and Gurobi for critical long-term investment decisions, considering the required solution quality, available computation time, and problem complexity.

---

## Section E: Algorithm Understanding (3 marks)

### E.1 (1.5 marks) - VNS Neighborhood Structures

**Role of Each Neighborhood:**

**N1 (Open Facility):**
- Purpose: To open a new facility and explore whether assigning customers to it reduces the total cost.
- Contribution: [ ] Intensification [X] Diversification
- Explanation: Opening a previously closed facility changes the current facility configuration and allows VNS to explore new regions of the solution space. Although it may increase fixed opening costs, it can reduce transportation costs by serving customers from a more suitable location.

**N2 (Close Facility):**
- Purpose: To close an existing facility and determine whether reallocating its customers to other open facilities reduces the total cost.
- Contribution: [ ] Intensification [X] Diversification
- Explanation: Closing an open facility changes the facility configuration and encourages exploration of alternative solutions. It reduces fixed opening costs, but customers must be reassigned to other facilities, which may increase transportation costs. This neighborhood helps VNS discover configurations with a lower total cost.

**N3 (Swap Facilities):**
- Purpose: To close one currently open facility and open another closed facility simultaneously, searching for a better facility configuration.
- Contribution: [ ] Intensification [X] Diversification
- Explanation: Swapping facilities allows VNS to explore different combinations of open facilities without necessarily changing their total number. This can help escape local optima by replacing a poorly located facility with a more suitable one, potentially reducing transportation and overall operating costs.

**N4 (Reassign Clients):**
- Purpose: To reassign clients among currently open facilities to reduce transportation costs without changing which facilities are open.
- Contribution: [X] Intensification [ ] Diversification
- Explanation: Reassigning clients improves the current solution by optimizing customer allocations while keeping the facility configuration unchanged. This neighborhood focuses on finding lower-cost assignments within the existing solution structure, making it an intensification strategy.

**How They Complement Each Other:**

These four neighborhoods complement each other by balancing diversification and intensification. N1 (Open Facility), N2 (Close Facility), and N3 (Swap Facilities) explore different facility configurations and help VNS escape local optima. In contrast, N4 (Reassign Clients) focuses on improving customer assignments within the current facility configuration. By alternating between these neighborhoods, VNS can explore new regions of the solution space and refine promising solutions, increasing the chance of finding lower-cost solutions.

---

### E.2 (1.5 marks) - Convergence Behavior Analysis

**Selected Convergence Plots:**

**Plot 1:** [Instance name: fac20cli68]
- Pattern: [X] Smooth [ ] Multiple jumps
- Description: The VNS convergence curve remains nearly flat throughout 100 iterations, with no significant improvement in the solution cost. The final optimality gap is 10.5%.
- What it reveals: VNS appears to stagnate at a local optimum and is unable to close the gap with the Gurobi optimal solution. This suggests that the neighborhood search did not find a better solution during the observed iterations.

**Plot 2:** [Instance name: fac25cli66]
- Pattern: [X] Smooth [ ] Multiple jumps
- Description: The VNS convergence curve remains almost flat across 100 iterations, showing no noticeable reduction in the solution cost. The final optimality gap is 14.5%.
- What it reveals: VNS shows limited improvement and remains above the Gurobi optimal solution. This indicates that the search may have stagnated in a local optimum and was unable to discover a better facility configuration.

**Plot 3:** [Instance name: fac27cli67]
- Pattern: [ ] Smooth [X] Multiple jumps
- Description: The VNS convergence curve shows a noticeable downward step around iteration 7, followed by a relatively stable solution cost. The final optimality gap is 10.8%.
- What it reveals: The downward step indicates that VNS discovered an improved solution during the search. However, the algorithm subsequently stagnated above the Gurobi optimal cost, showing that improvements do not necessarily guarantee convergence to the global optimum.

**Role of Shaking Mechanism:**

The shaking mechanism helps VNS escape local optima by introducing random changes to the current solution, allowing the algorithm to explore different regions of the search space. In Plot 3 (fac27cli67), the downward step around iteration 7 shows that VNS found a better solution after a period of limited improvement. This is consistent with the potential benefit of shaking, although the plot alone does not prove that shaking directly caused the improvement. In contrast, Plots 1 and 2 remain almost flat, indicating that shaking does not always lead to better solutions. Therefore, shaking supports diversification and helps reduce the risk of stagnation, but it does not guarantee reaching the global optimum.

---

## Section F: Critical Reflection (3 marks)

### F.1 (1 mark) - Limitations and Improvements

**Main Limitations of Current VNS Implementation:**

1. Limited Improvement and Stagnation: Several convergence plots show nearly flat curves, indicating that VNS often fails to improve its initial solution and may become trapped in local optima.

2. Sensitivity to Parameter Settings: The performance of VNS depends on parameters such as the number of iterations, shaking strength, and neighborhood selection, which may not be equally effective across different instance sizes and difficulty levels.

3. No Guarantee of Optimality: VNS is a heuristic algorithm and cannot guarantee finding the global optimum. The experimental results show noticeable optimality gaps compared with Gurobi, including gaps above 10% in several instances.

**Suggested Improvements:**

1. Adaptive Neighborhood Selection: Adjust the neighborhood selection and shaking strength based on search progress. This could help VNS escape stagnation and improve solution quality when the current neighborhoods fail to find better solutions.

2. Improved Initial Solution: Use a stronger greedy construction method or a Gurobi-based initial feasible solution to provide VNS with a better starting point. This could reduce the optimality gap and the number of iterations needed to obtain high-quality solutions.

3. Hybrid VNS with Exact Optimization: Combine VNS with Gurobi by using VNS to generate feasible solutions and Gurobi to refine promising solutions when computational time permits. This could improve solution quality while maintaining flexibility for larger or more difficult instances.

---

### F.2 (1 mark) - Real-World Deployment Considerations

**Additional Constraints for Real Logistics Company:**

1. Facility Capacity Constraints: Each warehouse has a maximum storage and handling capacity. Customer demand assigned to a facility must not exceed this capacity. This is important to prevent overcrowding and ensure that all orders can be processed efficiently.

2. Delivery Time and Service Level Constraints: Customers may require deliveries within specific time windows, and transportation routes must meet agreed service levels. These constraints are important because minimizing cost alone does not guarantee timely deliveries or customer satisfaction.

3. Workforce and Operational Constraints: Opening or closing a facility depends on staff availability, operating hours, and available equipment. These constraints matter because a mathematically feasible facility configuration may not be practical if sufficient personnel or resources are unavailable.

**Additional Objectives:**

In addition to minimizing total operating and transportation costs, a real-world logistics company should consider multiple objectives, including minimizing delivery times, maximizing customer satisfaction, improving service reliability, and reducing environmental impact. These objectives may conflict with cost minimization because faster deliveries or higher service quality can require additional resources. Therefore, a multi-objective optimization approach could help the company balance operational costs, delivery performance, and sustainability according to its business priorities.

---

### F.3 (1 mark) - Exact Method vs Heuristic in Practice

**Gurobi Optimality Status (from the `gurobi_status` column):**
- Instances solved to proven optimality: 144 out of 144
- Instances stopped at the time limit: 0 out of 144
- Do the time-limit instances share a size/difficulty? No instances reached the time limit, so there is no size or difficulty pattern to analyze.
**What VNS Gives Up and What It Gains:**

Across the 144 tested instances, VNS achieved an average optimality gap of 14.061% compared with Gurobi, while saving an average of 10.2494 seconds per instance. This demonstrates the trade-off between solution quality and computational efficiency. VNS sacrifices the guarantee of finding the global optimum and produces solutions with higher costs, but it reduces computational time. In contrast, Gurobi found proven optimal solutions for all 144 instances. Therefore, VNS can be useful when fast, reasonably good solutions are more important than guaranteed optimality.

**Practical Value of Heuristics:**

In real-world logistics and facility location problems, VNS-like heuristic algorithms are valuable because they can provide feasible solutions within a shorter computational time, especially when decisions must be made quickly. In this experiment, VNS saved an average of 10.2494 seconds per instance compared with Gurobi, although its solutions had an average optimality gap of 14.061%. This makes VNS useful for rapid planning, evaluating alternative facility configurations, and responding to changing customer demands. However, when guaranteed optimal solutions are required and sufficient computational resources are available, exact optimization methods such as Gurobi may be preferable. Therefore, the choice between VNS and Gurobi depends on the balance between solution quality, computational time, and practical business requirements.

---

## Section G: BONUS - VNS Improvement Challenge (+3 marks, optional)

*Leave this section empty if you do not attempt the bonus. See Section 8 of the guide. Your improved notebook (`StudentID_FirstName_LastName_Assignment1_IMPROVED.ipynb`) must be pushed to your repository.*


### G.1 (1 mark) - Bug Identification

**Where is the bug?**

The issue is located in Cell 11 of `Assignment_1.ipynb`, within the `n2_close_open_facility()` function.

The original implementation contains these operations:

```python
neighbor_facility_opened[j_open] = 0
neighbor_facility_opened[j_close] = 1
```

**What does the bug do?**

The N2 neighborhood is supposed to close an existing facility. However, the original code closes one facility while opening another. This produces a facility swap instead of a pure closing operation, making N2 overlap with the N3 neighborhood.

**Why does it degrade VNS performance?**

This behavior limits the diversity of neighborhood moves because VNS repeatedly explores similar facility configurations. It also prevents N2 from directly testing whether reducing the number of open facilities could lower fixed operating costs. Consequently, some potentially better solutions may remain unexplored. In the original results, 16 of the 144 instances had optimality gaps above 20%, showing that VNS struggled to approach the optimal cost in several cases.

---

### G.2 (1 mark) - The Fix

**Corrected code:**

```python
# Close an open facility without opening a replacement
neighbor_facility_opened = facility_opened.copy()
neighbor_facility_opened[j_open] = 0

# Reallocate clients to facilities that remain open
neighbor_client_assignments = assign_clients_to_nearest_open_facility(
    service_costs,
    neighbor_facility_opened,
    facility_capacities,
    client_demands
)

# Retain only solutions satisfying the capacity constraints
if is_feasible(
    neighbor_facility_opened,
    neighbor_client_assignments,
    facility_capacities,
    client_demands
):
    neighbors.append(
        (neighbor_facility_opened, neighbor_client_assignments)
    )
```

**Why does the fix work and why does it not break the rest of the algorithm?**

The revised N2 operation closes one facility without automatically replacing it. This allows VNS to evaluate configurations with fewer operating facilities and potentially lower fixed costs. After the closure, clients are reassigned and feasibility is checked before the candidate is accepted into the neighborhood.

The correction preserves the original solution format and function interface. It also keeps the responsibilities of N2 and N3 distinct: N2 investigates facility closures, while N3 explores facility swaps. The other neighborhood operations can therefore continue functioning without changes to the overall search structure.


---

### G.3 (1 mark) - Demonstrated Improvement

**Before vs After (same instances):**

| Metric | Original VNS | Improved VNS |
|---|---:|---:|
| Mean gap (%) | 14.061 | 11.447 |
| Std of gap (%) | 4.772 | 4.848 |
| Instances with gap < 5% | 4 | 5 |
| Instances with gap > 20% | 16 | 10 |
| Mean VNS time (s) | 0.522 | 1.317 |

**Analysis:**

Both versions were evaluated on the same set of 144 CFLP instances. The improved implementation reduced the average optimality gap from 14.061% to 11.447%, representing a reduction of approximately 18.6% relative to the original gap. In addition, the number of instances with gaps exceeding 20% decreased from 16 to 10, indicating better performance on several challenging cases.

However, this improvement came with additional computational effort. The average VNS execution time increased from 0.522 to 1.317 seconds per instance. The standard deviation of the gap also increased slightly, from 4.772% to 4.848%. Therefore, the experimental results show an improvement in average solution quality, but not in execution speed or consistency across every instance.

**Improved results files (names in your repository):**

- `BONUS_IMPROVED_447540109/results_student_447540109.csv`
- `BONUS_IMPROVED_447540109/results_student_447540109.xlsx`
- `BONUS_IMPROVED_447540109/report_summary_student_447540109.txt`
---

## Additional Comments (Optional)

[Any additional observations, challenges faced, or insights gained]

---

## Declaration

I hereby declare that:
- I have completed this assignment independently
- All numerical results are from MY experiments using MY student ID
- All analysis and interpretations are MY own work
- I have not copied results or answers from other students
- I understand the consequences of academic dishonesty

**Signature:** _______________________

**Date:** ___________________________

---

**END OF MY ANSWERS**
