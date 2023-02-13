In this project, we compare the implementations of an exact model and a few heuristic methods used to solve a capacitated vehicle routing problem.

The initial problem, proposed by the company <a href="http://www.optimerotas.com.br">OpTime</a> as part of the Fall semester class _Resolução de Problemas via Modelagem Matemática_ (Resolution of problems via mathematical modeling, <a href="https://www.unifesp.br/campus/sjc/">Unifesp</a>), was to implement methods for solving a Traveling Salesperson Problem together with a 3D-bin Packing Problem.  Our approach was to model this problem as a Capacitated Vehicle Routing Problem and compare heuristics with exact methods.  This is a joint work with [Davi Alves](https://github.com/davi-juliano/) and [Roberval Filho](https://github.com/roberval1994), supervised by Prof. Luiz Leduíno Neto and Prof. Horácio Yanasse (Unifesp). 

The results of this project were published in the annals of the LIV meeting of the Brazilian Operations Research Society as <a href="http://proceedings.science/sbpo/sbpo-2022/trabalhos/otimizacao-do-transporte-heterogeneo-de-cargas-modelagem-e-meta-heuristica">Otimização do Transporte Heterogêneo de Cargas - Modelagem e Meta-Heurística</a>.


## Model and heuristics

Given a set of points in the globe, a set of items that should be delivered to these points, and a set of vehicles that are able to deliver these items, our goal is to establish the route of each one of these vehicles such that the total cost of delivery is minimal.  Here the cost only accounts for the fuel that the vehicles use.

In order to obtain these optimal routes, we replace the condition that the items fit inside of the vehicle (the 3D-bin packing part) by the condition that the sums of the volumes and the weights of the items that are transported by a vehicle are smaller than the capacity of this vehicle.  We thus supplement the Miller-Tucker-Zemlin formulation of the Traveler Salesperson Problem with these two extra restrictions. 


## Files

The file `Data for capacitated vehicle routing problem.xlsx` contains the instances provided by the company OpTime.  The file `Exact model with Gurobi.ipynb` contains a Python implementation of the exact model, using the [`gurobipy`](https://pypi.org/project/gurobipy/) library.  The file `Heuristics and meta-heuristics.ipynb` contains Python implementations of a few heuristic methods, namely:
 * a meta-heuristic which constructs an initial route using the nearest-neighbor heuristic, then applies the Christofides-Serdyukov heuristic, and ends with a Simulated Annealing heuristic that uses 2-opt and swap as local searches;
 * a meta-heuristic which constructs an initial route using a randomized greedy constructive heuristic, then applies a Variable Neighborhood Descent that also uses 2-opt and swap as local searches;
 * a meta-heuristic which constructs an initial route using the nearest-neighbor heuristic, then applies the Christofides-Serdyukov heuristic, and ends with a Variable Neighborhood Descent that also uses 2-opt and swap as local searches;
 * a GRASP meta-heuristic;
 * a variation of the GRASP meta-heuristic which uses the nearest-neighbor and the Christofides-Serdyukov heuristics to constructs an initial route.


## Next steps

First, we would like to slightly change the current implementation to allow for the possibility that the items are stored in different locations.  To this end, one should replace the restrictions that are based on the Traveling Salesperson Problem by ones based on the Multiple Traveling Salesperson Problem.

Next, we would like to implement time windows.  In order to do that, one needs to estimate the time necessary for a vehicle to travel between every pair of delivery points and between the storage and delivery points.  Then, one is able to add restrictions to the problem that bounds the amount of time that each vehicle is used.

Finally, we would like to replace the restrictions on weights and volumes by an actual 3D-bin packing routine.  To this end, one can either develop their own implementation from scratch, or use one of the several Python libraries that are available online (for example, on Github).
