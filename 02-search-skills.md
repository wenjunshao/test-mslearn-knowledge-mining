---
lab:
  title: Create a stored procedure in Azure Database for PostgreSQL
  module: Procedures and functions in PostgreSQL
  description: In this exercise, you create a couple of stored procedures and execute them.
  duration: 30 minutes
  level: 400
  islab: true
  primarytopics:
    - Azure
    - Azure Database for PostgreSQL
---
### Download the exercise files

If you already cloned the GitHub repository containing the exercise files, *Skip downloading the exercise files*.

To download the exercise files, you clone the GitHub repository containing the exercise files to your local machine. The repository contains all the scripts and resources you need to complete this exercise.

1. Open Visual Studio Code if it isn't already open.

1. Select **Show all commands** (Ctrl+Shift+P) to open the command palette.

1. In the command palette, search for **Git: Clone** and select it.

1. In the command palette, enter the following to clone the GitHub repo containing exercise resources and press **Enter**:

    ```bash
    https://github.com/MicrosoftLearning/mslearn-postgresql.git
    ```

1. Follow the prompts to select a folder to clone the repository into. The repository is cloned into a folder named `mslearn-postgresql` in the location you selected.

1. When asked if you want to open the cloned repository, select **Open**. The repository opens in Visual Studio Code.
   
## Connect to the PostgreSQL extension in Visual Studio Code

In this section, you connect to the PostgreSQL server using the PostgreSQL extension in Visual Studio Code. You use the PostgreSQL extension to run SQL scripts against the PostgreSQL server.

1. Open Visual Studio Code if it isn't already opened and open the folder where you cloned the GitHub repository.

1. Select the **PostgreSQL** icon in the left menu.

    > &#128221; If you do not see the PostgreSQL icon, select the **Extensions** icon and search for **PostgreSQL**. Select the **PostgreSQL** extension by Microsoft and select **Install**.

1. If you already created a connection to your PostgreSQL server, skip to the next step. To create a new connection:

    1. In the **PostgreSQL** extension, select **+ Add Connection** to add a new connection.

    1. In the **NEW CONNECTION** dialog box, enter the following information:

        - **Server name**: psql-learn-westus3-k2qwer.postgres.database.azure.com
        - **Authentication type**: Password
        - **User name**: pgAdmin
        - **Password**: ADMIN_PASSWORD123
        - Check the **Save password** checkbox.
        - **Connection name**: psql-learn-westus3-k2qwer

    1. Test the connection by selecting **Test Connection**. If the connection is successful, select **Save & Connect** to save the connection, otherwise review the connection information, and try again.

1. If not already connected, select **Connect** for your PostgreSQL server. You're connected to the Azure Database for PostgreSQL server.

1. Expand the Server node and its databases. The existing databases are listed.

1. If you didn't create the zoodb database already, select **File**, **Open file** and navigate to the folder where you saved the scripts. Select **../Allfiles/Labs/02/Lab2_ZooDb.sql** and **Open**.

1. On the lower right of Visual Studio Code, make sure the connection is green. If it isn't, it should say **PGSQL Disconnected**. Select the **PGSQL Disconnected** text and then select your PostgreSQL server connection from the list in the command palette. If it asks for a password, enter the password you previously generated.

1. Time to create the database.

    1. Highlight the **DROP** and **CREATE** statements and run them.

    1. If you highlight just the **SELECT current_database()** statement and run it, you notice that the database is currently set to `postgres`. You need to change it to `zoodb`.

    1. Select the ellipsis in the menu bar with the *run* icon and select **Change PostgreSQL Database**. Select `zoodb` from the list of databases.

        > &#128221; You can also change the database on the query pane. You can note the server name and database name under the query tab itself. Selecting the database name will show a list of databases. Select the `zoodb` database from the list.

    1. Run the **SELECT current_database()** statement again to confirm that the database is now set to `zoodb`.

    1. Highlight the **Created tables**, **Create foreign keys**, and **Populate tables** sections and run them.

    1. Highlight the 3 **SELECT** statements at the end of the script and run them to verify that the tables were created and populated.

## Create the repopulate_zoo() stored procedure

In this section, you create the `repopulate_zoo()` stored procedure. This procedure is used to repopulate the zoo database with data. The procedure truncates and deletes all the data in the tables and then populates them with new data.

1. In the Visual Studio Code window, select **File**, **Open File**, and then navigate to the lab scripts. Select **../Allfiles/Labs/03/Lab3_RepopulateZoo.sql** and then select **Open**. If necessary, reconnect to the server by selecting the **PGSQL Disconnected** text and then selecting your PostgreSQL server connection from the list in the command palette. If it asks for a password, enter the password you previously generated.

