# Star Schema Benchmark (SSBM)

This repository contains a streamlined implementation of the table generation code from the **Star Schema Benchmark**, as described in:

> O'Neil, P., O'Neil, E., & Chen, X. (2007). *The Star Schema Benchmark*. [Online Publication of Database Generation Program](http://www.cs.umb.edu/~poneil/StarSchemaB.pdf).

The SSBM is designed to evaluate the performance of database systems optimized for star schema data warehouses. 

It generates formatted text files that you can load in your database.

The generated fact table (`lineorder.tbl`) can be nearly as large as you desire. It can serve for various benchmarking purposes.

---

## Usage

### Prerequisites
- Ensure you have the necessary tools (e.g., `make`) and dependencies installed.
- The `dbgen` tool is used to generate the benchmark tables.

### Generating Tables
Run the following commands to generate the benchmark tables at scale factor 1 (`-s 1`). The scale factor controls the size of the generated data.

```bash
# Build the tool
make

# Generate individual tables
dbgen -s 1 -T c  # customer.tbl
dbgen -s 1 -T p  # part.tbl
dbgen -s 1 -T s  # supplier.tbl
dbgen -s 1 -T d  # date.tbl
dbgen -s 1 -T l  # lineorder.tbl (fact table)

# Generate all tables at once
dbgen -s 1 -T a
```

#### Output Files
The above commands produce the following files:
- `customer.tbl`
- `date.tbl`
- `lineorder.tbl`
- `part.tbl`
- `supplier.tbl`

#### Scaling Data Size
To generate larger datasets, increase the scale factor (`-s`). For example:
```bash
dbgen -s 10 -T a  # Generates all tables with a scale factor of 10
```

### Generating Refresh Data (Insert/Delete)
To create refresh datasets for testing incremental updates:
```bash
dbgen -s 1 -r 5 -U 4
```

#### Parameters
- `-r 5`: Specifies a refresh rate of 5/10,000 (0.05%) for the fact table.
- `-U 4`: Generates 4 segments for deletes and inserts.

#### Output Files
This command produces:
- Delete files: `delete.1`, `delete.2`, `delete.3`, `delete.4`
- Insert files: `lineorder.tbl.u1`, `lineorder.tbl.u2`, `lineorder.tbl.u3`, `lineorder.tbl.u4`


## Notes
- Adjust the scale factor (`-s`) and refresh rate (`-r`) based on your testing needs.
- Ensure sufficient disk space for larger scale factors, as file sizes grow significantly.
- Refer to the original paper for detailed benchmark specifications and usage scenarios.



# Suitability

This is strictly for research purposes. 
