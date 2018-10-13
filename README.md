# Comparison of effects of 10 anti-cancer drugs on three cancer metrics in mice
## Overview
## Getting Started
Python modules Pandas, Numpy, and MatPlotLib were used for data analyses and visualisation.

```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
```

To standardise the size and the colour schemes for each graph to be generated, the style was set to `ggplot` and the dimensions were set before any of the analyses were conducted.

```python
# Choose ggplot as style for plots
plt.style.use('ggplot')

# Size of plots
fig_size = plt.rcParams["figure.figsize"] # get current size
fig_size[0] = 12
fig_size[1] = 8
plt.rcParams["figure.figsize"] = fig_size # customise plot size
```

The data came from two .csv files: `mouse_drug_data.csv` and `clinicaltrial_data.csv`. These files were merged into a dataframe `mt_df`. Four of the ten treatments were used for the analyses; hence, the dataframe was further filtered so that only the four drug therapies of concern were included.

```python
# Load csv
mouse_drug_data_to_load = "mouse_drug_data.csv"
clinical_trial_data_to_load = "clinicaltrial_data.csv"

# Read the Mouse and Drug Data and the Clinical Trial Data
mouse_df = pd.read_csv(mouse_drug_data_to_load)
trial_df = pd.read_csv(clinical_trial_data_to_load)

# Combine the data into a single dataset (mt = mouse trial)
mt_df = pd.merge(mouse_df, trial_df, on = "Mouse ID")

# Display the data table for preview
mt_df.head()

# select the four drugs for comparison
list_of_drugs = ["Capomulin", "Infubinol", "Ketapril", "Placebo"]
mt_df = mt_df[mt_df["Drug"].isin(list_of_drugs)]
mt_df.head()
```

## Data Analyses
### Experiment Overview
The experiment followed a repeat measures design in which there were two treatments: `time` and `drug`. Mice were randomly assigned to each drug treatment and response variables, `tumour volume` and `number of metastatic sites`. A third response variable, `number of surviving mice`, was extracted based on the number of observations per time. A table was generated to provide an overview of the experimental set-up.

```python
# list of subjects and treatments
mouse = mt_df["Mouse ID"].unique()
drugs = mt_df["Drug"].unique()
time = mt_df["Timepoint"].unique()

# counts of subjects and treatments
mouse_popn = len(mouse)
no_drugs = len(drugs)
no_measurements = len(time)
no_samples = no_drugs * no_measurements

# summarise in a dataframe
overview = pd.DataFrame({"Number of Mice": mouse_popn,
                         "Number of Drug Treatments": [no_drugs],
                         "Number of Time Measurements": [no_measurements],
                         "Number of Samples": [no_samples]})
```                         

### Tumour Size Changes
### Tumour Response Over Time
### Metastatic Response to Treatment
### Survival Rates
## Resources