Database code and documentation for the ITM instance of the Leaf clinical data explorer

Overview: the contents of this repository represent a first pass at populating an ITM version of Leaf which is common to participating institutions.  Emphasis on 'first pass' as this will likely require a number of iterations to work through the many nuances involved in finding an acceptable solution which meets the individual needs of each participant while, at the same time, meeting the overall technical and operational needs of the group.  That said, we have to start somewhere and this is as good a place as any.

Assumptions:
1. You have a Leaf 3.9.1 instance up and running w/ an MS SQL backend database.  While the name of the Leaf DB may differ depending on your specific configuration, suggestion to maintain consistency by naming the DB the following: LeafDB

2. You have a separate MS SQL database which contains clinical data from your institution in OMOP 5.3 format.  While the name of the OMOP DB may differ depending on your specific configuration, suggestion to maintain consistency by naming the DB the following: LeafClinDB

Step 1: Download, unzip, and run the following script to populate the Leaf GUI hierarchy: LeafDB_Concept.zip

Notes: 

1. If you already have an app.Concept table, you may comment out the create table SQL statement.
2. This script builds the concept hierarchy that you seen in the Leaf web interface.  Generated through a mostly-automated process, the content is based on the latest release of the UMLS Metathesaurus.  With each new release of the Metathesaurus, we can re-run the process which builds this SQL script, populate a revised app.Concept table, and publish the latest version.
3. The concept hierarchy includes a dynamically-build 'where clause' which looks for a specific concept_code in the OMOP data (see step 3).  One exception to searching on concept_code is the demographic data.  Current approach favors Leaf visualization options.  Further discussion needed around visualization scope within ITM Leaf instances.  

Step 2: Download, unzip, and run the following script to index the Leaf GUI search feature: LeafDB_Concept_Index.zip
	
Step 3: Download, unzip, and run the following script to associate Concept SQL Sets w/ SQL views: LeafDB_Concept_Index.zip

Note: If you already have an app.ConceptSQLSet table, you may comment out the create table SQL statement.
		
Step 4: Download, unzip, and run the following script to create SQL views in OMOP DB (LeafClinDB): LeafClinDB_Views.zip
	
Step 5: Download, unzip, and run the following script to create and populate OMOP DB concept table (LeafClinDB): LeafClinDB_Concept.zip

Notes:
1. If you already have a Concept table, you may comment out the create table SQL statement.
2. This script populates the latest concepts from OHDSI Athena (OMOP).  Generated through a mostly-automated process, the content is based on the latest release of the relevant OMOP vocabularies.  With each new release of a vocabulary, we can re-run the process which builds this SQL script, populate a revised Concept table, and publish the latest version.
	
For further discussion:
1. In scope?: visualization, age at encounter, telehealth

2. Performance tuning

