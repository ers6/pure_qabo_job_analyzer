# READ_ME
This jupyter notebook compares 2 csv files of publication metadata pulled from Elsevier's Pure RIMS to determine to isolate deleted records and write them out to a csv file for review. 

## 1. Generate your data for comparison

First, create a subfolder in the same directory you're saving your Python script in. This folder will contain all the research output data held in Pure at a particular point in time. I've named mine 20250425_ros. 

Next, you'll need to populate your folder with data. We gather publication metadata using the reporting module in Pure. If you do not have access to the reporting module, you can still produce a list of research outputs using the Pure API. 

### Using Reporting: 
1. Go into the reporting module in Pure. 
2. For your driver, select "Research Outputs."
3. For fields, select the "Pure ID" field and the title field. 
4. Next, add another sheet. While we could add all the fields we're interested in to this one sheet, the file would be too large to download. Creating separate sheets for each piece of metadata of interest and joining them together on common Pure ID fields will allow you to download large amounts of metadata relatively quickly. 

You'll need to create a single sheet and repeat this process for each piece of metadata you're interested in. for example, if you want to know the publication year of an RO, you should create a new sheet, select the "Pure ID" and the "year" for your metadata. This particular notebook is set up to analyze the following fields: 
- title : select Pure ID and Title
- year: select Pure ID and Year
- publisher: select Pure ID Publisher
- issn: select Pure ID and Journal ISSN (if there is no ISSN this will be left blank)
- journal title: select Pure ID and Journal Title (if there is no Journal Title this will be left blank)
- dois: select Pure ID and DOIs(Digital Object Identifiers)
- created_date: select Pure ID and created date
- last_modified: select Pure ID and Last modified date
- scopus_id: select Pure ID and Publication import ID (note that if imported from a source other than scopus, this will not be a scopus ID)
- qabo_id: select Pure ID and Additional source IDs- make sure that you select "Wide Preview" 
- persons: select Pure ID and Person- make sure that you select "Wide Preview"

After you create a sheet, export it to csv file and save it in the subdirectory you created in the above step. 


##  Using the Pure API 

