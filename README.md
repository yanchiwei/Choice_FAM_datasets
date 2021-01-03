# Testing Data Set for Choice-Based Fleet Assignment and Schedule Design
This repository containts a testing dataset for the paper ["Choice-Based Airline Schedule Design and Fleet Assignment: A Decomposition Approach"](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3513164).

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
   "availability": number of aircraft available for this fleet type
  }
  
- Minimum Turn Time: 35 minutes
  
## Computation Results

- Subnetwork partition (<img src="https://render.githubusercontent.com/render/math?math=\Pi_c^1">, <img src="https://render.githubusercontent.com/render/math?math=\Pi_t^1">), see paper for notation (cf. Table 3).

  - ``max_profit_ratio``: 1.0%
  - number of flights in <img src="https://render.githubusercontent.com/render/math?math=\Pi_c">: 198
    - of size: 1: 95, 2: 26, 3: 17
  - number of flights in <img src="https://render.githubusercontent.com/render/math?math=\Pi_t">: 617
    - of size: min: 4, max: 575, <img src="https://render.githubusercontent.com/render/math?math=|\Pi_t|">: 9
  - fare split time: 32 seconds

- 5 hour CPU time, 2.3 GHz Quad-Core Intel Core i7, Gurobi 9.02, see paper for notation (cf. Table 4).

Model | Fare Split | Obj. Val. | LP Relax. | CPU Time(s) | Solver Gap | B&B Node | Profit | Annual Profit Improvement
------------ | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- 
ISD-FAM | -- | 4,317,738 | 4,573,773 | 18,000 | 0.03% |  34,336 | 6,157,037 | 0
ISD-FAM-SR-ITIN | -- | 3,948,695 | 4,130,687 | 18,000 | 1.46% |  14,427 | 6,080,153 | (28.06) Million
CSD-FAM | -- | 6,172,158 | 6,740,345 | 18,000 | 4.53% |  8,838 | 6,172,158 | 5.52 Million
S-CSD-FAM(<img src="https://render.githubusercontent.com/render/math?math=\Pi_c^1">, <img src="https://render.githubusercontent.com/render/math?math=\Pi_t^1">) | opt | 6,373,924 | 6,733,420 | 18,000 | 3.25% |  8,446 | 6,235,549 | 28.67 Million
