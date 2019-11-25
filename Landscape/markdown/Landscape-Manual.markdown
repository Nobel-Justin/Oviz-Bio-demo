# Introduction
The 'Landscape' visualization is frequently utilized to provide a systematic illustration of integrative data from multiple layers of batch samples, which are always compared to each other on certain attributes, such as genes and biological pathways mutated in cancers. This online 'Landscape' visualization is designed as a fixed part (histogram and gene-panels) with additional panels (e.g., age, gender, and histology). To visualize data, upload a **CSV** file in the *required* format and use sidebar options to customize the display.

# Landscape Data (CSV file)
The uploaded **CSV** file must match the *required* format. Several demo files from **References** are provided in <a href="https://github.com/Nobel-Justin/BTDraw" target="_blank">BTDraw</a> GitHub project.

- **header**<br/>
  The first line is header which contains information keywords.
- **samples**<br/>
  The first column lists **sample names** in each row, with the keyword '**SampleID**' in the header line. (*mandatory*)
- **gene-panel**<br/>
  Add columns for genes that you want to display. (*mandatory*)
  - The header line keyword follows '**g\_GeneName**' format, such as '**g\_<a href="http://genecards.org/cgi-bin/carddisp.pl?gene=TP53" target="_blank">TP53</a>**' and '**g\_<a href="http://genecards.org/cgi-bin/carddisp.pl?gene=PTEN" target="_blank">PTEN</a>**'.
  - Generally, the cell content (one gene in one sample) lists the mutations types, such as 'Mis', 'InDel', and 'Gain'.
  - Each cell allows multiple words (separator is semicolon), e.g., 'Mis;Loss'.
  - Use '-' for non-mutation, and 'N/A' for not-available.
  - Each cell allows maximum three words after de-redundancy. For example, 'Mis;Splice\_Site;Mis;Loss' is OK, while 'Mis;Splice\_Site;InDel;Mis;Gain' is not OK.
  - All words in '**g\_GeneName**' columns are summrized to calculate sample frequency in each gene, shown by one horizontal histogram at the '**left-area**' of **gene-panel**.
  - Generally, in cancer research, genes are always annotated with more information, such as their **pathway**, **GO** ontology, certain **comments**, and **P-value** or **Q-value** representing their mutated significance in batch samples. These information (if given) will be shown at the '**right-area**' of **gene-panel** (tags, matrix or histogram).
     - for **pathway**, add one row with keyword '**g\_Pathway**' in the first column cell and **Pathway** name (e.g., Adhesion) in other cells. Use 'N/A' for not-available. (tags)
     - for **GO** ontology, add one row with keyword '**g\_GO**' in the first column cell and **GO** name (e.g., Metabolic) in other cells. Use 'N/A' for not-available. (tags)
     - for **comments**, add one row with keyword '**g\_Comments\_xxx**' in the first column cell. Note that the '**xxx**' is the comments name (e.g., **g\_Comments\_<a href="https://cancer.sanger.ac.uk/cosmic" target="_blank">COSMIC</a>**). Content in other cells could ONLY be Boolen (Y or N), numeric values (e.g., 10 or 15.3), or 'N/A'. (matrix)
     - for **P-value**, add one row with keyword '**g\_P\_value**' in the first column cell and **_P_-value** (e.g., 0.001 or 3E-8) in other cells. Use 'N/A' for not-available. (histogram)
     - for **Q-value**, similar to **P-value**, but with another keyword '**g\_Q\_value**'. (histogram)
- **histogram**<br/>
  Add columns for stacked histogram to show attributes' distribution in webpage top.
  - The header line keyword follows '**ht\_AttributeName**' format, such as '**ht\_Missence**' and '**ht\_Truncated**'.
  - ONLY accepts numeric values (e.g., 15, 23.9 or 0.327) as cell content, and ONLY keeps **three** decimals.
  - We consider the whole CSV file as a complete matrix, please use '-' to fill the crossed cells between 'histogram' columns and 'gene-information' rows (if has, i.e., these mentioned above: **pathway**, **GO**, **comments**, **P-value**, and **Q-value**).
  - To display multiple histograms, use '**ht2\_xxx**' for the second, and '**ht3\_xxx**' for the third. Of course, '**ht1\_xxx**' and '**ht\_xxx**' are both for the first one.
  - Basically, histogram is simply named with their NO., e.g., '**ht2\_xxx**' corresponds to '**Histogram 2**'. Optionally, users can give name to each histogram. To do this, just make the header line keywords follow '**ht2(NewName)\_xxx**' format, then '**Histogram 2**' will be renamed as '**Histogram NewName**'. And the relevant section of this histogram in the sidebar will apply the new name.
  - Although it's not common, user can skip '**ht\_**' headed columns to avoid displaying histogram in the figure.
