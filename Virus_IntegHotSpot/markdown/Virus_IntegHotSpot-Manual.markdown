##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/Virus_IntegHotSpot/demo_data/Virus_IntegHotSpot_demo.csv) and [Check](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/Virus_IntegHotSpot/demo_data/Virus_IntegHotSpot_demo.csv) the `Virus Integration CSV input`.

# Introduction
Nearly 20% of human cancers are related to viral infection, especially the oncovirus, which is found commonly integrate into the host genome, and cause genome instability and higher risks to develop cancers, such as human papillomavirus (HPV) in cervical carcinoma and hepatitis B virus (HBV) in liver cancer. So far, many viral integration hotspot genes are found in oncovirus studies. We implement the `Virus: Integ HotSpot` visualization to illustrate the oncovirus integrated hotspot of group samples in a genome browser way. Oviz-Bio automatically calculates the hotspot genomic regions from the virus integration list submitted by users.

# Input Files

## Virus Integration CSV File

Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/Virus_IntegHotSpot/demo_data/Virus_IntegHotSpot_demo.csv).<br/>
The uploaded **CSV** file must match the *required* format as specified below.

- **header**<br/>
  The header should follow the following format:

| #SampleID |  Chr |  Position | Strand |  JR_count |
|---|---|---|---|---|---|
| T9202 | chr8 | 128276003 | - | 13 |

# Display Interactions

- **Tooltips**<br/>
  Tooltips will show necessary information of object that the mouse points to.
  - __*integraion*__: SampleID, integration position, junction strand.
  - __*gene*__: transcript name, interval.
  - __*exon*__: NO., interval.
  - __*annotation*__: details of objects displayed in the annotation panel.
- **Zoom in/out**<br/>
  the main display level can be zoomed in/out via mouse wheel.
- **Pages**<br/>
  click 'Prev' or 'Next' to go to other hotspot loci.
- **Download**<br/>
  One SVG file will be generated when the '**Download**' button is clicked. Two themes are supplied: the default theme with a dark background and the light theme with white background. To use the light theme, please click the '**Light Theme**' button.

# Sidebar Functions

- **Files**
  - __*Manage Files*__: checklist of files uploaded previously, delete or download files.
  - __*Upload*__: upload files. Note that the duplicated file name will be alerted and given a random postfix.
  - __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered users (each account has certain storage).
  - __*File Sets*__: save multiple files together as a file set. User can also choose to apply one file set previously saved.
- **Data**
  - __*Hotspots*__: select to show integrations in current page.
  - __*Genes*__: select transcript for each gene or disable.
  - __*Leftouts*__: check integrations that cannot form hotspot region.
- **Annotation Panel**<br/>
  select annotation database.
- **Setting**<br/>
  - reset the interval size used in connecting integrations to form hotspot loci.
  - select hotspot locus to display.
  - select either strand to show genes.
  - merge gene track to get condensed displaying.
  - show one sample only one time in current page.
  - display gene name rather than transcript name.
  - display all genes.
  - color the integration icon with junction strand.
  - show the leftout integrations in addtional pages.

*Manual version=1.0*, written by Dr. JIA Wenlong on 2019-12-19.
