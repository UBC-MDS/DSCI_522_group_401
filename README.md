
# Medical Expense Data Analysis and Predictive Modeling

  - author: Karanpal Singh, Sreejith Munthikodu, Sirine Chahma

## About

Knowing the estimated medical expenses in advance is very critical for
insurance companies to set their yearly premiums to beneficiaries. They
should make sure that the amount they spent on beneficiaries is less
than the total premium they receive. Using a predictive model that
predicts the expected medical expense of a customer, the insurance
companies get an estimate of how much premium to charge on each segment
of customers such that the cost results in reasonable profit to the
company. Using such predictive models, they can identify potentially
high-risk customers and charge a higher premium from such customers. In
this project, we attempt to build a regression model that will help us
predict the medical expenses of a person given information such as age,
sex, number of children, smoking habits, and the region where the person
is from. In the process, we are also interested in figuring out if there
is a significant difference in expenses between smokers and non-smokers,
and between males and females. Our hypothesis tests suggest that at 0.05
significance level there is significant evidence to conclude that
smokers incur more medical expenses than non-smokers. Also, there is
statistically no significant evidence to conclude that the medical
expenses of men and women are different. For our predictive model, after
trying different regression models, we found that the decision tree
regressor performs the best on our data. Using our final tuned model, we
achieved satisfying results on the test data set, with a
![R^2](https://latex.codecogs.com/png.latex?R%5E2 "R^2") score of 0.826.

The Data we are using for this analysis is used in the book Machine
Learning with R by Brett Lantz(Lantz 2013); which is a book that
provides an introduction to machine learning using R. All of these
datasets are in the public domain. The data explain the cost of a small
sample of USA population Medical Insurance Cost based on attributes like
age, sex, number of children etc. Additional information about this data
can be found
[here](https://gist.github.com/meperezcuello/82a9f1c1c473d6585e750ad2e3c05a41).

## Report

  - The final report can be found
    [here](https://github.com/UBC-MDS/DSCI_522_group_401/blob/master/reports/medical_expense_analysis.md).
  - Exploratory Data Analysis can be found
    [here](https://github.com/UBC-MDS/DSCI_522_group_401/blob/master/notebooks/EDA.ipynb).

## Usage

To replicate the analysis, clone this GitHub repository, install the
[dependencies](#dependencies) listed below, and run the following
command at the command line/terminal from the root directory of this
project:

    make all

To reset the repo to a clean state (which means with no intermediate or
results files), run the following command at the command line/terminal
from the root directory of this project:

    make clean

You could also run the following command at the command line/terminal
from the root directory of this project:

    # Download the data
    python get_data.py --url=https://gist.githubusercontent.com/meperezcuello/82a9f1c1c473d6585e750ad2e3c05a41/raw/d42d226d0dd64e7f5395a0eec1b9190a10edbc03/Medical_Cost.csv --file_location=../../data/original/medical_cost_data.csv

    # Split the data
    Rscript src/data/pre_processing_data.R --input_file=data/original/medical_cost_data.csv --output_dir=data/processed

    # EDA Script
    python src/visualization/eda.py --input_data=data/processed/medical_cost_data_train.csv --output_location=reports/figures

    # Inferences
    Rscript src/inferences/inferences.R --input_file=data/original/medical_cost_data.csv --output_dir=reports/tables/

    # Predictive Modeling
    python src/models/train_predict_medical_expense.py --training_data_file_path="data/processed/medical_cost_data_train.csv" --test_data_file_path="data/processed/medical_cost_data_test.csv" --results_file_location="reports"

    # Report
    Rscript -e "rmarkdown::render('reports/medical_expense_analysis.Rmd')"

## Dependencies

  - Python 3.7.3 and Python packages:
      - docopt==0.6.2
      - pandas==0.24.2
      - feather-format==0.4.0
      - scikit-learn==0.22.1
      - altair==4.0.0
      - scipy==1.2.3
      - matplotlib==3.2.1
      - selenium –3.141.0
  - R version 3.6.1 and R packages:
      - knitr==1.26
      - testthat==2.3.1
      - broom==0.5.3
      - feather==0.3.5
      - tidyverse==1.2.1
      - caret==6.0-84
      - ggridges==0.5.1
      - ggthemes==4.2.0
      - selenium 3.141.0
  - ChromeDriver 79.0.3945.36

# References

<div id="refs" class="references">

<div id="ref-source">

Lantz, Brett. 2013. *Machine Learning with R*. PACKT Publishing.

</div>

</div>
