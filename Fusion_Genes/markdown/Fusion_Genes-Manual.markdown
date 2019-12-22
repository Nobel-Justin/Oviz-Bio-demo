##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/Fusion_Genes/demo_data/Fusion_Genes_demo.tsv) and [Check](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/Fusion_Genes/demo_data/Fusion_Genes_demo.tsv) the `offical demo input`.

# Introduction
Fusion gene is a chimeric transcript consists of gene bodies from two or more previously separate genes. Many fusion genes have been found to contribute tumorigenesis of multiple cancer types. We implement the `Fusion Genes` visualization to show the whole structure of chimeric transcript structure.

# Input Files

## Fusion TSV File

Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/Fusion_Genes/demo_data/Fusion_Genes_demo.tsv).<br/>
The uploaded **TSV** file must match the *required* format as specified below.

- **header**<br/>
  The header should follow the following format:

| #Sample-ID |  up_gene | up_chr | up_pos |  up_covlen | down_gene | down_chr | down_pos |  down_covlen |
|---|---|---|---|---|---|---|---|---|
| T003 | FGFR3 | chr4 | 1808661 | 886 | TACC3 | chr4 | 1739325 | 704 |

  - `up_covlen` and `down_covlen` respectively stand for the distance fusion supporting reads extend from the junction position of upstream (5') and downstream (3') fusion partern genes.
  - `up_pos` and `down_pos` are coordinates in the genome.
  - see more relevant information from SOAPfuse [wiki](https://sourceforge.net/p/soapfuse/wiki/Output_Files/) page.

# Display Interactions
Reference normal gene body of fusion partners are displayed with junction positions marked.

- **Tooltips**<br/>
  - __*exon*__: NO., interval, and length.
- **Pages**<br/>
  click 'Prev' or 'Next' to go to other genes (as listed in the Fusion TSV File).
- **Download**<br/>
  One SVG file will be generated when the '**Download**' button is clicked. Two themes are supplied: the default theme with a dark background and the light theme with white background. To use the light theme, please click the '**Light Theme**' button.

# Sidebar Functions

- **Files**
  - __*Manage Files*__: checklist of files uploaded previously, delete or download files.
  - __*Upload*__: upload files. Note that the duplicated file name will be alerted and given a random postfix.
  - __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered users (each account has certain storage).
  - __*File Sets*__: save multiple files together as a file set. User can also choose to apply one file set previously saved.
- **Data**
  To check exons information of fusion genes.
- **Setting**<br/>
  - enbale or disable Simplified mode.
  - display transcript name rather than gene name.

*Manual version=1.0*, written by Dr. JIA Wenlong on 2019-12-19.
