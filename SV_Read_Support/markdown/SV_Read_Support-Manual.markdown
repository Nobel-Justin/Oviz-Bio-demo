##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/SV_Read_Support/demo_data/demo.junc.reads.txt) the `official demo input`.

# Introduction
We implement the "SV: Reads Support" to display how sequencing reads support the connection of two segments in SV cases[1]. Concatenated SV junction sequence is horizontally shown in the middle of page with two types of split supporting reads aligning to it base by base. Miscro-homology base pairs are highlighed with pink color. Read base pair quality are colored likt  `samtools tview`, for instance, `Blue:0-9 Green:10-19 Yellow:20-29 White:>=30`. Genes and transcripts that locate in the 5-prime and 3-prime SV segments are shown at the page top and bottom respectively. Area of supporting reads supports zooming in to check the details, such as base quality and alignment mismatch. This visualization greatly helps users determine the credibility of SV cases.
To visualize data, upload a **TXT** file in the *required* format, and then use sidebar options to adjust SV event and read to display.

# SV:Read Support Data (TXT file)
The uploaded **TXT** file must match the *required* format.

User can generate the `junc.reads.txt` files using `read_support.py` with **BAM** file and [SvABA](https://github.com/walaj/svaba) generated sv **VCF** file. Please check https://github.com/paprikachan/ComplexSV for source code and usage of `read_support.py`.

The demo output file `demo_data/simu.junc.reads.txt` stores supporting split reads for given SV. It starts with "sv" section,  the description of headers are listed below:

|header|example|description|
|---|---|---|  
| `chrom_5p` | `chr11` | chromosome of 5' breakpoint |
| `bkpos_5p` | `100000`| position of 5' breakpoint |
| `strand_5p` | `+` | strand of 5' breakpoint |
| `chrom_3p` | `chr1` | chromosome of 3' breakpoint |
| `bkpos_3p` | `101000` | position of  3' breakpoint |
| `strand_3p` | `-` |  strand of 3' breakpoint |
|| `innser_ins:TACCGATAT` | `TACCGATAT` is the detected inner insertion at breakpoint, `NONE` if not available |
| `meta_info` | `HM:TCA,-3` | `TCA` is the detected micro-homology at breakpoint, `-3` is the HM start position, the index convention is the same as `read_position` which will be introduced later |
|| `BX:TTAAGGCCAAGAGTCG-1,TTAAGGCCAAGAGTCG-1` | `TTAAGGCCAAGAGTCG-1,TTAAGGCCAAGAGTCG-1` is the barcode associated with this SV event, `NONE` if not applicable |
| `splits_read_num` | 10 | the number of supporting split read pairs |

Then, it list all supporting split reads, from left to right the columns are ordered by:
+ `read_query_name`, the read id;
+ `read_flags`, it consists of flag `j`, `J`, `r`, `R`, `d`, where

|Flag|Description|
|---|---|
|`j`|The current read is split read|
|`J`|The paired read of current read is split read|
|`r`|The current read is reverse read|
|`R`|The paired read of current read is reverse read|
|`d`|The current read is duplicated|

+ `read_position`, the read start position aligned to reconstructed SV haplotype.


  ```
    |<-   5'segment   ->| inner_ins |<- 3'  segment  ->|
    |xxxxxxxxxxxxxxxxTCA|iiiiiiiiiii|xxxxxxxxxxxxxxxxxx|
                  :    ^
         negative : <- 0 -> positive
                  :
  split_read:     xxxxxxxxxxxxxxxxxxxxxxxxxxxx
                  ^
  read_position: -5
                     
  micro-homology:    TCA   
                     ^
  HM position       -2
  ```
  
+ `read_seq`, the read sequence;
+ `read_qual`, the read sequence quality;
+ `barcode`, the barcode attached to read if applicable, emtpy string `''` otherwise.

# Display Interactions
There are two types of interactions: *Tooltips* and *Download*.

- **Tooltips**
  Tooltips will show necessary information of object that the mouse points to.
  + __*Read*__: Current read and its paired read will be enhanced. Information to show: read id, read offset, wheather this read or its paired read is split read and reversed, attached barcode if applicable. If the read body is clicked, floating box contained above information will appear, users can select, copy, and paste the text they desire.
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
  + __*Transcript*__: choose the transcript to display.

*Manual version=1.1*, written by Miss. CHEN Lingxi and Dr. JIA Wenlong on 2019-12-19.
