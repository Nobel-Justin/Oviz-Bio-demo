# Oviz-Bio-demo

Documents of <a href="https://bio.oviz.org/" target="_blank">Oviz-Bio</a>, a Platform for Bioinformatics Visualization

## LandScape
The 'LandScape' visualization is frequently utilized to provide a systematic illustration of integrative data from multiple layers of batch samples, which are always compared to each other on certain attributes, such as genes and biological pathways mutated in cancers. To visualize data, a CSV file in the required format is needed.
### demo_csv
Several demo CSV files are provided.
- `landscape_demo.csv` is the official demo CSV file.
- `PMIDxxx.Figx.landscape.csv` files to present LandScape instances in published papers (see <a href="https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/LandScape/markdown/LandScape-References.markdown" target="_blank">Reference</a>).
### markdown
Markdown files of LandScape analysis page on Oviz-Bio Platform.
- Manual
- References
- About

## SV:Heatmap
Linkage heatmap is an useful method to visualize read linkage patterns on SV event, especially in studies with long-range sequencing data, such as 10x linked-reads. We apply the "SV: Heatmap" visualization to display the heatmap matrix based on sequencing reads linkage between two local windowlized regions of SV case. The color depth of each cross-linked window pair is proportional to the number of linkages. Along the chromosome coordinate axis of the heatmap matrix, annotation information is added, such as Ensembl genes. To visualize data, upload a **TXT** file in the *required* format, and then use sidebar options to adjust heatmap color scheme and choose other SVs to display if uploaded data contains multiple cases.

### demo_data
Two demo **TXT** files are provided.
- `10x.txt` stores the shared 10x barcodes linkage matrix.
- `pair_end.txt` stores the shared pair end reads linkage matrix.
### markdown
Markdown files of SV:Heatmap analysis page on Oviz-Bio Platform.
- Manual
- References
- About

## SV:Reads Support
The "SV:Reads Support" visualization is frequently utilized to provide the detail illustration of supporting split reads for given SV events. To visualize data, a **TXT** file in the required format is needed.
### demo_data
Two demo **TXT** files are provided, `simu.junc.reads.txt` and `junc.reads.txt` store information of supporting split reads for given SV events.
### markdown
Markdown files of SV:Reads Support analysis page on Oviz-Bio Platform.
- Manual
- References
- About
