# READ_ME
This jupyter notebook compares 2 csv files of publication metadata pulled from Elsevier's Pure RIMS to isolate deleted records and write them out to a csv file for review. Please note that we're using the reporting module to pull research output data from pure which has determined the sort of odd data structure. You can get this same information from the Pure API--we just went the quick and dirty route with this one! If you end up using the API, please share! 

## 1. Generate your baseline data 

First, create a subfolder in the same directory you're saving your Python script in. This folder will contain all the research output data held in Pure at a particular point in time. I've named mine 20250320_ros. 

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

###  Using the Pure API 

If you don't have access to the reporting module you should be able to pull metadata from the API. You'll want to pull the same information outlined above from every research output in your instance. You can save these to individual CSV files as detailed above. For example, send a get call to the API asking it to return every RO with its pure ID and doi, and save the results to a csv file. 

## 2. Generate post QABO data for comparison
 
Wait a week or until you run another QABO job. Then, create another subdirectory in the same directory you've saved your python script. I've named mine 20250327_ros. Then, populate the new directory with data using your prefered method outlined above. Now you're ready to run the Python script and compare the publication data in your Pure instance after the QABO job runs. 

## 3. Run the script 

Launch the jupyter notebook. To do so, you'll need to have jupyter, pandas, and the OS library installed in a virtual environment on your machine. Prior to executing the cells, make sure you set the `this_dir` variable equal to the path on your computer where you've saved the subdirectories containing the publication csv files. 

Before you run the cells under the **Compare QABO Results** header, make sure to set up the `past_qabo` variable equal to the csv file of the compiled data from the past QABO job you created in the above section of the notebook, i.e. 20250327_ros.csv. Likewise, the `current_qabo` should be generated from the compiled data from the current QABO job created in the above section, i.e., 20250402_ros.csv. 

Continue running the notebook to generate a dataframe of research outputs that were present in the `past_qabo` log but are missing in the `current_qabo` log. These entries represent Pure IDs that have been removed from the system between QABO logs. You'll want to investigate these further to understand their deletion from the system. 






