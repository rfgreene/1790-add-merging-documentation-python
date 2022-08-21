# Combining CEJST Data with Other Sources

This guide details how to combine data from this tool with other data sources using Python, including data sources which may use other geographies than Census tracts. Useful CEJST data sources can be found at [DATASETS.md](DATASETS.md) and the [Downloads page of the CEJST website](https://screeningtool.geoplatform.gov/en/downloads).

## Step 0: Setup

### Installations

First, ensure you have an appropriate version of Python installed. This guide will use Python 3, and while most features will likely work on Python 2.7, many libraries no longer ensure backwards compatibility with Python 2.7. You can check the version of Python installed on your computer by typing <code>python --version</code> into Powershell (Windows) or Terminal (Mac). The newest version of Python can be downloaded at [python.org/downloads](https://www.python.org/downloads/).

Next, ensure you have all necessary libraries. <code>pandas</code> is essential for database operations and will be used extensively in this guide. <code>pyprojroot</code> is quite useful for creating relative paths within the project directory. <code>numpy</code> and <code>scipy</code> (particularly <code>scipy.stats</code>) are both useful for statistical analysis, but are not strictly necessary. Likewise, <code>matplotlib</code> (particularly <code>matplotlib.pyplot</code>) can be used to create interesting visualizations, but is optional depending on your use case. Depending on your needs and preferred workflow, you may also want to use other libraries not listed here. Instructions for installing libraries can be found in the [Python documentation](https://docs.python.org/3/installing/index.html).

### Downloads

Download all required data into a subfolder within the project folder. For this example we will use the Communities List Data found on the [CEJST website](https://screeningtool.geoplatform.gov/en/downloads) and the 2019 School District Boundaries offered by the [National Center for Educational Statistics](https://nces.ed.gov/programs/edge/Geographic/DistrictBoundaries).

### Getting Started

If you've installed Python and all necessary libraries, and you have all your data downloaded and organized in the project folder, you're ready to get started! Create a new Python file, open your favorite Python editor, and move on to the next section.

## Step 1: Merging Geographies

The Justice40 dataset uses 2010 Census tracts as its subunits. If the dataset(s) you wish to combine with the Justice40 data also use 2010 Census tracts, great! Feel free to skip this section and move on to [Step 2](#step-2-performing-a-data-merge). If you are using data with different subunits, read below for information on how to use a crosswalk to obtain tract-level data.

### Determining the Merge Rule

## Step 2: Performing a Data Merge

