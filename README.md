# Testing Data Set for Choice-Based Fleet Assignment and Schedule Design
This repository containts a testing dataset for the paper ["Choice-Based Airline Schedule Design and Fleet Assignment: A Decomposition Approach"](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3513164).

## Instance Summary

Flights | Itineraries | Fare Products | Markets | Fleet Types | Aircraft | Market Share
------------ | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- 
815 | 4290 | 47190 | 819 | 7 | 186 | 42.36%

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
  "cabin": cabin of the fare products, {'Y': economy, 'C': business, 'F': first};
  "origin": origin airport;
  "destination": destination airport;
  "demand": unconstrained demand / attractiveness value;
  "market": origin-destination market;
  "leg": list of flight IDs which this fare product uses}
  
- `market.json`

  key: market ID, origin+destination
  
  value:
  {"total_demand": total demand in this origin-destination market (includin competing airline);
   "OA_demand": competin airlines' demand in this origin-destination market}
   
- `fleet.json`

  key: fleet ID
  
  value:
  {"FCAP": seats in F cabin; 
   "CCAP": seats in C cabin; 
   "YCAP": seats in Y cabin;
   "hourly_cost": hourly operating cost;
   "availability": number of aircraft available for this fleet type
  }
