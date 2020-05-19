
## Introduction

This repository contains a
[reportfactory](https://github.com/reconhub/reportfactory) automating the
production of research reports aiming to detect changes in COVID-19 incidence
using potential COVID-19 symptoms reported through England **NHS Pathways**.

The **NHS Pathways** dataset describes potential COVID-19 symptoms reported in 
England through 111 and 999 calls, and 111 online reports. It is updated 
daily (except weekends), and is freely available via the [NHS Digital website](https://digital.nhs.uk/data-and-information/publications/statistical/mi-potential-covid-19-symptoms-reported-through-nhs-pathways-and-111-online/latest).



<br>
<img src="data/images/line_bubbles.png" alt="line">



## Initial setup

When initialising the reportfactory, you can load all dependencies using:

``` r
## install dependencies (if first time running)
source("scripts/install_devel_packages.R")
reportfactory::install_deps()

``` 


<br>
<img src="data/images/line_bubbles.png" alt="line">




<br>
<img src="data/images/line_bubbles.png" alt="line">


## Updating data and analyses

The simplest way to update data and analyses is to run:

```r

reportfactory::update_reports(clean_report_sources = TRUE)

```

This will compile all reports in `report_sources/` in alphanumeric order, and
save all outputs to `report_outputs/`; actions include:

* download publicly available NHS pathways data
* process this data, save it in a `rds`
* create an `import_pathways()` function in `scripts/` which will automatically
  read the latest version of the data
* run all analyses based on the new data
* save all outputs in `report_outputs/`


See other sections for specific actions.





<br>
<img src="data/images/line_bubbles.png" alt="line">


## Specific actions

### Compiling the data cleaning report

Data can be updated using:

```r

reportfactory::compile_report("clean_latest_pathways_2020-05-13.Rmd",
                              clean_report_sources = TRUE)

```

This will compile a data cleaning report which will: 

* download publicly available NHS pathways data
* process this data, save it in a `rds`
* create an `import_pathways()` function in `scripts/` which will automatically
  read the latest version of the data
* save the html output of the report in `report_outputs/`




### Loading the latest extracted NHS Pathways dataset

When working within this reportfactory, the latest extracted **NHS Pathways** 
dataset can be loaded using a helper function. After loading the global factory
scripts (in `scripts/`) using `reportfactory::rfh_load_scripts()`, the data can 
be loaded with `import_pathways()`:

```r
## load the global factory scripts
reportfactory::rfh_load_scripts()

## load the latest extracted NHS Pathways dataset
pathways <- import_pathways()
pathways

```



### Compiling the analysis

```r
reportfactory::compile_report("nhs_pathways_analysis_2020-05-13.Rmd")
```

All outputs will be generated in the `report_outputs/` folder, classified
by report name (including the date of the report source, not of the
compilation), and then by date and time of compilation.

These outputs are then used to update the clean report.


### Generating the report 

Once the initial analysis has been locally compiled, the report can be 
generated using the `nhs_pathways_report_2020-05-13.Rmd` report in the
`report_sources/` folder. 

```r
reportfactory::compile_report("nhs_pathways_analysis_2020-05-13.Rmd")
```

Again, all outputs will be generated in the `report_outputs/` folder,
including the pdf report.




<br>
<img src="data/images/line_bubbles.png" alt="line">




## Locally updating datasets

### Updating the NHS Pathways dataset

If you wish to locally extract and clean the latest version of the
**NHS Pathways** data from the NHS website, this can be achieved with
the `clean_latest_pathways_2020-05-13.Rmd` report, in the
`report_sources/` folder. The report can be compiled using:

```r
reportfactory::compile_report("clean_latest_pathways_2020-05-13.Rmd")
```


### Updating the deaths dataset

Similarly, the **deaths** dataset can also be locally updated using the
`clean_latest_deaths_2020-05-13.Rmd` report.

```r
reportfactory::compile_report("clean_latest_deaths_2020-05-13.Rmd")
```


<br>
<img src="data/images/line_bubbles.png" alt="line">


