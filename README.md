# benchmarking

This script help to expand 1 Million Rows to 10 Million Rows. If requres 1 billion rows, rename pl.read_csv("1MILLION-ROWS.CSV") and path: pathlib.Path = "Combine.csv", do it again and again, you can get 100 Million rows and then 1 Billion rows.

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
