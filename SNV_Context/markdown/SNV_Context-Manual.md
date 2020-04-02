##### Please try the demo file in the sidebar (`Demo File Sets`).

<!-- ##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/SNV_Context/demo_data/SNV_Context_demo_MutList.tsv.bgz) and [Check](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data/SNV_Context_demo_MutList.tsv.bgz) the `SNV TSV.bgz input` (required).
##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/SNV_Context/demo_data/SNV_Context_demo_Region.bed) and [Check](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data/SNV_Context_demo_Region.bed) the `Region BED input` (optional). -->

# Introduction
The 'Context' visualization, otherwise known as the 'Lego plot' of mutational frequencies, describes the distribution of mutations across batch samples on a given region. Base substitutions are divided into six types to represent the six possible base changes (each type represented by a different color as shown in the “Mutation Type” legend). Substitutions in each type are further subdivided by the 16 possible flanking nucleotides surrounding the mutated base as listed in the “Trinucleotide Context” table. The pie chart illustrates the percentage of all mutations types in said batch samples.

# Input Files
Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data).

## SNV File
This input file could be standard **MAF** file (see [format](https://docs.gdc.cancer.gov/Data/File_Formats/MAF_Format/)) or **VCF** file.

Or, a simple **TSV** file in the format specified below.

| #contig |  position | ref_allele |  alt_allele | tumor_f |
|---|---|---|---|---|
| chr1  | 101686  | A | G | 0.113636 |

- the first line should be the `header` as specified above.
- `#` prefix is mandatory to indicate the header line.
- `contig` and `position` respectively stand for the chromosome and position of the mutation.
- `ref_allele` and `alt_allele` respectively stand for the base before and after the mutation.
- `tumor_f` is optional. We allow users to filter mutations with `tumor_f` value by custom condition.

<!--   The TSV file must be `sorted` by chromosome and position, and compressed by `bgzip` tools for `tabix` indexing to support fast data processing at the backend of Oviz-Bio.<br/>
  For example [tsv file](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data/SNV_Context_demo_MutList.tsv), run the following command in the linux terminal (bgzip installed):
  <pre><code>(head -1 SNV\_Context\_demo\_MutList.tsv; sed -n '2,$p' SNV\_Context\_demo\_MutList.tsv | sort -k1,1 -k2n) | bgzip -c > SNV\_Context\_demo.tsv.bgz</code></pre>
 -->
## Custom BED File (optional)

A custom bed file allows users to replace the default region used in our website, which is the whole genome sequence. We will filter out mutations that are not in the custom region during the calculation. Note that the uploaded bed file is only applied when you **choose the custom bed option** in the **Settings** section of the sidebar. 

The uploaded **BED** file must match the *required* format as specified below (please keep the `header`).

| #chr |  startPos |  endPos |
|---|---|---|
| chr1  | 11174854  | 11175054 |

# Display Interactions
There are three types of interactions: *Tooltips*, *Transparent Bins* and *Download*.

- **Tooltips**<br/>
A tooltip shows necessary information of the object the mouse points to.
  - _*bin*_: A tooltip is drawn when the mouse lands on the bottom of a bin. The displayed information includes the mutation type and the trinucleotide context represented by this bin as well as the exact height of the bin.
  - _*pie*_: A tooltip is drawn when the mouse moves to a certain arc of the pie chart and shows the exact percentage of the corresponding mutation type among all mutations.
- **Transparent Bins**<br/>
  When the mouse lands on the bottom of a bin, the bottom will be highlighted and all bins before it will become transparent to avoid hindered view.
- **Download**<br/>
  One SVG file will be generated when the '**Download**' button is clicked. Only the default **Dark Theme** is available at this point.

# Sidebar Functions
The sidebar provides diverse options to fine-tune the display, namely managing files, adding labels on bins, choosing base regions and setting the measurements of mutations.

- **Files**
  - __*Manage Files*__: checklist of TSV files uploaded previously, delete or download said BGZ files.
  - __*Upload*__: upload batch sample BGZ file and the optional bed TSV file. Note that the duplicated file name will be alerted and given a random postfix.
  - __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered users (each account has certain storage).
  - __*File Sets*__: save a batch sample file and a bed file together as a file set. Users can also choose to apply one file set from all saved ones.
- **Labels**
  - __*Label Buttons*__: choose a symbol (except for the first and the last button) to enter labeling mode. In this mode, when you click a bar, the corresponding symbol will be added to the bar as an annotation.
  - __*Off Button*__: click this button to exit from labeling mode. Re-click to re-enter labeling mode with the last-used symbol. 
  - __*Remove Button*__: click to enter removing mode. In this mode, when you click a bar with a symbol, the corresponding symbol will be removed.
- **Setting**<br/>
  - __*Interval*__: choose between the default region and the custom region. If no bed file is provided, the only option is the default whole genome region.
  - __*Y axis*__: provide three measurements of the mutation count, namely the numeric sum of the mutation, mutations per Mb and the percentage among all mutations.
  - __*Filter by tumor\_f*__: choose the compare method and the threshold for filtering mutations.

*Manual version=1.4*, written by Miss. Li Shiying and Dr. JIA Wenlong on 2020-04-02.
