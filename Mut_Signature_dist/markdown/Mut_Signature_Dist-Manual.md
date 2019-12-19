##### [Download](https://raw.githubusercontent.com/Nobel-Justin/Oviz-Bio-demo/master/Mut_Signature_dist/demo_data/Mut_Signature_dist_demo.csv) and [Check](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/Mut_Signature_dist/demo_data/Mut_Signature_dist_demo.csv) the `official demo input`.

# Introduction
The 'Signature Dist' visualization shows the fraction of signatures within individual samples. It can also be used to show the fraction of signatures within several cancer types.

# Signature Dist Data (CSV file)
The uploaded **CSV** file must match the *required* format as specified below.<br/>
Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/Mut_Signature_dist/demo_data/Mut_Signature_dist_demo.csv).

- **header**<br/>
  The first line of the file should be a header that contains column names as keys. The header should follow the following format:

| Observations |  T38_Stomach | TCGA_BR_7197_01A_11D_2201_08_Stomach | TCGA_D7_5578_01A_01D_1600_08_Stomach |
|---|---|---|---|
| processes1  | 5.363950322  | 21.10195793 | 13.46599926 |

  - `Observations` takes the values of the names of signatures.
  - keys like `T38_Stomach` is the name of an individual sample. The number of keys is not limited.

- **rows**<br/>
  Each row in the file is the measure of a specified signature in each individual sample. Note that this measure does not have to be normalized.

# Display Interactions
There are three types of interactions: *Highlights*, *Scrolling* and *Download*.

- **Highlights**<br/>
    The bin being pointed to will be highlighted.
- **Scrolling**<br/>
    When the samples cannot be fitted in one page, a scroller will appear in the bottom and user can drag the scroller to view different samples.
- **Download**<br/>
  One SVG file will be generated when the '**Download**' button is clicked. The SVG file only captures the current view determined by the scroller. Only the default **Dark Theme** is available at this point.

# Sidebar Functions
The sidebar provides options to manage files and reorder samples.

- **Files**
  - __*Manage Files*__: checklist of CSV files uploaded previously, delete or download the CSV files.
  - __*Upload*__: upload Signature Dist CSV file. Note that the duplicated file name will be alerted and given a random postfix.
  - __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered users (each account has certain storage).
  - __*File Sets*__: NOT available to this page.
- **Settings**<br/>
  In settings, user can reorder samples by ascending or descending order of the sample name or the fraction of a certain signature.

*Manual version=1.0*, written by Miss. Li Shiying on 2019-12-19.
