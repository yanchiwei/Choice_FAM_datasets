# Testing Dataset for Choice-Based Airline Fleet Assignment and Schedule Design
This repository contains an additional synthetic testing dataset (based on realistic characteristics of data from a major carrier in 2016) for the paper ["Choice-Based Airline Schedule Design and Fleet Assignment: A Decomposition Approach"](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3513164). If you use any of the material here, please include a reference to the paper and this webpage.


## Instance Summary

Flights | Itineraries | Fare Products | Markets | Fleet Types | Aircraft | Market Share
------------ | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- 
815 | 4,290 | 47,190 | 819 | 7 | 186 | 42.36%

## Schema

- `flight.json`
  
  key: flight ID
  
  value:
  {"origin": origin airport;
  "destination": destination airport;
  "depttime": departure time in hhmm format;
  "arrtime": arrival time in hhmm format}
  
- `product.json`

  key: product ID
  
  value:
  {"fare": price of the fare product;
  "cabin": cabin of the fare product, {'Y': economy, 'C': business, 'F': first};
  "origin": origin airport;
  "destination": destination airport;
  "demand": unconstrained demand/attractiveness value;
  "market": origin-destination market;
  "leg": list of flight IDs which this fare product uses}
  
- `market.json`

  key: market ID, origin+destination
  
  value:
  {"total_demand": total demand/attractiveness value in this origin-destination market (including competing airline);
   "OA_demand": competing airlines' demand/attractiveness value in this origin-destination market}
   
- `fleet.json`

  key: fleet ID
  
  value:
  {"FCAP": seats in F cabin; 
   "CCAP": seats in C cabin; 
   "YCAP": seats in Y cabin;
   "hourly_cost": hourly operating cost;
   "availability": number of aircraft available for this fleet type}
  
- Minimum Turn Time: 35 minutes
  
## Computation Results

- Subnetwork partition (<img src="https://render.githubusercontent.com/render/math?math=\Pi_c">, <img src="https://render.githubusercontent.com/render/math?math=\Pi_t">), see paper for notation (cf. Table 3).

  - ``max_profit_ratio``: 0.5%
  - number of flights in <img src="https://render.githubusercontent.com/render/math?math=\Pi_c">: 143
    - of size: 1: 74, 2: 16, 3: 11, 4: 1
  - number of flights in <img src="https://render.githubusercontent.com/render/math?math=\Pi_t">: 672
    - of size: min: 4, max: 641, <img src="https://render.githubusercontent.com/render/math?math=|\Pi_t|">: 6
  - fare optimization CPU time: 31 seconds

- 5 hour CPU time, 2.3 GHz Quad-Core Intel Core i7, Gurobi 9.02, see paper for notation (cf. Table 4).

Model | Fare Split | Obj. Val. | LP Relax. | CPU Time(s) | Solver Gap | B&B Node | Profit | Num of Flight | Annual Profit Improvement (Million)
------------ | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- 
ISD-FAM | -- | 4,328,945 | 4,584,530 | 18,000 | 0.04% |  30,722 | 6,159,056 | 743 | 0
ISD-FAM-SR-ITIN | -- | 3,891,445 | 4,140,062 | 18,000 | 4.38% |  4,903 | 6,047,442 | 711 | (40.74)
CSD-FAM | -- | 6,208,314 | 6,748,932 | 18,000 | 5.08% |  5,992 | 6,208,314 | 662 | 17.98
CSD-FAM-S | -- | 5,955,392 | 6,630,624 | 18,000 | 8.05% |  1,148 | 5,955,392 | 616 | (74.34)
S-CSD-FAM (<img src="https://render.githubusercontent.com/render/math?math=\Pi_c">, <img src="https://render.githubusercontent.com/render/math?math=\Pi_t">) | opt | 6,328,372 | 6,721,355 | 18,000 | 3.50% |  6,936 | 6,255,524 | 679 | 35.21
