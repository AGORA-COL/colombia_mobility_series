# Process Mobility Series and Get Contact Data

## Overview

This repository contains scripts designed to analyze the mobility and shelter-in-place trends during the COVID-19 pandemic, with a focus on various departments in Colombia. The primary script, `get_intervention_file.ipynb`, processes community contact trends using mobility and shelter-in-place data sourced from Facebook.

The contact trend curves are smoothed using the Generalized Additive Models (GAMs) provided by the `pygam` package.

## Output Files

Outputs are saved in `output_folder/interventions/` and include:
- `interventions_covid_timevarying_community_baseline.csv`
- `interventions_covid_timevarying_community.csv`
- `interventions_covid_timevarying_shelter.csv`
- `interventions_covid_timevarying_shelter_lockdown.csv`

## Detailed Workflow

### Initialization
- `num_forecast_days`: A variable set to zero, indicating no additional days are forecasted by default. This can be adjusted to extend the prediction into the future.
- `selected_columns`: Specifies the columns to be included in the final output DataFrame, focusing on dates, replication indices, shelter trends, and geographical identifiers.

### Data Processing Loop
- Iterates through each department, loading corresponding shelter trend data from CSV files.
- Normalizes shelter trend data for consistency and prepares it for modeling.

### Defining Intervention Periods
- **Pre-Christmas Period**: Up to December 10, 2020. This period captures the behavior before the holiday season when movements might be less due to early pandemic responses.
- **Post-Christmas Period**: Starting from December 25, 2020. This focuses on the holiday impact and subsequent behavior, which is crucial for understanding changes in sheltering due to potentially increased social interactions during the holidays.
- Splits the dataset into two periods based on these dates for targeted analysis.

### Model Fitting and Prediction
- Fits a Generalized Additive Model (GAM) to each defined period separately to capture distinct trends.
- Predicts shelter trends for days within each period.

### Adjustments and Final Compilation
- After combining predictions from both periods, an additional adjustment is made for a reopening phase in June 2021, multiplying trends by 1.2 to reflect increased mobility post-lockdown.
- Values are capped to ensure they remain within plausible limits (0 to 1).
- The final DataFrame is prepared by merging predicted trends with the appropriate dates and departmental information.

### Output Preparation
- The resulting DataFrame containing all compiled and adjusted predictions is finalized for output, capturing significant trends and interventions across time.

## Intervention Periods
The script explicitly models the following periods for detailed analysis:
- **June Reopening Adjustment**: From June 8, 2021, onward. This adjustment acknowledges the reopening of activities and an expected increase in mobility and lesser sheltering as restrictions may have eased.