- **additional panels**<br/>
  Add columns to show additional panels (more information on samples) at the webpage bottom. Each panel might contain several attributes belonging to one category, e.g., panel 'Individual-Info' contains attributes like age, gender, smoking.
  - The header line keyword follows '**PanelName\_xxx**' format, e.g., '**Individual-Info\_age**' and '**Individual-Info\_gender**'. Note that please avoid '\_' in the **PanelName** string. Do not worry, the sidebar has options to change the displaying name of each panel to any string you want, such as '**Individual\_Info**' or '**Individual Info**'.
  - The cell content could be strings, numeric values, or 'N/A'.
     - __*strings*__: It is always used for *classifications*, e.g., gender ('Female' and 'Male'). We accept **maximum six** classifications besides 'N/A'. One attribute will be considered as *classifications* type, once string is found in cells of its column.
     - __*numeric values*__: It is always used for continuously distributed numeric attributes, e.g., age. The attribute will be shown by **gradient color** ranging from minimum value to maximum value. Considering that sometimes the numeric values may be used for *classifications*, e.g., tumor stages (1,2,3), OR, users just want to design groups corresponding to several value ranges, we provide options in the sidebar to state such usages. Note here the *classifications* sill needs to be subject to the **maximum six** requirements.
  - We have two resevered **PanelName** shortnames: '**mtif**' for '**Metadata**' and '**pw**' for '**Pathway**'. Of course, you can just use the full original name as your wish.
  - By default, all panels will be displayed from top to bottom on the page in the order in which they appear in the uploaded CSV file.

# Display Interactions
There are four types of interactions: *Highlights*, *Tooltips*, *External Link* and *Download*.

- **Highlights**<br/>
  When the mouse moves on the landscape figure, the column (sample) and row (gene or attribute) it points to will be highlighted.
- **Tooltips**<br/>
  Tooltips will show necessary information of object that the mouse points to.
  - __*histogram*__: SampleID, and value of the stacked area where the mouse points.
  - __*gene-panel*__
     - __*middle-area*__: SampleID, gene name, and relevant mutation types.
     - __*left-area*__: Gene name, and count of relevant (mutated) samples.
     - __*right-area*__: At __*gene-comments*__ matrix, Gene name, comments name, and comments value. At __*P/Q-value*__ histogram, Gene name, and P/Q-value.
  - __*other-panels*__: SampleID, attribute name and value.
- **External Link**<br/>
  - __*gene name*__: links to <a href="https://www.genecards.org/" target="_blank">genecard</a> search webpage.
  - __*pathway*__: links to <a href="https://www.kegg.jp/" target="_blank">kegg pathway</a> search webpage.
  - __*GO*__: links to <a href="http://amigo.geneontology.org/" target="_blank">amigo</a> search webpage.
- **Download**<br/>
  One SVG file will be generated when the '**Download**' button is clicked. Two themes are supplied: the default theme with dark background and the light theme with white backgroud. To use the light theme, please click the '**Light Theme**' button.

# Sidebar Functions
The sidebar provides diverse options to fine-tune the display, such as manage files, reset size and color, group and reorder objects, and so on.

- **Files**
  - __*Upload*__: upload landscape CSV file, and manage uploaded files. Note that duplicated file name will be alerted and given a random postfix.
  - __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered user (each account has certain storage).
  - __*File Sets*__: NOT available to this page.
- **General**
  - __*Common*__: reset column width; choose color for 'N/A' (effective globally).
  - __*Samples*__: reorder samples with series of selected conditions OR manually. We prepare a list of **conditions** (sorted or reversed sorted), such as SampleID (ASCII), Histogram values, and attributes in additional panels. Note that the well-known '**Bisect sorting**' of mutated genes in cancer research is also provided.
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

*Manual version=1.0*, written by Dr. JIA Wenlong on 2019-11-25.
