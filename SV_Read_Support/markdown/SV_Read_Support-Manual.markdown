##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/SV_Read_Support/demo_data/demo.junc.reads.txt) the `official demo input`.

# Introduction
For one given sv event, "SV: Read Support" exhibits all split reads across the breakpoints.  The top and bottom chromosome axis respectively represent the 5' and 3' breakpoint position, associated genes and transcripts annotation are also illustrated. The "consensus junction sequence" with white text in the black ground on the top is the concatenated SV junction sequence. All supporting split reads were aligned to the consensus junction sequence base by base. Users may zoom in to display the base pair of split reads in detail. Read base-pair quality are colored followed the scheme of `samtools tview`, for instance, `Blue:0-9 Green:10-19 Yellow:20-29 White:>=30`. All alignment mismatches are colored in red. Small insertions were labelled with yellow “inverted triangle". Small deleteions were labelled with red '-'. Micro-homology base pairs are highlighted in pink. Users may upload the required input file, then utilize sidebar options to select the desired SV event and read to display.

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
| `sv_meta_info` | `HM:TCA,-3` | `TCA` is the detected micro-homology at breakpoint, `-3` is the HM start position, the index convention is the same as `read_position` which will be introduced later |
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
+ `read_meta_info`, stores all read meta information, e.g. `BX:NONE;INS:-12(3),15(2);DEL:-86(1),36(4)`.
  - `BX:GACACTAGTTAAGATG-1` is the barcode associated with the read.
  - `INS:-12(3),15(2)` shows the small insertions on reads. `-12(3)` means that the first base of the insertion has 3 base pairs and its index is -12, and `15(2)` means that the first base of the second insertion has 2 base pairs and locates at index 15.  Note that the insertion sequence will not be displayed on reads, but marked with a yellow “inverted triangle” at the insertion position.
  - `DEL:-86(1),36(4)` shows the small deletaion on reads. `36(4)` means that the front base of the deleted fragment is index 36, and the length of the deleted fragment is 4 bases. The deletion sequence is filled with red '-' on reads.


# Display Interactions
There are two types of interactions: *Tooltips* and *Download*.

- **Tooltips**
  Tooltips will show necessary information of object that the mouse points to.
  + __*Read*__: Current read and its paired read will be enhanced. Information to show: read id, read offset, wheather this read or its paired read is split read and reversed, attached barcode if applicable. If the read body is clicked, floating box contained above information will appear, users can select, copy, and paste the text they desire.
  + __*Gene Transcript*__: Transcript name, transcript start position, and transcript end position.
  
- **Download**
  One SVG file will be generated when the '**Download**' button is clicked. Two themes are supplied: the default theme with dark background and the light theme with white backgroud. 
- **Light Theme**
  To use the light theme, please click the '**Light Theme**' button.

# Sidebar Functions
The sidebar provides diverse options to fine-tune the display, such as manage files, reset color, select SV event, and so on.

- **Files**
  + __*Upload*__: upload heatmap TXT file, and manage uploaded files. Note that duplicated file name will be alerted and given a random postfix.
  + __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered user (each account has certain storage).
  + __*File Sets*__: NOT available to this page.
- **Reads**
  Select desired read to present.
- **Transcripts**
  Select desired gene transcript to present.
- **Settings**
  + __*SV Case*__: select the SV event and maximum reads number to show.
  + __*Sort Read*__: choose read sorted by "Junc read index" or "Left read index".
  + __*Read Quality*__: tick to display read quality and select quality format.

*Manual version=1.1*, written by Miss. CHEN Lingxi and Dr. JIA Wenlong on 2019-12-19.
