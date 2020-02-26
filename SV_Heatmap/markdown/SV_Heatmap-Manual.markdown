##### [Download](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SV_Heatmap/demo_data/pair_end_resolution25_ALK-KIF5B.txt) the `official demo input`.

Additional demo files are provided in the [GitHub](https://github.com/Nobel-Justin/Oviz-Bio-demo/tree/master/SV_Heatmap/demo_data) project.

# Introduction
The "SV: Heatmap" may demonstrate the read and barcode linkage of SV events for WGS pair-end reads and 10x linked reads, respectively. We adopt heatmap to manifest the sequential read/barcode linkages on the surrounding region of the two breakpoints for the given SV event.  As indicated in the color bar, the darker the heatmap entry, the more supported ties. Users may upload the specified input file that holding several SV events, then manage the sidebar to customize the heatmap color scheme and select the desired SV event to present.

# SV:Heatmap Data (TXT file)
The uploaded **TXT** file must match the *required* format. Several demo files from **References** are provided in the [GitHub](https://github.com/Nobel-Justin/Oviz-Bio-demo/tree/master/SV_Heatmap/demo_data) project.

User can generate the `heatmap.txt` files using `linkage_heatmap.py` with **BAM** file and [SvABA](https://github.com/walaj/svaba) generated sv **VCF** file. Please check https://github.com/paprikachan/ComplexSV for source code and usage of `linkage_heatmap.py`.


The demo output file `demo_data/10x.txt` starts with "sv" section.

```
#sv
chr11	76139879	+	chr2	63328429	-   VARTYPE=BND:TRX-tt
```

It stores the breakpoints information of SV event, ordered by:

| chrom_5p |  bkpos_5p |  strand_5p | chrom_3p |  bkpos_3p |  strand_3p | meta_info |
|---|---|---|---|---|---|---|
| chr11  | 76139879  | + | chr2  | 63328429  |- | VARTYPE=BND:TRX-tt |

where `chrom_5p`, `bkpos_5p`, `strand_5p` respectively stands for the chromosome, position, strand of 5' breakpoint, and `chrom_3p`, `bkpos_3p`, `strand_3p` respectively stands for the chromosome, position, strand of 3' breakpoint. `meta_info` stores the meta information, such as the variation type of the SV.

The second section is "heatmap" section, it starts with the comment:

```
#heatmap    linkage_type=10x barcode
```

where `linkage_type` specifies the type of read linkage used to count, now we support to show "10x barcode" and "Pair End" linkage type.

For a SV event with two breakpoints, expand the breakpoint with `1000bp`, we can generate four region pairs and their shared linkage count matrix.

Region pair 1: vertical region is `(bkpos_5p-1000bp, bkpos_5p+1000bp)` and horizontal region is `(bkpos_5p-1000bp, bkpos_5p+1000bp)`.

```
v=chr2:63327429-63329429	h=chr2:63327429-63329429	resolution=100	axis=left-top
63.0,34.0,35.0,32.0,21.0,...
34.0,82.0,56.0,37.0,36.0,...
35.0,56.0,104.0,47.0,40.0,...
32.0,37.0,47.0,84.0,40.0,...
21.0,36.0,40.0,40.0,83.0,...
...
```

Region pair 2: vertical region is `(bkpos_5p-1000bp, bkpos_5p+1000bp)` and horizontal region is `(bkpos_3p-1000bp, bkpos_3p+1000bp)`.

```
v=chr2:63327429-63329429	h=chr11:76138879-76140879	resolution=100	axis=right-top
8.0,14.0,7.0,8.0,11.0,...
9.0,17.0,13.0,14.0,13.0,...
14.0,16.0,17.0,22.0,15.0,...
9.0,14.0,11.0,13.0,13.0,...
8.0,13.0,13.0,16.0,13.0,...
...
```

Region pair 3: vertical region is `(bkpos_3p-1000bp, bkpos_3p+1000bp)` and horizontal region is `(bkpos_5p-1000bp, bkpos_5p+1000bp)`.

```
v=chr11:76138879-76140879	h=chr2:63327429-63329429	resolution=100	axis=left-bottom
8.0,9.0,14.0,9.0,8.0,...
14.0,17.0,16.0,14.0,13.0,...
7.0,13.0,17.0,11.0,13.0,...
8.0,14.0,22.0,13.0,16.0,...
11.0,13.0,15.0,13.0,13.0,...
...
```

Region pair 4: vertical region is `(bkpos_3p-1000bp, bkpos_3p+1000bp)` and horizontal region is `(bkpos_3p-1000bp, bkpos_3p+1000bp)`.

```
v=chr11:76138879-76140879	h=chr11:76138879-76140879	resolution=100	axis=right-bottom
80.0,52.0,27.0,42.0,33.0,...
52.0,140.0,56.0,61.0,50.0,...
27.0,56.0,124.0,72.0,50.0,...
42.0,61.0,72.0,152.0,57.0,...
33.0,50.0,50.0,57.0,112.0,...
...
```







# Display Interactions
There are two types of interactions: *Tooltips* and *Download*.

- **Tooltips**
  Tooltips will show necessary information of object that the mouse points to.
  + __*SV Point*__: Chromosome of 5' breakpoint, position of 5' breakpoint, chromosome of 3' breakpoint, position of 3' breakpoint, and variation type of SV event.
  + __*Heatmap Window*__: Window start and end position of 5' and 3' region.
- **Download**
  One SVG file will be generated when the '**Download**' button is clicked. Two themes are supplied: the default theme with dark background and the light theme with white backgroud. 
- **Light Theme**
  To use the light theme, please click the '**Light Theme**' button.

# Sidebar Functions
The sidebar provides diverse options to fine-tune the display, such as manage files, reset color, select SV event, show gene annotation and so on.

- **Files**
  + __*Upload*__: upload heatmap TXT file, and manage uploaded files. Note that duplicated file name will be alerted and given a random postfix.
  + __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered user (each account has certain storage).
  + __*File Sets*__: NOT available to this page.
- **Settings**
  + __*Color for Min Value*__: reset color of min value.
  + __*Color for Max Value*__: reset color of max value.
  + __*Show gene annottaions*__: tick to show gene annotations.
- **Genes**
  Show 5' and 3' gene if available, user can select desired gene transcript.
- **SV Points**
  A table of SV events can be selected to visualize. Table headers `Gp`, `5'`, `Pos`, `3'`, `Pos`, `Type` respectively refer to the SV group id, chromosome of 5' breakpoint, position of 5' breakpoint, chromosomeof 3' breakpoint, position of 3' breakpoint, variation type of SV event. "blue" and "yellow" stands for positive and negative strand respectively. **Users can click the header to reorder the table.**

*Manual version=1.0.3*, written by Miss. CHEN Lingxi on 2020-02-26.
