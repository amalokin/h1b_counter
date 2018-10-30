# Problem

This tool is designed to produce aggregated statistics of **certified** H1b-visa applications based on the data provided by the US Department of Labor and its [Office of Foreign Labor Certification Performance Data](https://www.foreignlaborcert.doleta.gov/performancedata.cfm#dis). Aggregation is done separately by two attributes: **occupations** and **employment states**. At most 10 highest ranking attribute values (i.e., occupations or states) are outputted along with the number of certified applications and the share of this attribute value (in percents rounded to the first decimal place).

The tool accepts as input a CSV (semicolon-delimeted) file named __`h1b_input.csv`__ in the __input__ subfolder. After a successful run, the script outputs two text files __top_10_occupations.txt__ and __top_10_states.txt__ into the __output__ subfolder. Filenames could be changed by editing the script file __run.sh__.

See [Run](README.md#run) for additional input file structure requirements.

# Approach

The tool consists of a Python 3.x script that uses a standard csv library to read an input dataset. The script initializes two dictionaries (occupations and states) with attribute values and counters as keys and values, respectively. Only certified applications are counted. After reading the entire input file, counts are sorted, tallied up, and percent shares are calculated. The generated output of atmost 10 highest ranking attribute values has the following schema: TOP_<OCCUPATIONS,STATES>;NUMBER_CERTIFIED_APPLICATIONS;PERCENTAGE (for occupations and states, respectively).

The script accepts different naming conventions for the used attributes (fields, variables, features). Please make sure that these attributes exist in your input data (i.e., rename the attributes in the data file if necessary):

__STATUS__ or __CASE_STATUS__ for application status
__LCA_CASE_SOC_NAME__ or __SOC_NAME__ for standardized occupation name
__LCA_CASE_WORKLOC1_STATE__ or __WORKSITE_STATE__ for employment state

Note:
FY2014 data specifies up to two working locations. The current version of the script considers the first location (__LCA_CASE_WORKLOC1_STATE__ is state of the first location) as the primary location for the analysis. However, if state of the first location is missing, the state of the second location (__LCA_CASE_WORKLOC2_STATE__) is considered, if available.

# Run 

Run __./run.sh__ to generate statistics based on the provided input dataset.
You can edit __run.sh__ to specify alternative paths and names for the python script, input dataset, top occupations text file, and top states text file.
