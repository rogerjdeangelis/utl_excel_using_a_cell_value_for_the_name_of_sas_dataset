# utl_excel_using_a_cell_value_for_the_name_of_sas_dataset
Using cell A3 for the name of the imported SAS dataset

    ```  Using cell A3 for the name of the imported SAS dataset                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      Two solutions sql and datastep                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```        WORKING CODE                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```          SQL                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```           connect to excel (Path='d:/xls/class.xlsx' );                                                                                                       ```
    ```           select                                                                                                                                              ```
    ```               * into :name trimmed                                                                                                                            ```
    ```               from                                                                                                                                            ```
    ```                 connection to Excel                                                                                                                           ```
    ```               (                                                                                                                                               ```
    ```                Select                                                                                                                                         ```
    ```                    *                                                                                                                                          ```
    ```                from                                                                                                                                           ```
    ```                   [class$A3:A4]  * GET NAME FROM THE A3 CELL ;                                                                                                ```
    ```               );                                                                                                                                              ```
    ```           select                                                                                                                                              ```
    ```               create                                                                                                                                          ```
    ```                 table &name as   * USE NAME - BARBARA;                                                                                                        ```
    ```               select                                                                                                                                          ```
    ```                 *                                                                                                                                             ```
    ```               from                                                                                                                                            ```
    ```                 connection to Excel                                                                                                                           ```
    ```               (                                                                                                                                               ```
    ```                Select                                                                                                                                         ```
    ```                    *                                                                                                                                          ```
    ```                from                                                                                                                                           ```
    ```                   [class]                                                                                                                                     ```
    ```               );                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```         DATASTEP                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```           data _null_;                                                                                                                                        ```
    ```             set  xel.'class$A3:A4'n;                                                                                                                          ```
    ```             array chr _character_;                                                                                                                            ```
    ```             call symputx('name',chr[1]);                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```           data &name;                                                                                                                                         ```
    ```              set xel.'class$A3:A4'n;                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://stackoverflow.com/questions/46956195/sas-naming-a-table-based-on-a-cell-value                                                                        ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  HAVE                                                                                                                                                         ```
    ```  ====                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  HAVE workbook d:/xls/class.xlsx with sheet class (you can use [sheet1])                                                                                      ```
    ```                                                                                                                                                               ```
    ```     d:/xls/class.xlsx                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```        +-----------------------------------------------------------------------------+                                                                        ```
    ```        |     A      |     B      |    C       |     D      |    E       |    F       |                                                                        ```
    ```        +-----------------------------------------------------------------------------+                                                                        ```
    ```     1  |   UID      | NAME       |   SEX      |    AGE     |  HEIGHT    |  WEIGHT    |                                                                        ```
    ```        +------------+------------+------------+------------+------------+------------+                                                                        ```
    ```     2  |    1       | ALFRED     |    M       |    14      |    69      |  112.5     |                                                                        ```
    ```        +------------+------------+------------+------------+------------+------------+                                                                        ```
    ```     3  |    2       | BARBARA    |    F       |    13      |    58      |  101.5     |                                                                        ```
    ```        +------------+------------+------------+------------+------------+------------+                                                                        ```
    ```         ...          ...                                                                                                                                      ```
    ```        +------------+------------+------------+------------+------------+------------+                                                                        ```
    ```     20 |    19      | WILLIAM    |    M       |    15      |   66.5     |  112       |                                                                        ```
    ```        +------------+------------+------------+------------+------------+------------+                                                                        ```
    ```                                                                                                                                                               ```
    ```     [CLASS]                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  WANT                                                                                                                                                         ```
    ```  ====                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  WORK.BARBARA total obs=19                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  Obs    NAME       SEX    AGE    HEIGHT    WEIGHT                                                                                                             ```
    ```                                                                                                                                                               ```
    ```    1    Alfred      M      14     69.0      112.5                                                                                                             ```
    ```    2    Alice       F      13     56.5       84.0                                                                                                             ```
    ```    3    Barbara     F      13     65.3       98.0                                                                                                             ```
    ```    4    Carol       F      14     62.8      102.5                                                                                                             ```
    ```    5    Henry       M      14     63.5      102.5                                                                                                             ```
    ```    6    James       M      12     57.3       83.0                                                                                                             ```
    ```   ....                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %utlfkil(d:/xls/class.xlsx);                                                                                                                                 ```
    ```  libname xel "d:/xls/class.xlsx";                                                                                                                             ```
    ```  data xel.class;                                                                                                                                              ```
    ```    set sashelp.class;                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```  libname xel clear;                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  *          _                        _   _                                                                                                                    ```
    ```   ___  __ _| |   _ __   __ _ ___ ___| |_| |__  _ __ _   _                                                                                                     ```
    ```  / __|/ _` | |  | '_ \ / _` / __/ __| __| '_ \| '__| | | |                                                                                                    ```
    ```  \__ \ (_| | |  | |_) | (_| \__ \__ \ |_| | | | |  | |_| |                                                                                                    ```
    ```  |___/\__, |_|  | .__/ \__,_|___/___/\__|_| |_|_|   \__,_|                                                                                                    ```
    ```          |_|    |_|                                                                                                                                           ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  proc sql dquote=ansi;                                                                                                                                        ```
    ```    connect to excel (Path='d:/xls/class.xlsx' );                                                                                                              ```
    ```       select                                                                                                                                                  ```
    ```           * into :name trimmed                                                                                                                                ```
    ```           from                                                                                                                                                ```
    ```             connection to Excel                                                                                                                               ```
    ```           (                                                                                                                                                   ```
    ```            Select                                                                                                                                             ```
    ```                *                                                                                                                                              ```
    ```            from                                                                                                                                               ```
    ```               [class$A3:A4]                                                                                                                                   ```
    ```           );                                                                                                                                                  ```
    ```       create                                                                                                                                                  ```
    ```         table &name as                                                                                                                                        ```
    ```       select                                                                                                                                                  ```
    ```         *                                                                                                                                                     ```
    ```       from                                                                                                                                                    ```
    ```         connection to Excel                                                                                                                                   ```
    ```       (                                                                                                                                                       ```
    ```        Select                                                                                                                                                 ```
    ```            *                                                                                                                                                  ```
    ```        from                                                                                                                                                   ```
    ```           [class]                                                                                                                                             ```
    ```       );                                                                                                                                                      ```
    ```       disconnect from Excel                                                                                                                                   ```
    ```   ;Quit;                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  5718  proc sql dquote=ansi;                                                                                                                                  ```
    ```  5719    connect to excel (Path='d:/xls/class.xlsx' );                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  5720       select                                                                                                                                            ```
    ```  5721           * into :name trimmed                                                                                                                          ```
    ```  5722           from                                                                                                                                          ```
    ```  5723             connection to Excel                                                                                                                         ```
    ```  5724           (                                                                                                                                             ```
    ```  5725            Select                                                                                                                                       ```
    ```  5726                *                                                                                                                                        ```
    ```  5727            from                                                                                                                                         ```
    ```  5728               [class$A3:A4]                                                                                                                             ```
    ```  5729           );                                                                                                                                            ```
    ```  5730       create                                                                                                                                            ```
    ```  5731         table &name as                                                                                                                                  ```
    ```  SYMBOLGEN:  Macro variable NAME resolves to Barbara                                                                                                          ```
    ```  5732       select                                                                                                                                            ```
    ```  5733         *                                                                                                                                               ```
    ```  5734       from                                                                                                                                              ```
    ```  5735         connection to Excel                                                                                                                             ```
    ```  5736       (                                                                                                                                                 ```
    ```  5737        Select                                                                                                                                           ```
    ```  5738            *                                                                                                                                            ```
    ```  5739        from                                                                                                                                             ```
    ```  5740           [class]                                                                                                                                       ```
    ```  5741       );                                                                                                                                                ```
    ```  NOTE: Table WORK."BARBARA" created, with 19 rows and 5 columns.                                                                                              ```
    ```                                                                                                                                                               ```
    ```  5742       disconnect from Excel                                                                                                                             ```
    ```  5743   ;                                                                                                                                                     ```
    ```  5743!   Quit;                                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```  *    _       _            _                                                                                                                                  ```
    ```    __| | __ _| |_ __ _ ___| |_ ___ _ __                                                                                                                       ```
    ```   / _` |/ _` | __/ _` / __| __/ _ \ '_ \                                                                                                                      ```
    ```  | (_| | (_| | || (_| \__ \ ||  __/ |_) |                                                                                                                     ```
    ```   \__,_|\__,_|\__\__,_|___/\__\___| .__/                                                                                                                      ```
    ```                                   |_|                                                                                                                         ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  libname xel "d:/xls/class.xlsx";                                                                                                                             ```
    ```  * you can also use a datastep;                                                                                                                               ```
    ```  data _null_;                                                                                                                                                 ```
    ```    set  xel.'class$A3:A4'n;                                                                                                                                   ```
    ```    array chr _character_;                                                                                                                                     ```
    ```    call symputx('name',chr[1]);                                                                                                                               ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  %put &=name;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```  data &name;                                                                                                                                                  ```
    ```     set xel.'class$A3:A4'n;                                                                                                                                   ```
    ```  run;quit;                                                                                                                                                    ```
    ```  libname xel clear;                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  5711  data _null_;                                                                                                                                           ```
    ```  5712    set  xel.'class$A3:A4'n;                                                                                                                             ```
    ```  5713    array chr _character_;                                                                                                                               ```
    ```  5714    call symputx('name',chr[1]);                                                                                                                         ```
    ```  5715  run;                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  NOTE: There were 1 observations read from the data set XEL.'class$A3:A4'n.                                                                                   ```
    ```  NOTE: DATA statement used (Total process time):                                                                                                              ```
    ```        real time           0.01 seconds                                                                                                                       ```
    ```        user cpu time       0.01 seconds                                                                                                                       ```
    ```        system cpu time     0.00 seconds                                                                                                                       ```
    ```        memory              306.87k                                                                                                                            ```
    ```        OS Memory           17392.00k                                                                                                                          ```
    ```        Timestamp           10/27/2017 07:07:43 PM                                                                                                             ```
    ```        Step Count                        530  Switch Count  0                                                                                                 ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  5715!     quit;                                                                                                                                              ```
    ```  5716  libname xel clear;                                                                                                                                     ```
    ```  NOTE: Libref XEL has been deassigned.                                                                                                                        ```
    ```  SYMBOLGEN:  Macro variable NAME resolves to Barbara                                                                                                          ```
    ```  5717  %put &=name;                                                                                                                                           ```
    ```  NAME=Barbara                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```

