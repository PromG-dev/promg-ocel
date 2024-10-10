# Importing OCED format into EKG

## Description

This repository enables an import from the Object-Centric Event Data (OCED) format produced by Konekti into the Event Knowledge Graph (EKG).
For this, we use a python script that can automatically read the JSON files produced by Konekti and import the events, objects and the relationships in between.
Currently, it is not (yet) supported that the state of an object may change.


---------------------

## Installation
### Neo4j
The code assumes that Neo4j is installed.

Install [Neo4j](https://neo4j.com/download/):

- Use the [Neo4j Desktop](https://neo4j.com/download-center/#desktop)  (recommended), or
- [Neo4j Community Server](https://neo4j.com/download-center/#community)

### PromG
PromG should be installed as a Python package using pip
`pip install promg==2.2.1`.

The source code for PromG can be found [PromG Core Github repository](https://github.com/PromG-dev/promg-core).

---------------------

## Getting Started

1. Create database or connect to a database.
   <details> 
      <summary> Click here for step-by-step instructions  </summary>

    1. Select `+Add` (Top right corner)
    2. Choose Local DBMS or Remote Connection with :exclamation: version 5.9.
    3. Follow the prompted steps (the default password we assume is 12345678)

</details>

> [!IMPORTANT]  
> The code only works Neo4j databases up to v5.17.0.

2. Configure the database settings (only do this step when you created a local database)
   1. Install APOC: `Neo4j APOC Core library` (see https://neo4j.com/labs/apoc/)
      <details>
         <summary>Click here for step-by-step instructions</summary>
      
      1. Select the database in Neo4j desktop 
      2. On the right, click on the `plugins` tab > Open the `APOC` section > Click the `install` button
      3. Wait until a green check mark shows up next to `APOC` - that means it's good to go!
      
    </details>

   2. Install APOC: `Neo4j APOC Extended library`
      <details>
        <summary>Click here for step-by-step instructions</summary>
   
      1. Download the [appropriate release](https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases) (same version numbers as your Neo4j version)
          1. Look for the release that matches the version number of your Neo4j Database.
          2. Download the file `apoc-[your neo4j version]-extended.jar`
       2. Locate the `plugins` folder of your database:  
          Select the Neo4j Server in Neo4j Desktop > Click the three dots > Select `Open Folder` > Select `Plugins`
       4. Put `apoc-[your neo4j version]-extended.jar` into the `plugins` folder of your database
       5. Restart the server (database)
      
      </details>

   3. Configure extra settings using the configuration file `$NEO4J_HOME/conf/apoc.conf`
      <details>
        <summary>Click here for step-by-step instructions</summary>
      
      1. Locate the `conf` folder of your database  
         Select the Neo4j Server in Neo4j Desktop > Click the three dots > Select `Open Folder` > Select `Conf`
      2. Create the file `apoc.conf`
      3. Add the following line to `apoc.conf`: `apoc.import.file.enabled=true`.
   
      </details>

    
3. Save the data sets
   <details> 
      <summary> The datafile `eventstore.json` should be stored in the folder `\data`.  </summary>

    TODO, add data source
    </details>
   4. Create and store the configuration file `config.yaml` in the root directory
       <details>
       <summary> Click here for example `config.yaml` file </summary>
      Create a `config.yaml` file and store in the root directory.
      The file should be formatted as follows:

      ```yaml
           # Database Credentials and Information
       db_name: "neo4j"
       uri: "bolt://localhost:7687"
       user: "neo4j"
       password: "12345678"
    
       # Dataset information
       dataset_name: "KonektiEventStream"
       semantic_header_path: ""
       dataset_description_path: ""
       use_sample: false
    
       # Import settings
       verbose: false
       batch_size: 25000
       use_preprocessed_files: false
      ```
   
   >    **_NOTES_** 
   >    1) Set the URI in `config.yaml` to the URI of your server. Default value is `bolt://localhost:7687`.
   >    2) Set the password in `config.yaml` to the password of your server. Default value is `12345678`. 

## Getting Stuck??
If you're getting stuck (or you have questions), feel free to reach out to me at a.j.e.swevels@tue.nl.