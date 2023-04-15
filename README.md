# File Expansion for Benchmarking

This script is a tool that can increase the amount of data you have by copying the existing rows multiple times. For example, if you have a file with 1 million rows of data, this script can create a new file with 10 million rows of data by copying the original file 10 times and appending them together. If you want to have more data, such as 1 billion rows, you can modify the script by changing the name and location of the input and output files. 

The input file is specified by pl.read_csv(“1MILLION-ROWS.CSV”) and the output file is specified by path: pathlib.Path = “Combine.csv”. You can rename these files to whatever you want, as long as they match the format and location of your data. Then, you can run the script again to create another file with 10 times more data than the previous one. You can repeat this process as many times as you need until you reach your desired amount of data. 

However, you should also be aware that if you are using a newer version of Polars, which is a library that helps you manipulate data in Python, you may need to change one line of code in the script. The line that writes the output file to a CSV format is q.write_csv(path, sep=“,”), but in newer versions of Polars, the argument sep has been renamed to separator. So, you may need to change this line to q.write_csv(path, separator=“,”) to avoid errors.

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

print("Polars Processing Time = {}".format(e-s))

# About Polars

https://www.pola.rs/

# About Peaks
https://www.linkedin.com/in/max01/recent-activity/all/
