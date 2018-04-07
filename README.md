# utl_transpose_rows_to_column_identifying_type_of_data
Transpose rows to column identifying type of data. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Transpose rows to column identifying type of data

     Identifying employees who have the keyword 'SALE' in variables level1-level4 or
     job1.

     Same result in WPS and SAS

     github
     https://tinyurl.com/y8dh6y6g
     https://github.com/rogerjdeangelis/utl_transpose_rows_to_column_identifying_type_of_data

     Alea Uacta gather macro
     https://github.com/clindocu

     SAS Forum
     https://tinyurl.com/ybouy3jb
     https://communities.sas.com/t5/Base-SAS-Programming/traspose-rows-to-column-identifying-type-of-data/m-p/451801

     Not exactly a solution to ops question, however this creates a powerfull data structure.
     Especially useful when searching meta data.
     Also easily manipulated in SQL with indexes.
     I have used these to search meta data of 100s of tables and 1000s of columns of
     meta along with key stats label, like max, min, percen missing, mean.. all in one 'val' column.

     Type an length can be  moved to a dimension table.

    INPUT
    =====

     WORK.HAVE total obs=48

        LEVEL2           LEVEL1          LEVEL3             LEVEL4          JOB1             LEVEL5

        TOKYO       International Ai     ADMIN              CONTRACTS       MANAGER          So Suumi
        TOKYO       International Ai     ADMIN              CONTRACTS       ASSISTANT        Steffen Graff
        TOKYO       International Ai     ADMIN              FINANCE         ACCOUNTANT       Karin Schmidt
        LONDON      International Ai     ADMIN              PERSONNEL       MANAGER          Anne Bauer
        TOKYO       International Ai     ADMIN              PERSONNEL       ADMIN            Barbara Bial
        TOKYO       International Ai     ADMIN              SHIPPING        ASSIST.          Lisa Lammers
        LONDON      International Ai     ADMIN              SHIPPING        ASSISTANT        Juergen Heidler
        LONDON      International Ai     SALES/MARKETING    MARKETING       MARKET. CONS.    Alex Brudel
        TOKYO       International Ai     SALES/MARKETING    MARKETING       MARKETING        Uwe Benz
        LONDON      International Ai     SALES/MARKETING    MARKETING       ASSISTANT        Merzedes Schauer
        LONDON      International Ai     SALES/MARKETING    SALES           SALES.-CONS.     Heinz Ballmann
        LONDON      International Ai     SALES/MARKETING    SALES           SALES CONS       Cornelia Gut
        LONDON      International Ai     SALES/MARKETING    SALES           SALES CONS BERL  Hartwig Hartmann
        LONDON      International Ai     SALES/MARKETING    SALES           MARKET. CONS.    Jochen Lacker

      data have;
        set sashelp.company;
      run;quit;

    PROCESS
    =======

     %utl_gather(have,var,val,level5,normalize,valformat=$12.,withFormats=Y);

     proc sql;
        create
              table want as
        select
              *
        from
              normalize
        where
              val contains 'SALE'
     ;quit;

    OUTPUT
    ======

     WORK.WANT total obs=44

        LEVEL5                  VAR      VAL             _COLFORMAT    _COLTYP

        Alex Brudel            LEVEL3    SALES/MARKET       $20.          C
        Uwe Benz               LEVEL3    SALES/MARKET       $20.          C
        Merzedes Schauer       LEVEL3    SALES/MARKET       $20.          C
        Heinz Ballmann         LEVEL3    SALES/MARKET       $20.          C
        Heinz Ballmann         LEVEL4    SALES              $30.          C

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

      data have;
        set sashelp.company;
      run;quit;
      sashelp.company

     *         _       _   _
     ___   __ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;


    SAS
    ===

     %utl_gather(have,var,val,level5,normalize,valformat=$12.,withFormats=Y);

     proc sql;
        create
              table want as
        select
              *
        from
              normalize
        where
              val contains 'SALE'
     ;quit;
    libname hlp sas7bdat "C:\Program_Files\SASHome\SASFoundation\9.4\core\sashelp";


    WPS
    ===

    %utl_submit_wps64('
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    %utl_gather(wrk.have,var,val,level5,normalize,valformat=$12.,withFormats=Y);

     proc sql;
        select
              *
        from
              wrk.normalize
        where
              val contains "SALE"
     ;quit;
    run;quit;
    ');



