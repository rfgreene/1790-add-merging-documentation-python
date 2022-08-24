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

In addition to a merge rule, you may wish to weight your data for cases where source units are split across multiple target units. For example, Census Tract 0820.22 in Maricopa County, Arizona contained three elementary school districts in 2014: Litchfield Elementary School District, Littleton Elementary School District, and Pendergast Elementary School District. The tract-to-elementary school district crosswalk contains an allocation factor, which represents the percentage of residents in that tract who live within a given elementary school district. Some crosswalks include allocation factors, but some do not. If an allocation factor is not available, land area may be used as a proxy for population allocation, with the (incorrect) assumption that population is evenly distributed across a census tract. 

To determine allocation factors based on land area divisions, first ensure you have a valid ArcPy license. Then, download shapefiles of both the [Justice40 dataset](https://screeningtool.geoplatform.gov/en/downloads) and the geographies of your secondary data source, which may be available as a [TIGER/Line shapefile](https://www.census.gov/cgi-bin/geo/shapefiles/index.php). From there, you can use <code>arcpy.analysis.TabulateIntersection</code> to generate the percentage of each "zone feature" that is occupied by a given "class feature". Since we wish to determine the percentage of a given source unit (e.g. Census tract) that is within each target unit (e.g. elementary school districts), we will set the zone features to source units and the class features to target units:

<pre><code>
import arcpy, pandas, pyprojroot

WRITE CODE HERE
</pre></code>

### Writing a Lookup Generator

Now that we've prepared our data and determined how we will use it, we will write a script to generate a lookup. A lookup is a table (likely in .csv format) with two columns: a set of keys, which correspond to the target geographies, and a value corresponding to each key. Common keys may be 5-digit zip codes, a state's postal abbreviation followed by two digits representing a given congressional district, or the name of the elementary school within the school district. The values would be the result of the merge rule for that target geography.

First, locate your crosswalk and the Justice40 data using pyprojroot, and read those files into DataFrames:

<pre><code>
import pandas, pyprojroot
 
crosswalk = pyprojroot.here('./data/inputs/your_crosswalk_filename')
justice40 = pyprojroot.here('./data/inputs/communities-2022-05-31-1915GMT.csv') #the timestamp on the file may be different depending on when you downloaded the data!
 
lookup = pandas.read_csv(crosswalk)
communities_df = pandas.read_csv(justice40)
</code></pre>

Next, 

[in progress]

## Step 2: Performing a Data Merge

[in progress]

<br>

##### This guide created by Robert Greene, Harvard University.
