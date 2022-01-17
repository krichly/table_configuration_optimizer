# Table Configuration Optimizer 

A linear programming approach to jointly optimize the sorting, compression, indexing, and tiering decision for spatio-temporal workloads. 

## Setup

To get all dependencies of the Table Configuration Optimizer installed, run

    pip install -r requirements.txt

To start the jupyter lab, run

    jupyter lab

Additionally, it is required to have a solver, such as [gurobi](https://www.gurobi.com), installed.

## Example: Workload 

We used a workload consisting of six query templates to evaluate the models based on the data of a transportation network company. 

| ID            | Query            | Frequency | Skipped Chunks   |
| ------------- | ---------------- | --------- | ---------------- |
| q<sub>0</sub> | SELECT * FROM TABLE WHERE <br> ("driver_id" <= {selectivity of the value: 0.0001}) AND <br> ("status" <= {0.7}) | 20%       | 0, 3, 6, 7, 8 |
| q<sub>1</sub> | SELECT * FROM TABLE WHERE <br> ("timestamp" BETWEEN {0.2}) AND <br> ("latitude" BETWEEN {0.5}) AND <br> ("longitude" BETWEEN {0.5}) AND <br> ("status" <= {0.7}) | 15%       |  |
| q<sub>2</sub> | SELECT * FROM TABLE WHERE <br> („driver_id" <= {0.01}) AND <br> ("latitude" BETWEEN {0.1}) AND <br> ("longitude" BETWEEN {0.1}) | 10%       | 4, 5, 6, 7, 8, 9 |
| q<sub>3</sub> | SELECT * FROM TABLE WHERE <br> ("timestamp" <= {0.05}) AND <br> ("latitude" BETWEEN {0.7}) AND <br> ("longitude" BETWEEN {0.7}) | 25%       | 0, 1, 2, 6, 7, 8, 9 |
| q<sub>4</sub> | SELECT * FROM TABLE WHERE <br> („driver_id" <= {0.01}) AND <br> ("timestamp" <= {0.4}) | 15%       | 1, 2, 3, 4, 5, 6, 7, 8, 9 |
| q<sub>5</sub> | SELECT * FROM TABLE WHERE <br> ("latitude" BETWEEN {0.01}) AND <br> ("longitude" BETWEEN {0.01}) AND <br> ("timestamp" BETWEEN {0.5}) | 15%       | 0, 1, 8, 9 |

Further workload examples are provided in `/data/workloads`. 


