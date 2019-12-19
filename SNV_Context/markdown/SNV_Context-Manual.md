##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/SNV_Context/demo_data/SNV_Context_demo_MutList.tsv.bgz) and [Check](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data/SNV_Context_demo_MutList.tsv.bgz) the `official demo input`.

# Introduction
The 'Context' visualization, otherwise known as the 'Lego plot' of mutational frequencies, describes the distribution of mutations across batch samples on a given region. Base substitutions are divided into six types to represent the six possible base changes (each type represented by a different color as shown in the “Mutation Type” legend). Substitutions in each type are further subdivided by the 16 possible flanking nucleotides surrounding the mutated base as listed in “Trinucleotide Context” table. The pie chart illustrates the percentage of all mutations types on said batch samples. To visualize data, upload a **BGZ** file in the *required* format and use sidebar options to customize the display.

# Context Data (BGZ file)

## Batch Sample
The uploaded **BGZ** file must match the *required* format as specified below.<br/>
Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data/SNV_Context_demo_MutList.tsv.bgz).

- **header**<br/>
  The file can be converted from a TSV file with the following format: 
  | #contig |  position |  context | ref_allele |  alt_allele | tumor_f |
  |---|---|---|---|---|---|
  | chr1  | 101686  | AxA | A | G | 0.113636 |
  - `#contig` and `position` respectively stand for the chromosome and position of the mutation.
  - `context` stands for the trinucleotide context of the mutation.
  - `ref_allele` and `alt_allele` respectively stand for the base before and after the mutation.
  - `tumor_f` is optional. We allow user to filter out mutations with `tumor_f` value lower than a custom threshold.

  To convert the TSV file, for example [SNV_Context_demo_MutList.tsv.txt](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data/SNV_Context_demo_MutList.tsv.txt), run the following command in the terminal
  <pre><code>(head -1 SNV_Context_demo_MutList.tsv.txt; sed -n '2,$p' SNV_Context_demo_MutList.tsv.txt | sort -k1,1 -k2n) | bgzip -c > SNV_Context_demo.tsv.bgz</code></pre>
  This command sorts the TSV file by chromosome and position for faster data processing.

## Custom Bed File (optional)

A custom bed file allows user to replace the default region used in our website, which is the whole genome sequence. We will filter out mutations that are not in the custom region during the calculation.

The uploaded **TSV** file must match the *required* format as specified below.<br/>
Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data/SNV_Context_demo_Region-1.bed) and [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Context/demo_data/SNV_Context_demo_Region-2.bed).

- **header**<br/>
  The header should follow the following format:
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
  - __*File Sets*__: save a batch sample file and a bed file together as a file set. User can also choose to apply one file set from all saved ones.
- **Labels**
  - __*Label Buttons*__: choose a symbol (except for the first and the last button) to enter labeling mode. In this mode, when you click a bar, the corresponding symbol will be added to the bar as annotation.
  - __*Off Button*__: click this button to exit from labeling mode. Re-click to re-enter labeling mode with the last-used symbol. 
  - __*Remove Button*__: click to enter removing mode. In this mode, when you click a bar with symbol, the corresponding symbol will be removed.
- **Setting**<br/>
  - __*Interval*__: choose between the default region and the custom region. If no bed file is provided, the only option is the default whole genome region.
  - __*Y axis*__: provide three measurements of the mutation count, namely the numeric sum of the mutation, mutations per Mb and the percentage among all mutations.
  - __*Filter by tumor\_f*__: choose the compare method and the threshold for filtering mutations.
