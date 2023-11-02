# Incremental Load with Lookup

The other day, I wrote about overwriting data [using SSIS and demonstrated it by executing an SQL task to drop and recreate the destination](https://medium.com/@favboladale/a-step-by-step-guide-on-how-to-load-and-overwrite-data-from-sql-server-into-an-excel-file-using-a415cbaec269) when you re-execute to avoid duplicate data. It didn’t take so long to realize that this method is not scalable, especially for large datasets. In my pursuit of knowledge, I found a better method which is Incremental Load.

Incremental load is an ETL technique used to update a target database with only the new or changed data, reducing the processing time and resource usage. Instead of transferring the entire dataset, you only move the data that is new or modified.

# In this task, 

* I configured the Flat File Source to read data from my CSV file and the OLE DB Destination to write data to the SQL Server table where I want to perform the incremental load.

* Connected the output of my Flat File Source to the Lookup Transformation to validate the data in the source and perform a simple equi-join between the input and a reference data set. 

* Connected the "Lookup Match Output" from the Lookup Transformation to the Conditional Split to filter rows where the lookup operation finds a match to route data back to the existing OLE DB destination 

* Configured the Row Count transformation to count unmatched rows as they pass through a data flow and store the final count in a variable. Then route the data to OLE DB Destination to handle the unmatched rows.

* Configured the destination to perform the necessary updates to the SQL Server table for these unmatched rows.

Incremental load in SSIS using the Lookup Transformation, Conditional Split, and Row Count components is a powerful way to update specific records in your data warehouse efficiently. By identifying changed records and updating them, you can keep your data warehouse up to date without reloading the entire dataset. This approach is particularly useful when dealing with large datasets and frequent source data updates.

To learn more about Incremental Load and some of the scenarios where they come in handy, [click here](https://medium.com/@favboladale/incremental-load-in-ssis-using-lookup-transformation-real-world-scenarios-1a8e2b9a06f5)
