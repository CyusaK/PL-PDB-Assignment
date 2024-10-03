# PL-PDB-Assignment

README
Problem Statement
This database system is designed to manage an e-commerce platform that handles clients, products, and orders. The primary goal is to facilitate transactions between clients and products while maintaining a structured record of orders, clients, and product inventory. The database supports operations such as adding clients, products, and orders, updating client details, and deleting products from inventory.

SQL Commands Executed
1. Creating a Pluggable Database
Create a Pluggable Database (PDB)

### sql

CREATE PLUGGABLE DATABASE plsql_class2024db
  ADMIN USER cy_plsqlauca IDENTIFIED BY cyusa
  FILE_NAME_CONVERT = ('E:\oradata\ORA19\pdbseed', 'E:\oradata\ORA19\plsqp_class2024db');
Explanation: This command creates a new pluggable database named plsql_class2024db with an admin user cy_plsqlauca and a password of cyusa. The FILE_NAME_CONVERT parameter specifies the location for the new PDB's data files.

Open the Pluggable Database

### sql

ALTER PLUGGABLE DATABASE plsql_class2024db OPEN;
Explanation: This command opens the newly created PDB, making it accessible for operations.

List All PDBs

### sql

SELECT name FROM v$pdbs;
Explanation: This query retrieves the names of all pluggable databases in the container database (CDB). It helps verify that the new PDB has been created successfully.

2. Creating and Managing Another Pluggable Database
Create Another PDB

### sql

CREATE PLUGGABLE DATABASE cy_to_delete_pdb
  ADMIN USER cy_plsqlauca IDENTIFIED BY cyusa
  FILE_NAME_CONVERT = ('E:\oradata\ORA19\pdbseed', 'E:\oradata\ORA19\cy_to_delete_pdb');
Explanation: This command creates a second pluggable database named cy_to_delete_pdb using the same admin user as the first PDB.

Open the New PDB

### sql

ALTER PLUGGABLE DATABASE cy_to_delete_pdb OPEN;
Explanation: This command opens the cy_to_delete_pdb, making it accessible for operations.

Attempt to Open an Already Open PDB

### sql

ALTER PLUGGABLE DATABASE cy_to_delete_pdb OPEN;
Explanation: This command tries to open the cy_to_delete_pdb again, but it fails because the PDB is already open. This demonstrates error handling when trying to perform operations on a PDB that is already open.

Close the PDB

### sql

ALTER PLUGGABLE DATABASE cy_to_delete_pdb CLOSE;
Explanation: This command closes the cy_to_delete_pdb, making it inaccessible until it is opened again.

Drop the PDB

### sql

DROP PLUGGABLE DATABASE cy_to_delete_pdb INCLUDING DATAFILES;
Explanation: This command drops the cy_to_delete_pdb, including its data files, permanently removing it from the database system.

3. Verify PDBs Again

### sql

SELECT name FROM v$pdbs;
Explanation: This query retrieves the names of all remaining pluggable databases after the deletion of cy_to_delete_pdb, allowing you to confirm the operation was successful.


Explanations of Results and Transactions
Creating PDBs: The creation of PDBs allows for better management of multiple databases within a single Oracle instance. Each PDB can be managed independently while sharing the same container database resources.

Opening and Closing PDBs: Opening and closing PDBs enables or restricts access to them. This is important for maintenance and resource management.

Dropping PDBs: The ability to drop a PDB allows for cleanup of unused or temporary databases, ensuring that the database environment remains organized and efficient.

Listing PDBs: Querying the PDBs provides insights into the current state of the database environment, allowing for better monitoring and management.
