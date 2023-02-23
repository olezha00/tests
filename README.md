#         Database and tables creation and data upload user guide

This user guide contains information about how to create database and tables and fill them with data.
Please, read it attentively before making any attempt of database and data management.
Structure of DBManagement folder:
- create_db_and_tables.py – Python script used for creation of database, tables, extensions etc. and setting up system configurations.
#Important!
This script requires PostgreSQL user with admin rights!

- upload_data.py - Python script used for data upload to clay_content and spatial_data tables.
- keygen.py – Python script used for one-time generation and insertion of clay_api_key to clay_api_keys table. 
  Those keys are used for access to Clay API.
- db.cfg – configuration file, which contains all parameters for database connection and data upload setup.
- data – folder with test data
- conda_reqs.txt – text file with required packages and libraries that can be
  installed only with conda.
- pip_reqs.txt – text file with required packages and libraries that can be
  installed only with pip.

Preparation for data upload

Data needs to be prepared before upload. Tabular data must be placed in one folder and spatial – in another one. Absolute path to both folders must be saved in db.cfg in [data_config] section. Please, find the example below.
 
The second requirement is Anaconda must be installed.
Please find download and installation guide links below. Download - https://www.anaconda.com/
Installation guide - https://docs.anaconda.com/anaconda/install/

Steps for data upload

After data preparation and Anaconda installation you should prepare an environment for code run.
1. Create virtual environment. Use the next command

    $ conda create -n <name_of_env>

2. Activate it

    $ conda activate <name_of_env>

Note:
To deactivate your virtual environment use $ conda deactivate <name_of_env>

3. Navigate to DBManagement folder

    $ cd <path_to_DBManagement_folder>

4. Install conda_reqs.txt

    $ conda install --file conda_reqs.txt

5. Install pip_reqs.txt

    $ pip install -r pip_reqs.txt

6. Fill in needed parameters in db.cfg for [landviser_clay_db] section according to your PostgreSQL server parameters
#Be sure that chosen user has admin rights!

7. Runcreate_db_and_tables.py

    $ python3 create_db_and_tables.py

This script creates DB and tables with required parameters. If it runs successfully, you will see similar output
  Else – similar to the next output

8. Runupload_data.py

    $ python3 upload_data.py

This script uploads data to the created DB.
CLI will ask you to input version of data to upload. You can put it in in integer format or you can leave it blank and press Enter. In that case version of data will be generated automatically as max(version) + 1. But if you choose the version, the script will update priviously uploaded data with chosen version and will set its is_relevant = false
If success
Else

9. If you need to generate a clay_api_key, run following

    $ python3 keygen.py
   
