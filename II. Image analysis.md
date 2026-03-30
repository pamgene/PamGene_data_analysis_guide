## Tercen Structure 

### Teams > Projects

Access is determined at Team level (Teams can be shared with other members). Own Team is for personal use.

![Tercen home page: Projects view with recent and personal projects](Attachments/da_08.png)

![Tercen Teams page for pamgene: Members tab](Attachments/da_09.png)

---

### Upload Data to a Project

![Tercen project page: Tercen training with project actions and README](Attachments/da_10.jpg)

The zip file to upload should contain:
- `ImageResults/` folder (can contain multiple PS12 runs)
- `Array Layout.txt` (correct file, do not change name)
- Zip file name must **not contain a dot (.)**

---

#### Uploading Sample Annotation: Set Column Types

![Column type dialog: Barcode must be changed from numeric to character](Attachments/da_11.png)

- **Barcode** is numeric by default → must be set to **character** to join with IA output
- Check all other columns too — MS Excel sometimes changes column types
- If Sample name is a number, change it to character (numeric columns are used as y-axis factors)


---

### Add New Image analysis template
New worfklow → search for image_analysis templates. 
You can rename the template - useful if multiple of the same type exist in a project.

![New workflow dialog: selecting image_analysis_PTK_afterwash_template](Attachments/da_13.jpg)
### Image Analysis Overview - part 1.

A template contains different types of steps (indicated by icon in top left corner), e.g. 
* data upload step,
* operator, which changes the input data and produces an output. 


![IA workflow part 1: data file to ps12image + Image overview, then Grid afterwash, Gather, ReGrid](Attachments/da_14.jpg)

Overview of steps (details below)
1. Click data file → Run → select zip file
2. Run **Image overview** to see if everything is OK (see below)
3. Run **ReGrid** (previous steps run automatically) and do gridding 

---
### Image Overview

![Image overview operator](Attachments/da_15.png)
The Image overview is run by a **Shiny operator** (reactive — expects user interaction). Shiny operators are computation-intensive; if no interaction occurs, the operator stops (turns grey) after ~30 seconds.
Grey appearance means that the shiny operator has stopped. → just restart it.

Look at the image overview **afterwash** to see if there is anything concerning:

- Shadow
- Blurry arrays
- **Bubble** → in most cases still usable
- **Broken arrays** → must be discarded

If there is something concerning, look at prewash in the same image overview. If the issues are not present there, in the data analysis template, change the cycle number for afterwash (e.g. from 94 to 92 for PTK; in STK from 124 to 122 or earlier). Change it in all apps up to and including the QC_PTK / QC_STK step where there is a filter.

Stopping the PTK or STK experiment run and rerunning it causes a difference in cycle numbers. In IA, **filters must be adjusted in Grid, Regrid, and Select steps**. Filters are saved in workflows and can be brought into later steps ("Clone Project Filter").

![Working with filters](Attachments/da_21.png)

---
#### Examples of issues
Bubble on the side (still usable)
![Bubble on the side](Attachments/da_19.png)
Broken array → discard 
![Broken array](Attachments/da_20.png)


---

### Special Peptides on the Array Layouts

![PamChip fluorescence image: Functional peptides, Reference spots, Positive control labeled](Attachments/da_12.png)

| Type                 | Description                                                                                                  | Peptide names                   |
| -------------------- | ------------------------------------------------------------------------------------------------------------ | ------------------------------- |
| **REF**              | Grid reference spots (8): fluorescent peptides on sides of PamChip, help gridding                            | —                               |
| **Positive control** | Pre-phosphorylated peptides; check performance of detection system (e.g. antibody). Expectation: S100 > 1000 | PTK: ART_003; STK: pVASP, pTY3H |
| **Negative control** | No phosphosite (Y, S, or T)                                                                                  | PTK: EFS_246_258_Y253F          |
| **ART_004**          | Non-prephosphorylated counterpart of ART_003 (PTK) — artificial but phosphorylated by multiple kinases       | Similar: ART_025 (STK)          |

> **Note:** If a sample shows overall lower intensity, check the positive control. High signal in prephosphorylated peptides = enough antibody → lower intensity is biological. Low signal in prephosphorylated peptides = technical problem (insufficient antibody).


### Gridding

![ReGrid interface](Attachments/video_01.mp4)

The purpose of gridding is to find incorrectly placed grids and manually correct them.

> ⚠️ Gridding is done by a Shiny operator. **Always finish it and do not leave the page** — if it stops, all reviewed grids are lost!

---

### Image Analysis Overview — Part 2

![IA workflow part 2: ReGrid, Gather, Quantitation Type, Join, select, Export](Attachments/da_16.png)

Just **click Run All**.
- The **Join** step merges the IA output with the peptide enrichment (annotation) file
- The **Export** step: exported data is saved in the project folder and used as input for the next workflow

---

### The Peptide Enrichment File and the Join Step


![Peptide enrichment file](Attachments/da_17.png)

Each peptide sequence has 1 or more BLAST matches to a target protein with a `SeqSimilarity` value. `UniprotName` is the primary gene name (unique). Protein matches to peptides are not directly used in downstream data analysis but can be used to make hypotheses about which proteins could have been phosphorylated in the sample. 
![Join step: ds1.ID matched to enrichment ID, namespace js0](Attachments/da_18.png)

The **Join** step combines two datasets using a common key column (here: `ID`). The resulting table contains all factors (columns, rows and values) from both datasets.