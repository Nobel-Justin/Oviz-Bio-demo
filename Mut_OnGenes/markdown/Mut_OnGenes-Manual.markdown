##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/Mut_OnGenes/demo_data/Mut_OnGenes_demo.mutations.csv) and [Check](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/Mut_OnGenes/demo_data/Mut_OnGenes_demo.mutations.csv) the `Mutation CSV input`.
##### [Download](https://github.com/Nobel-Justin/Oviz-Bio-demo/raw/master/Mut_OnGenes/demo_data/Mut_OnGenes_demo.depth.tsv.bgz) the `Depth BGZ input`.

# Introduction
The 'Mutations on Genes' displays SNVs and InDels with their coordinates and function annotations along the selected transcript of a given gene. Mutation information can be viewed in three levels (genome, cDNA, and peptide). Different icons are applied to mutations according to their types and function changes, such as synonymous and missense SNV, frame-shift InDels. Interactive tooltip gives more information, including mutation coordinates, function area and details of exons. Sidebar offers options to adjust displays, such as changing resolution, and selecting mutation. This visualization is commonly utilized to show the mutation landscape of given genes in a group of cancer samples.

# Input Files

## Mutation CSV File

Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/Mut_OnGenes/demo_data/Mut_OnGenes_demo.mutations.csv).<br/>
The uploaded **CSV** file must match the *required* format as specified below.

- **header**<br/>
  The header should follow the following format:

| #SampleID |  alt_type |  chr | pos |  ref_allele | alt_allele | gene |
|---|---|---|---|---|---|---|---|
| TCGA-AK-3451 | SNP | chr3 | 10183646 | G | A | VHL |

## Depth tsv.BGZ File

Please upload a **tsv.bgz** compressed file to supply the depth distribution of the gene region.<br/>
Download the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/raw/master/Mut_OnGenes/demo_data/Mut_OnGenes_demo.depth.tsv.bgz). <br/>
The uploaded file must match the *required* format as specified below.

- **header**<br/>
  The header should follow the following format:

| #chr |  pos |  depth |
|---|---|---|
| chr1  | 10182642  | 100 |

- `#` prefix is mandatory to indicate the header line.
- `chr` and `pos` respectively stand for the chromosome and position of the mutation.
- `depth` is the sequencing depth at this genomic position.

  The TSV file must be `sorted` by chromosome and position, and compressed by `bgzip` tools for `tabix` indexing to support fast data processing at the backend of Oviz-Bio.<br/>
  For example, run the following command in the linux terminal (bgzip installed):
  <pre><code>(head -1 Mut\_OnGenes\_demo.depth.tsv; sed -n '2,$p' Mut\_OnGenes\_demo.depth.tsv | sort -k1,1 -k2n) | bgzip -c > Mut\_OnGenes\_demo.depth.tsv.bgz</code></pre>

# Display Interactions

- **Highlights**<br/>
  - exons will be highlighted in three levels (DNA, cDNA, peptide) simultaneously.
  - mutation guide line will be highlighted to link mutated locations in the three levels.
- **Tooltips**<br/>
  Tooltips will show necessary information of object that the mouse points to.
  - __*exon*__: NO., interval, transcript, sense strand, sample amount having mutation in this exon.
  - __*mutation*__: mutation details, sample(s) involved.
- **Level exchange**<br/>
  - the main display level can be changed via clicking the level name.
- **Zoom in/out**<br/>
  the main display level can be zoomed in/out via mouse wheel.
- **Pages**<br/>
  click 'Prev' or 'Next' to go to other genes (as listed in the Mutation CSV File).
- **Download**<br/>
  One SVG file will be generated when the '**Download**' button is clicked. Two themes are supplied: the default theme with a dark background and the light theme with white background. To use the light theme, please click the '**Light Theme**' button.

# Sidebar Functions

- **Files**
  - __*Manage Files*__: checklist of files uploaded previously, delete or download files.
  - __*Upload*__: upload files. Note that the duplicated file name will be alerted and given a random postfix.
  - __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered users (each account has certain storage).
  - __*File Sets*__: save multiple files together as a file set. User can also choose to apply one file set previously saved.
- **Data**
  - __*Genes*__: select transcript for each gene.
  - __*Mutations*__: enable or disable to display certain mutations.
  - __*Exons*__: reset resolution for each exon.
- **Setting**<br/>
  - select gene to display.
  - extend certain interval bilaterally from the gene body.
  - enbale or disable displaying of exon NO.
  - reset the Intron:Exon displaying resolution scale in DNA level.
  - reset the UTR:CDS displaying resolution scale in cDNA level.

*Manual version=1.1*, written by Dr. JIA Wenlong on 2019-12-27.
