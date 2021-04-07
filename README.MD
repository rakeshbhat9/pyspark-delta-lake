Repo to test out Delta Lake.

Pre-Requisites:
1. Docker CE installed on the local machine.

Steps:

1. Clone the repo.
2. From within the directory, pull and run Jupyter's PySpark docker image as seen below.


``` docker
    docker run \
          --rm  \
          -v "$PWD":/home/jovyan/work \
          -p 8888:8888 \
          -p 4040:4040 \
          jupyter/pyspark-notebook:latest
```

Above will;
- Pull the image
- Mount the current directory in to the container
- Run jupyter notebook and expose port 8888 from container
- Also expose port 4444 for SparkUI. 

Folder structure is as below;
1. Data - Sample csv data from Kaggle [https://www.kaggle.com/c/demand-forecasting-kernels-only/data]
2. lake - This is the folder where delta lake is instantiated.
- _delta_log : Where delta lake stores json logs
- .parquet - All parquet files generated as result of save and updates.
3. Notebooks:
- spark_delta_table.ipynb - Code to read csv into spark df then saved as Delta lake
- spark_delta_table_ml.ipynb - WIP

```
├── data
│   └── train.csv
├── lake
│   ├── _delta_log
│   │   ├── 00000000000000000000.json
│   │   └── 00000000000000000001.json
│   ├── part-00000-457fb9cf-fd52-423d-9af9-c2922d0c85fe-c000.snappy.parquet
│   ├── part-00000-bb692ea7-87a1-4af0-b7f3-95189f10bdcf-c000.snappy.parquet
│   ├── part-00001-225c2da3-6d10-4561-a7eb-66d51c4e0720-c000.snappy.parquet
│   ├── part-00001-a6373976-cac8-45d4-ab3d-120c40bd7222-c000.snappy.parquet
│   ├── part-00002-2236d358-9a8e-4d96-bb24-38caecae18d6-c000.snappy.parquet
│   ├── part-00002-712810b1-3c68-4e17-9536-246c20c10d4b-c000.snappy.parquet
│   ├── part-00003-376097a8-e45b-4d0e-a3fd-7940325b6c65-c000.snappy.parquet
│   └── part-00003-7557dfdc-4c47-42d3-9801-4c80cafa6c21-c000.snappy.parquet
└── notebooks
    ├── pandas.ipynb
    ├── spark_delta_table.ipynb
    └── spark_delta_table_ml.ipynb
```