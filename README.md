# benchmarking

import polars as pl
import time
import pathlib
s = time.time()

df = pl.read_csv("1MILLION-ROWS.CSV")

q = pl.concat(
    [
        df,
        df,
        df,
        df,
        df,
        df,
        df,
        df,
        df,
        df
    ],
    how="diagonal",
)

path: pathlib.Path = "Combine.csv"
q.write_csv(path, sep=",")

e = time.time()
print("Polars Loading Time = {}".format(e-s))
