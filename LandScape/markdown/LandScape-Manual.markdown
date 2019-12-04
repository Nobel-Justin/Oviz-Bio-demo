# Introduction
The 'LandScape' visualization is frequently utilized to provide a systematic illustration of integrative data from multiple layers of batch samples, which are always compared to each other on certain attributes, such as genes and biological pathways mutated in cancers. This online 'LandScape' visualization is designed as a fixed part (histogram and gene-panels) with additional panels (e.g., age, gender, and histology). To visualize data, upload a **CSV** file in the *required* format and use sidebar options to customize the display.

# LandScape Data (CSV file)
The uploaded **CSV** file must match the *required* format as specified below.<br/>
Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/LandScape/demo_csv/landscape_demo.csv). Additional demo files from the **[References](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/LandScape/markdown/LandScape-References.markdown)** are provided in the [GitHub](https://github.com/Nobel-Justin/Oviz-Bio-demo/tree/master/LandScape/demo_csv) project.

- **header**<br/>
  The first line of the file should be a header that contains column names as keys.
- **rows**<br/>
  Each row in the file should contain data for a sample.
- **samples** (`SampleID` column)<br/>
  The first column lists **sample names** in each row, with the key `SampleID` in the header line. (*mandatory*)
- **gene-panel** (`g_` columns)<br/>
  Add columns for genes that you want to display. (*mandatory*)
  - The header line keyword follows `g_[GeneName]` format, such as '**g_[TP53](http://genecards.org/cgi-bin/carddisp.pl?gene=TP53)**' and '**g_[PTEN](http://genecards.org/cgi-bin/carddisp.pl?gene=PTEN)**'.
  - Typically, the content of each table cell for one gene and one sample lists the mutations types, such as 'Mis', 'InDel', and 'Gain'. Use `-` for non-mutation, and `N/A` for not-available.
  - A cell may contain multiple mutation types (or values) using semicolon as separator, e.g., `Mis;Loss`.
  - Each cell allows three unique values at maximum. For example, `Mis;Splice_Site;Mis;Loss` is OK, while `Mis;Splice_Site;InDel;Mis;Gain` is not allowed because it contains 4 distinctive mutation types.
  - All values appeared in `g_` columns are summarized to calculate the sample frequency in each gene, which is shown by the horizontal histogram at the '**left-area**' of **gene-panel**.
  - Generally, in cancer research, genes are always annotated with more information, such as their **pathway**, **GO** ontology, certain **comments**, and **P-value** or **Q-value** representing their mutated significance in batch samples. These information (if given) will be shown at the '**right-area**' of **gene-panel** as tags, matrix or histogram.
     - for each **pathway**, add a row with key **`g_Pathway`** as the `SampleID` in the first column and specify the **Pathway** name (e.g., Adhesion) for each gene in other columns. Use `N/A` for not-available. (displayed as tags)
     - for each **GO** ontology, add a row with key **`g_GO`** as the `SampleID` in the first column and specify the **GO** name (e.g., Metabolic) for each gene in other columns. Use `N/A` for not-available. (displayed as tags)
     - for **comments**, add a row with key **`g_Comments_[name]`** in the `SampleID` column, where `[name]`  should be the comments name, e.g., **g\_Comments\_[COSMIC](https://cancer.sanger.ac.uk/cosmic)**. Values for comments _must_ be boolean (`Y` or `N`), numeric values (e.g., 10 or 15.3), or `N/A`. (displayed as matrix)
     - for **P-value**, add a row with key **`g_P_value`** in the `SampleID` column and **_P_-value** (e.g., 0.001 or 3E-8) for each gene in other cells. Use 'N/A' for not-available. (displayed as histogram)
     - for **Q-value**, all should be the same as **P-value** except that the key should be `g_Q_value`. (displayed as histogram)
- **histogram** (`ht` columns)<br/>
  It is possible to add multiple stacked histograms that show attributes' distribution at the top of the visualization.
  - Column names for histograms should follow the **`ht_[AttributeName]`** format, such as `ht_Missence` and `ht_Truncated`.
  - _Only_ numeric values (e.g., 15, 23.9 or 0.327) are allowed as cell content, and it keeps up to **three** decimals.
  - Since the whole CSV file as a complete matrix, please use `-` to fill the intersecting cells between 'histogram' columns and 'gene-information' rows (i.e., these mentioned above: **pathway**, **GO**, **comments**, **P-value**, and **Q-value**, if exist).
  - To display multiple histograms, use `ht2_[attr]` for the second one, `ht3_[attr]` for the third one, and so on. To allow flexibility, `ht1_` and `ht_` are both treated as the first one.
  - Basically, histogram is simply named with their NO., e.g., `ht2_` corresponds to '**Histogram 2**'. Optionally, users can assign a name to each histogram by adding a bracketed value after `ht`. For example, `ht2(NewName)_` will be named as '**Histogram NewName**' rather than '**Histogram 2**'. The cooresponding section of this histogram in the sidebar will also use this new name.
  - Although it's not common, user can omit `ht` columns to avoid displaying any histogram in the figure.
- **additional panels**<br/>
  Add columns to show additional panels (more information on samples) at the bottom of the visualization. Each panel might contain several attributes belonging to one category, e.g., panel 'Individual-Info' contains attributes like age, gender, smoking.
  - The column name key should follow the `[PanelName]_[AttributeName]` format, e.g., `Individual-Info_age` and `Individual-Info_gender`.<br/>
    Note that please avoid using '\_' in **PanelName**s. Do not worry about panel naming because the sidebar provides options to customize the displaying name of each panel, where users can choose their preferred name such as '**Individual\_Info**' or '**Individual Info**'.
  - The cell content could be strings, numeric values, or `N/A`.
     - __*strings*__: It is always used for *classifications*, e.g., gender ('Female' and 'Male'). We accept **maximum six** classifications besides `N/A`. An attribute will be considered as a *classifications* type as long as *strings* is found in any cell in its column.
     - __*numeric values*__: It is always used for continuously distributed numeric attributes, e.g., age. The attribute will be shown in **gradient color** ranging from the minimum value to the maximum value. Considering that sometimes the numeric values may be used for *classifications*, e.g., tumor stages (1,2,3), OR, users just want to design groups corresponding to several value ranges, we provide related options in the sidebar to cover such usages. Note here that the *classifications* sill needs to subject to the **maximum six** requirements.
  - We have two reserved **PanelName** short names: `mtif` for '**Metadata**' and `pw` for '**Pathway**'. Of course, you can just use the full original name as you wish.
  - By default, all panels will be displayed from top to bottom on the page in the order in which they appear in the uploaded CSV file.

# Display Interactions
There are four types of interactions: *Highlights*, *Tooltips*, *External Link* and *Download*.

- **Highlights**<br/>
  When the mouse moves on the LandScape figure, the column (sample) and row (gene or attribute) it points to will be highlighted.
- **Tooltips**<br/>
  Tooltips will show necessary information of object that the mouse points to.
  - __*histogram*__: SampleID, and value of the stacked area where the mouse points.
  - __*gene-panel*__
     - __*middle-area*__: SampleID, gene name, and relevant mutation types.
     - __*left-area*__: Gene name, and count of relevant (mutated) samples.
     - __*right-area*__: At __*gene-comments*__ matrix, Gene name, comments name, and comments value. At __*P/Q-value*__ histogram, Gene name, and P/Q-value.
  - __*other-panels*__: SampleID, attribute name and value.
- **External Link**<br/>
  - __*gene name*__: links to [genecard](https://www.genecards.org/) search webpage.
  - __*pathway*__: links to [kegg pathway](https://www.kegg.jp/) search webpage.
  - __*GO*__: links to [amigo](http://amigo.geneontology.org/) search webpage.
- **Download**<br/>
  One SVG file will be generated when the '**Download**' button is clicked. Two themes are supplied: the default theme with a dark background and the light theme with white background. To use the light theme, please click the '**Light Theme**' button.

# Sidebar Functions
The sidebar provides diverse options to fine-tune the display, such as manage files, reset size and color, group and reorder objects, and so on.

- **Files**
  - __*Manage Files*__: checklist of CSV files uploaded previously, delete or download the CSV files.
  - __*Upload*__: upload LandScape CSV file. Note that the duplicated file name will be alerted and given a random postfix.
  - __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered users (each account has certain storage).
  - __*File Sets*__: NOT available to this page.
- **General**
  - __*Common*__: reset column width; choose color for 'N/A' (effective globally).
  - __*Samples*__: reorder samples with a series of selected conditions OR manually. We prepare a list of **conditions** (sorted or reversed sorted), such as SampleID (ASCII), Histogram values, and attributes in additional panels. Note that the well-known '**Bisect sorting**' of mutated genes in cancer research is also provided.
  - __*Panels*__: reorder and rename additional panels.
- **Histogram**<br/>
  If there are multiple histograms, they will be shown in separate sections one by one in the sidebar.
  - __*Settings*__: hide this histogram; reset the maximum value of the Y-axis; reset the Y-axis label text; display SampleID along the X-axis.
  - __*Data*__: reorder the stacked groups; reset colors of the stacked groups.
- **Gene panel**
  - __*Main*__: reorder genes manually; reset the colors of mutation types; group gene comments; reset gradient colors and value ranges of gene comments.
  - __*Left*__: group mutation types; reset colors of mutation groups; reset maximum value of the axis; reset the axis label text.
  - __*Right*__: choose to show (P/Q-value, Pathway, GO, or None); reset maximum value of P/Q-value histogram axis; reset the threshold red line of P/Q-value histogram.
- **Additional panel(s)**<br/>
  If there are multiple additional panels, they will be shown in separate sections one by one in the sidebar.
  - __*Settings*__
     - for *classifications* attribute, reorder the categories in legend (left-side), and reset colors of each classification.
     - for *numeric value* attribute, reset gradient colors and value ranges, OR, enable groups displaying with customized value ranges.
  - __*Reorder*__: reorder attributes in this additional panel.

*Manual version=1.1*, written by Dr. JIA Wenlong and Mr. LI Hechen on 2019-12-02.