1. Run the **SELECT current_database()** statement to check your current database. Again, the database is most likely set to `postgres`. If so, you need to change it to `zoodb`. Select the ellipsis in the menu bar with the *run* icon and select **Change PostgreSQL Database**. Select `zoodb` from the list of databases. Test the connection again by running the **SELECT current_database()** statement.

1. Highlight the section under **Create stored procedure** from **DROP PROCEDURE** to **END $$.** Run the highlighted text.

1. Keep Visual Studio Code open to continue with the next section.

## Create the new_exhibit() stored procedure

In this section, you create the `new_exhibit()` stored procedure. This procedure is used to add a new exhibit to the zoo database. The procedure inserts a new row into the enclosure table and then inserts rows into the animal table for each animal in the exhibit.

1. In Visual Studio Code, select **File**, **Open File**, and then navigate to the lab scripts. Select **../Allfiles/Labs/05/Lab5_StoredProcedure.sql** and then select **Open**. If necessary, reconnect to the server by selecting the **PGSQL Disconnected** text and then selecting your PostgreSQL server connection from the list in the command palette. If it asks for a password, enter the password you previously generated.

1. Run the **SELECT current_database()** statement to check your current database. Again, the database is most likely set to `postgres`. If so, you need to change it to `zoodb`. Select the ellipsis in the menu bar with the *run* icon and select **Change PostgreSQL Database**. Select `zoodb` from the list of databases. Test the connection again by running the **SELECT current_database()** statement.

1. Highlight the **CALL repopulate_zoo()** statement and run it to start with clean data.

1. Highlight the section under **Create stored procedure** from **DROP PROCEDURE** to **END $$.** Run the highlighted text. Read through the procedure. You see that it declares some input parameters and uses them to insert rows into the enclosure table and the animal table.

1. Keep Visual Studio Code open to continue with the next section.

## Call the stored procedure

Now that you created the `new_exhibit()` stored procedure, you can call it to add a new exhibit to the zoo database. The procedure takes several input parameters, including the name of the exhibit, the type of enclosure, and the number of animals in the exhibit.

1. Highlight the section following the **Call the stored procedure** comment. Run the highlighted text. This script calls the stored procedure by passing values to the input parameters.

1. Highlight and run the two **SELECT** statements. Run the highlighted text. You note that a new row is inserted into enclosure, and five new rows inserted into animal.

## Create and call a table-valued function

Time to create a table-valued function. A table-valued function is a user-defined function that returns a table. You can use a table-valued function in a `SELECT` statement, just like a regular table.

1. In Visual Studio Code, select **File**, **Open File**, and then navigate to the lab scripts. Select **../Allfiles/Labs/05/Lab5_Table_Function.sql** and then select **Open**. If necessary, reconnect to the server by selecting the **PGSQL Disconnected** text and then selecting your PostgreSQL server connection from the list in the command palette. If it asks for a password, enter the password you previously generated.

1. Run the **SELECT current_database()** statement to check your current database. Again, the database is most likely set to `postgres`. If so, you need to change it to `zoodb`. Select the ellipsis in the menu bar with the *run* icon and select **Change PostgreSQL Database**. Select `zoodb` from the list of databases. Test the connection again by running the **SELECT current_database()** statement.

1. Highlight and run the **CALL repopulate_zoo()** stored procedure to start with clean data.

1. Highlight and run the script following the **Create a table valued function** comment. This function returns a table called **enclosure_summary**. Read through the function code to understand how the table is populated.

1. Highlight and run the two select statements, passing in a different enclosure ID each time.

1. Highlight and run the script following the **How to use a table valued function with a LATERAL join** comment. This script shows the table-valued function being used in place of a table name in a join.

## In-built functions

In this section, you explore some of the built-in functions available in PostgreSQL. PostgreSQL has a rich set of built-in functions that you can use to perform various operations on data. These functions can be used in SQL queries to manipulate and analyze data.

1. In Visual Studio Code, select **File**, **Open File**, and then navigate to the lab scripts. Select **../Allfiles/Labs/05/Lab5_SimpleFunctions.sql** and then select **Open**. If necessary, reconnect to the server by selecting the **PGSQL Disconnected** text and then selecting your PostgreSQL server connection from the list in the command palette. If it asks for a password, enter the password you previously generated.

> &#128221; The functions in this script are not specific to the zoo database. They are general PostgreSQL functions that can be used in any database. You can run them in any database, including the `postgres` database.

1. Highlight and run each function to see how it works. For more information, review the [online documentation](https://www.postgresql.org/docs/current/functions.html) article for information about each function.


