# Paper Inventory - Database Design and Implementation
	
## Description :
	
*** This project requires me to use Python and SQLite to build and run a database that will hold data about paper imports that is taken from an Excel file. I create a table called "product_data" with several fields such as HS Code, Product Description, Shipper and Consignee Names, Standard Quantity, and Country Details using SQL after reading the data using pandas. I use the "tabulate" programme to format and show the data as an orderly table, which improves readability and makes it easier to analyse paper inputs.
	
	
Technologies  and tools used: 
	
|Python language and SQLite database engine|
| :------------ |:---------------:|
|Technologies:| pandas, sqlite3 and tabulate library.|
	

          File name : 
          paper_import.ipynb
          paper_inventory.xlsx

           Data Source: https://www.volza.com/p/paper/import/import-in-canada/
 

          1 - Import Statements and Libraries: 

             \``` 
               
import pandas as pd
import sqlite3

          /```

           2 - Read Data from the "Data Sheet":  This code read de file called "paper_inventory.xlsx" data sheet using Python's Pandas module and stores it in the variable data.

   \``` 
excel_file = "paper_inventory.xlsx"
sheet_name = "Data Sheet"
data = pd.read_excel(excel_file, sheet_name)

          /```

          3 - Database implementation - This code generates a cursor for executing SQL queries, establishes a connection to a SQLite database called "output.db", and defines a SQL query to build the table "product_data" with particular column names and let ready to store product-related data.


 \``` 
db_connection = sqlite3.connect("output.db")
cursor = db_connection.cursor()

create_table_query = """
CREATE TABLE IF NOT EXISTS product_data (
    HS_Code TEXT,
    Product_Description TEXT,
    Shipper_Name TEXT,
    Consignee_Name TEXT,
    Standard_Qty TEXT,
    Country_Of_Origin TEXT,
    Country_of_Destination TEXT
);
"""

cursor.execute(create_table_query)

          /```


       4 - Display formatted table from SQLite - The command "tabulate" is used to retrieve shipping data from a SQLite database and show it as a structured table.

 

     \``` 
import sqlite3
from tabulate import tabulate

# Connect to the SQLite database and retrieve data
db_connection = sqlite3.connect("output.db")
cursor = db_connection.cursor()

select_query = """
SELECT * FROM product_data;
"""

cursor.execute(select_query)
data = cursor.fetchall()

db_connection.close()

# Convert the data to a list of dictionaries for tabulate
table_data = []
for row in data:
    table_data.append({
        "HS Code": row[0],
        "Product Description": row[1],
        "Shipper Name": row[2],
        "Consignee Name": row[3],
        "Standard Qty": row[4],
        "Country Of Origin": row[5],
        "Country of Destination": row[6]
    })

# Print the data in a tabular format
table_format = "grid"  
# You can choose other formats like "grid", "plain", "pipe", "html", etc.
print(tabulate(table_data, headers="keys", tablefmt=table_format))

          /```
