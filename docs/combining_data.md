# Combining CEJST Data with Other Sources

This guide details how to combine data from this tool with other data sources using Python, including data sources which may use other geographies than Census tracts. Useful CEJST data sources can be found at [DATASETS.md](DATASETS.md) and the [Downloads page of the CEJST website](https://screeningtool.geoplatform.gov/en/downloads).

## Step 0: Setup

### Installations

First, ensure you have an appropriate version of Python installed. This guide will use Python 3, and while most features will likely work on Python 2.7, many libraries no longer ensure backwards compatibility with Python 2.7. You can check the version of Python installed on your computer by typing <code>python --version</code> into Powershell (Windows) or Terminal (Mac). The newest version of Python can be downloaded at [python.org/downloads](https://www.python.org/downloads/).

Next, ensure you have all necessary libraries. <code>pandas</code> is essential for database operations and will be used extensively in this guide. <code>pyprojroot</code> is quite useful for creating relative paths within the project directory. <code>numpy</code> and <code>scipy</code> (particularly <code>scipy.stats</code>) are both useful for statistical analysis, but are not strictly necessary. Likewise, <code>matplotlib</code> (particularly <code>matplotlib.pyplot</code>) can be used to create interesting visualizations, but is optional depending on your use case. Depending on your needs and preferred workflow, you may also want to use other libraries not listed here. Instructions for installing libraries can be found in the [Python documentation](https://docs.python.org/3/installing/index.html).

### Downloads

Download all required data into a subfolder within the project folder. The .csv format is generally easiest for usability and storage efficiency, though Excel files will work as well.

### Getting Started

If you've installed Python and all necessary libraries, and you have all your data downloaded and organized in the project folder, you're ready to get started! Open your favorite Python editor and move on to the next section.

## Step 1: Merging Geographies

The Justice40 dataset uses 2010 Census tracts as its geographic units. If the dataset(s) you wish to combine with the Justice40 data also use 2010 Census tracts, great! Feel free to skip this section and move on to [Step 2](#step-2-performing-a-data-merge). If you are using data with different geographic units, read below for information on how to use a crosswalk to obtain tract-level data.

### Obtaining a Crosswalk

A crosswalk is a file that matches two different geographic units together. To merge a dataset that does not use 2010 Census tract geographies with the Justice40 dataset, you will need a crosswalk to match the unit used by the first dataset with the 2010 Census tracts. The crosswalk will transform the "source geography" to the "target geography," so set the target geography to the unit that you would like in your final analysis. Generally, this is likely to be the geography used by the non-Justice 40 dataset. For example, if we wanted to determine the average number of Justice40 criteria exceeded for each elementary school district, we would set 2010 Census tracts as the source geography and elementary school districts as the target geography.

Crosswalks for most geographies can be downloaded from the [Missouri Census Data Center](https://mcdc.missouri.edu/applications/geocorr2014.html) or the [U.S. Census Bureau](https://www.census.gov/geographies/reference-files/time-series/geo/relationship-files.2010.html).

### Determining the Merge Rule and Weighting

A merge rule determines how to draw data from multiple source units when a target unit contains more than one source unit. For example, an elementary school district is likely to contain around a dozen or more census tracts. Mean and median are the most commonly used merge rules, though many other merge rules exist, including sum, count, min, max, and mode. Different use cases may require different merge rules, so pick one that works well for your data and needs.

In addition to a merge rule, you may wish to weight your data. Many geographic units, like Census tracts, do not have equal populations, so weighting a mean may provide a more accurate representation of target geographies than raw averages. Also note that source geographies may be split across multiple target geographies. For example, Census tract 0820.22 in Maricopa, Arizona is split between Litchfield Elementary School District, Littleton Elementary School District, and Pendergast Elementary School District. My crosswalk includes population for each intersection (259 people in that tract are within Litchfield Elementary School District, 1350 are within Littleton Elementary School District, and 2562 are within Pendergast Elementary School District). Some crosswalks only provide data for the source geography as a whole (4171 in Census tract 0820.22). In this case, you might approximate the weight for each intersection by dividing the total source geography population by the number of target geographies that include that source geography (4171 / 3 = 1390.33333...). If you do not have data for the population of each unit, you may not be able to establish population-based weights.

### Writing a Lookup Generator

Now that we've prepared our data and determined how we will use it, we will write a script to generate a lookup. A lookup is a table (likely in .csv format) with two columns: a set of keys, which correspond to the target geographies, and a value corresponding to each key. Common keys may be 5-digit zip codes, a state's postal abbreviation followed by two digits representing a given congressional district, or the name of the elementary school within the school district. The values would be the result of the merge rule for that target geography.

First, locate your crosswalk and the Justice40 data using pyprojroot, and read those files into DataFrames:

<pre><code>
import pandas, pyprojroot
 
#Make sure to change these path names to fit your project!
crosswalk = pyprojroot.here('./data/inputs/your_crosswalk_filename.csv')
justice40 = pyprojroot.here('./data/inputs/communities-timestamp.csv')
 
lookup = pandas.read_csv(crosswalk)
communities_df = pandas.read_csv(justice40)
</code></pre>

Next, 

[in progress]

## Step 2: Performing a Data Merge

[in progress]

<br>

##### This guide created by Robert Greene, Harvard University.
