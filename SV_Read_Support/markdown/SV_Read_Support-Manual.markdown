##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/SV_Read_Support/demo_data/demo.junc.reads.txt) and [Check](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/SV_Read_Support/demo_data/demo.junc.reads.txt) the `official demo input`.

# Introduction
We implement the "SV: Reads Support" to display how sequencing reads support the connection of two segments in SV cases[1]. Concatenated SV junction sequence is horizontally shown in the middle of page with two types of split supporting reads aligning to it base by base. Genes and transcripts that locate in the 5-prime and 3-prime SV segments are shown at the page top and bottom respectively. Area of supporting reads supports zooming in to check the details, such as base quality and alignment mismatch. This visualization greatly helps users determine the credibility of SV cases.
To visualize data, upload a **TXT** file in the *required* format, and then use sidebar options to adjust SV event and read to display.

# SV:Read Support Data (TXT file)
The uploaded **TXT** file must match the *required* format.

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

- **Tooltips**
  Tooltips will show necessary information of object that the mouse points to.
  + __*Gene Transcript*__: Transcript name, transcript start position, and transcript end position.
- **Download**
  One SVG file will be generated when the '**Download**' button is clicked. Two themes are supplied: the default theme with dark background and the light theme with white backgroud. To use the light theme, please click the '**Light Theme**' button.


# Sidebar Functions
The sidebar provides diverse options to fine-tune the display, such as manage files, reset color, select SV event, and so on.

- **Files**
  + __*Upload*__: upload heatmap TXT file, and manage uploaded files. Note that duplicated file name will be alerted and given a random postfix.
  + __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered user (each account has certain storage).
  + __*File Sets*__: NOT available to this page.
- **Settings**
  + __*Display*__: select the SV event and maximum reads number to show.
  + __*Reads*__: choose the read to display.

*Manual version=1.1*, written by Miss. CHEN Lingxi and Dr. JIA Wenlong on 2019-12-19.
