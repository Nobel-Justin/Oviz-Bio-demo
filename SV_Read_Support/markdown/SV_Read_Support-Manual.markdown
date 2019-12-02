# Introduction
xxx. To visualize data, upload a **TXT** file in the *required* format, and then use sidebar options to adjust xxx.

# SV:Read Support Data (TXT file)
The uploaded **TXT** file must match the *required* format. Several demo files from **References** are provided in <a href="https://github.com/Nobel-Justin/BTDraw/tree/master/SV_Read_Support/demo_data" target="_blank">BTDraw</a> GitHub project.

User can generate the `junc.reads.txt` files using `read_support.py` in https://github.com/paprikachan/ComplexSV.

The demo output file `demo_data/simu.junc.reads.txt` stores supporting split reads for given SV. It starts with "sv" section.

| chrom_5p |  bkpos_5p | chrom_3p |  bkpos_3p |  inner_ins | splits_read_num |
|---|---|---|---|---|---|
| chr11  | 100000  | chr1 | 101000  | Inner-Ins:TACCGATAT  |10 | 

where `inner_ins` refers to the detected inner insertion, and `splits_read_num` refers to the number of supporting split read pairs.

Then, it list all supporting split reads, ordered by:
+ `read_query_name`, the read id;
+ `read_flags`, it consists of flag `J`, `P`, `r`, `R`, `d`, where

  |Flag|Description|
  |---|---|
  |`J`|The current read is split read|
  |`P`|The paired read of current read is split read|
  |`r`|The current read is reverse read|
  |`R`|The paired read of current read is reverse read|
  |`d`|The current read is duplicated|

+ `read_position`, the read start position aligned to reconstructed SV haplotype.
  ```
   |<-   5'segment   ->| inner_ins |<- 3'  segment  ->|
   |xxxxxxxxxxxxxxxxxxx|iiiiiiiiiii|xxxxxxxxxxxxxxxxxx|
                  :    ^
         negative : <- 0 -> positive
                  :
  split_read:     xxxxxxxxxxxxxxxxxxxxxxxxxxxx
                  ^
  read_position: -5
  ```
+ `read_seq`, the read sequence;
+ `read_qual`, the read sequence quality.

# Display Interactions
There are two types of interactions: *Tooltips* and *Download*.

To be continued...

# Sidebar Functions
The sidebar provides diverse options to fine-tune the display, such as manage files, reset color, select SV event, and so on.

- **Files**
  + __*Upload*__: upload heatmap TXT file, and manage uploaded files. Note that duplicated file name will be alerted and given a random postfix.
  + __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered user (each account has certain storage).
  + __*File Sets*__: NOT available to this page.
- **To be continued...**

*Manual version=1.0*, written by Miss. CHEN Lingxi on 2019-11-28.
