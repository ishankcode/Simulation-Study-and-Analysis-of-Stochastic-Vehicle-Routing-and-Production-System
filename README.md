# Simulation-Study-and-Analysis-of-Stochastic-Vehicle-Routing-and-Production-System

Problems of Vehicle Routing are known in mathematics as NP hard. The time required to solve such problems is an exponential function of the number of locations and is a popular area of research in the industry.
In this study, attempt is made to solve one type of VRP known as Capacitated Vehicle Routing Problem (CVRP) in which a fleet of identical vehicles with limited capacity, located at a central depot must be optimally routed to supply a set of customers with known demands. 
The goal is to optimize the last mile delivery process by calculating optimum delivery routes and minimizing the transportation costs while ensuring minimum number of stockouts.
 
 ---

## <ins>Project is divided in 3 parts: </ins>
 
 ---
 
### <ins>PART1 : Data Preperation</ins>

1. Filtered out dataset to remove stores data outside Texas Region. Demand is aggregated weekly (Assumption : Products de;ivered weekly instead of daily).Fit various distributions to weekly data and identified Normal distibution as best fit with p-value of 0.9663. To imcrease size of dataset we used linearly Interpolated CDF to generate Random demand values based on historical dataset to increase size of dataset for 52 weeks.
2. Calculated the location of stores from Google maps. Generally Central Depot location is a very important decided based on various factor. For our project we calculated the Central depot location based on Centre of Gravity Method (Considered both location, and weekly demand pattern of each stores).  

![image](https://github.com/ishankcode/Simulation-Study-and-Analysis-of-Stochastic-Vehicle-Routing-and-Production-System/assets/66678343/d1ee6dbc-280f-4b49-9600-0710a297b706)
Red-Central Depot
Blue - Store Locations

 
 ---
 
 ### <ins>PART2 : Vehcile Routing Analsis</ins>
 
 1. Assumptions made: 
     - If additional trucks are needed to satisfy demand at any store in a route they will have tranverse through entire route
     - Paying fixed shortage cost to each store in case demand is unmet
 2. Deremined all properties of system as close to real world as possible.
 3. Used to Routing methods:
     - Savings Method : Heuristic method in which for each pair of nodes (stores), the savings in money spent if they are included in one route is calculated                (since less distance is travelled) by:  𝑆𝑖,𝑗=𝐶o,𝑖+𝐶o,𝑗− 𝐶𝑖,𝑗 where 𝐶𝑖,𝑗 is the cost of travelling from node i to node j
       Each pairing is ranked in terms of savings. Based on this rankings routes are calculated. <br />
       Although this method is very fast it's not very optimum.
       
     - Linear Programming: Used Gurobi solver in python to solve the routing problem. See the report attached for complete model description.
4. Python Experiments:
    - <ins>Trace Driven Simulation</ins>: <br />
      Finding Optimum Routes for Hoistorical Demand data.
    - <ins>Based on Savings Method</ins>: <br />
     - <ins>Based on New Data</ins>: <br />
      Finding Optimum Routes for New Demand data.
     But observed Large number of stores being Unsatisfied thats why in following models assigned priority levels to stores.
    - Next 3 scenarios are where top 20% of stores are assigned priority of 2,3 and 5 in the optimization model.
    - Further Next 3 scenarios are where top 30% of stores are assigned priority of 2,3 and 5 in the optimization model.
    By assigning priority means that if a store is assigned priority level of 5 then instead of 5 stores only 1 particular stores is added to route (Because of Truck capacity).<br />
    
    For each scenario the Operating cost and number of stores unsatisfied is calculated. Optimum route is decided based on trade off these 2 values.
    ![image](https://github.com/ishankcode/Simulation-Study-and-Analysis-of-Stochastic-Vehicle-Routing-and-Production-System/assets/66678343/72f101a2-af8c-4716-92f3-c733798dcc8b)
Used CRN (Common random Numbers) to identify best model because each week data is independant of each other.
![image](https://github.com/ishankcode/Simulation-Study-and-Analysis-of-Stochastic-Vehicle-Routing-and-Production-System/assets/66678343/c04007b0-59af-4fcd-9dc4-82e5c5d913b2)


5. Analyze the effect of various Uncontrollable factors (Meta Experiments) on the selected model from previous step:
   1. Hike in Fuel Price (increased by 66%)
   2. Demand to increase Worker salary (upto 35$/hr)
   3. Demand of parts doubled
   4. Higher stockout paymnet required
   5. Road block - routes need to be changed 
  
---

 ### <ins>PART3 : SIMIO</ins>
Simulation optimization is carried out to determine the most optimum value of parameters like vehicle capacity and pallet capacity resulting in the maximum expected value of throughput of system and minimum expected value of total transportation cost accrued.
The estimated optimal values turn out to be: throughput of 43,550 parts and transportation cost of 51,049.9 USD. The 95% confidence interval for throughput and cost is [39000, 45500] and [49710.61, 51490.52]


