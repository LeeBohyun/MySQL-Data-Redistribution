# MySQL Data Redistribution

## Publication
- Bohyun Lee, Mijin An, Sangwon Lee, "A Case for Space Compaction of B-Tree Nodes on Flash Storage", IEEE Access Vol. 10 2022, April 2023 
- [Publication Link](https://ieeexplore.ieee.org/document/10102447?source=authoralert)

## Motivation
While B-Tree is a ubiquitous index structure used in managing data, it is well known for its low space utilization in nodes. Such space under-utilization is detrimental to flash storage in terms of cost and performance. In particular, the logical space waste in B-tree will amplify physical writes inside flash storage, worsening the transaction throughput. 

## Contribution
Our evaluation results from running OLTP benchmarks(TPC-C) using the data redistribution MySQL clearly show that those optimizations improve transaction throughput (i.e., more than 50%) with less space and cost (i.e., less than 40%) in flash storage. Also the overall index space utilization is improved.


## Prerequisites & Installation Guide

1. Install prerequisites of mysql-5.6.26. Follow the instructions in the [site](https://github.com/LeeBohyun/mysql-tpcc/blob/master/installation_guide/multi-mysql-tpcc.md).
2. Clone this repository.
```bash
$ git clone https://github.com/FlashSQL/MySQL-Data-Redistribution.git
```
3. Run ``mysqld`` server to run MySQL.
4. Compare with Vanilla MySQL and see how table size changes



## Implementation Details about Data Redistritbution
- reserved free space are applied according to the record sizes and update pattern
- added a new function in btr0btr.cc: btr_page_redistribute_before_split()
- returns the inserted record
- btr_page_redistribute_before_split() is called during btr_page_split_and_insert()(btr0btr.cc) before split is performed
- modifications in srv0srv and fil0fil are for adding table id and table name

## Future Work
We are planning to create additonal branches (MySQL-5.7, MySQL-5.8) for porting.

## References
- https://dev.mysql.com/
