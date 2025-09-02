# Theoretical calculations of condensate velocity

These notebooks are used to calculate the condensate velocity from theory. The `Fig_1C_CSV.ipynb` notebook uses Python, whereas `Fig_2B.ipynb`, `Fig_4B.ipynb`, and `Fig_S2-S3-S5-S6.ipynb` uses Julia.

First, run `Fig_1C_CSV.ipynb` to generate `flow_stats.csv` and `flow_stats_100.csv` files. Then, use the following code in `Fig_4B.ipynb` to insert analytical calculations into `flow_stats_100.csv`. Only then can you make the analytical velocity plots in the Python notebook `Fig_1C_CSV.ipynb`.

```
Threads.@threads for stats in glob("20240224_FlowPhaseDiagramHighRes/*/flow_stats_100.csv")
    df = CSV.read(stats, DataFrame)
    df[!,"analytical_velocity"] = map(introw,eachrow(df))
    # arr = df[!, "mean_radius"]
    # avgR = sum(arr)/length(arr)
    # df[!,"analytical_velocity_avgR"] = map(row -> introwR(row, avgR),eachrow(df))
    CSV.write(stats, df)
    print("Done. ")
end
```