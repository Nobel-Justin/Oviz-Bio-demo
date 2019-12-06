# Introduction
The 'Signature' visualization is wildly used in mutational signature analysis. It shows the signature profile with the conventional 96 mutation type classification. The classification first divides mutations into six substitution subtypes, namely C>A, C>G, C>T, T>A, T>C, and T>G. Subsequently, taking the information from the 5' to 3' adjacent bases lead to said 96 possible mutation types. Moreover, we compare each signature with all recorded signature references in the COSMIC database by the cosine similarity test. The top three similar signature references are listed with percentage of similarity. In particular, possible sequencing artifacts in the signature references are shown in pink while others in blue.

# Signature Data (CSV file)
The uploaded **CSV** file must match the *required* format as specified below.<br/>
Check the official demo input [here](https://github.com/Nobel-Justin/Oviz-Bio-demo/blob/master/SNV_Signature/demo_data/signature.csv).
- **header**<br/>
  The first line of the file should be a header that contains column names as keys. The header should follow the following format:

    | types |  subtypes | processes1 | processes2 |  processes3 | processes4 | processes5 |
    |---|---|---|---|---|---|---|
    | C>A  | ACA  | 0.000353018 | 0.000284683 | 0.000401966 | 0.002938016 | 0.002984077 |

    - `types` and `subtypes` respectively stand for the six substitution subtypes and the adjacent bases. The values of the two keys should also follows the format shown above.
    - `processes1` to `processes5` each stands for a signature. The name, such as `processes1`, is not fixed and can be replaced by any other text. The number of signatures is not limited.

- **rows**<br/>
  Each row in the file is one of the 96 mutation types.

# Display Interactions
There are three types of interactions: *Highlights*, *External link* and *Download*.

- **Highlights**<br/>
    When the mouse moves on the signature profile, the corresponding bin will be highlighted. Also, when the mouse moves on the three most similar signature references, the corresponding reference label will be highlighted.
- **External link**<br/>
    Each reference label links to the [COSMIC SBS Signatures](https://cancer.sanger.ac.uk/cosmic/signatures/SBS/) search webpage.
- **Download**<br/>
  One SVG file will be generated when the '**Download**' button is clicked. Only the default **Dark Theme** is available at this point.

# Sidebar Functions
The sidebar provides options to manage files.

- **Files**
  - __*Manage Files*__: checklist of CSV files uploaded previously, delete or download the CSV files.
  - __*Upload*__: upload Signature CSV file. Note that the duplicated file name will be alerted and given a random postfix.
  - __*Choose*__: choose files uploaded previously. Note that this function is ONLY available to registered users (each account has certain storage).
  - __*File Sets*__: NOT available to this page.
