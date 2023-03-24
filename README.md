# File Expansion for Benchmarking

This script help to expand 1 million Rows to 10 million Rows. If requres 1 billion rows, rename pl.read_csv("1MILLION-ROWS.CSV") and path: pathlib.Path = "Combine.csv", do it again and again, you can get 100 Million rows and then 1 billion rows. You may need to change q.write_csv(path, sep=",") to q.write_csv(path, separator=",") for newer version of Polars.

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
