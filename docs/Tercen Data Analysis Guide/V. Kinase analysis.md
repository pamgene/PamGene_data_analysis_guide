## Introduction to Upstream Kinase Analysis (UKA)

Read about the overview of the UKA algorithm [here](../PamDx methods/2. UKA.md).

Two `UKA_apps`:
- UKA_app: legacy, deprecated, but supported. Please use the newer csUKA_app.
- csUKA_app: confidence scoring UKA algorithm. This is the latest way to do UKA, with practical benefits - the output is equivalent to the output of the UKA_app. Read about confidence scoring in the [UKA introduction](). 
## After which normalization should UKA be done?

In UKA, there is **no pairing option** available.

ComBat should only be done for UKA (or PCA, class prediction) **if:**

1. The design is **balanced** (conditions balanced over technical batches)

2. There is a batch effect **and** ComBat can remove it

If ComBat cannot remove the batch effect → UKA on log/VSN data.

```
Is there batch effect?
│
├── Yes → ComBat → UKA on log/VSN + ComBat-corrected data
│
└── No  → UKA on log/VSN data
```


## How to visualize the UKA output?

* **Flutter Volcano Plot**: Inside the (cs)UKA_app, there is a highly customizable volcano app which shows the direction of effect, specificity and the names of selected kinases.  
* **UKA dotplot**: run the UKA dotplot app in the workflow template, after UKA, to see more detailed information about the specificity and fold change of kinases grouped by kinase families. The dotplot also allows for direct comparison of significant kinases between contrasts. Set the specificity threshold at least to > 0.7!

The images the above apps create are downloadable in high quality and can be directly added to publications.

Check out the visualizations [here](../PamDx methods/2. UKA.md).

## Interpretation of kinases and phosphosites 

Read about the interpretation (pathway / network analysis) of kinases and phosphosites [here](../PamDx methods/3. Further insights to PamDx data.md).
## (cs)UKA app details

For information on (cs)UKA_app versions, what exactly changed, or how to fill out the wizard, read the readmes of the [UKA_app](https://github.com/pamgene/UKA_app) / [csUKA_app](https://github.com/pamgene/csUKA_app).