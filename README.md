# utl-RE-Altair-Personal-slc-Monarch-Learning-Series_2023-Exercise_6-Sales---Inventory-Analysis
RE Altair Personal slc Monarch Learning Series 2023 Exercise 6 Sales &amp; Inventory Analysis
    %let pgm=utl-RE-Altair-Personal-slc-Monarch-Learning-Series_2023-Exercise_6-Sales-&-Inventory-Analysis;

    %stop_submission;

    RE Altair Personal slc Monarch Learning Series 2023 Exercise 6 Sales & Inventory Analysis

    Listserv messed up my post, see github

    github
    https://github.com/rogerjdeangelis/utl-RE-Altair-Personal-slc-Monarch-Learning-Series_2023-Exercise_6-Sales---Inventory-Analysis

    community.altair
    https://community.altair.com/discussion/39107
    https://community.altair.com/discussion/39107/altair-monarch-learning-series-2023-exercise-6-solution-classic-sales-inventory-master-analysis?utm_source=community-search&utm_medium=organic-search&utm_term=exe


    Prep Copy Workboooks

    libname tab excel "d:/xls/Classic_Multiple_Tabs.xlsx";
    libname mas excel "d:/xls/Classic Inventory Master.xlsx";


    1.  What were the Total Sales between Jan-May?

        Sales from Jan to Apr = $79,399.02

        libname tab excel "d:/xls/Classic_Multiple_Tabs.xlsx";

        data allmth;

          retain totsal 0;

          set
            tab.'jan$'n
            tab.'feb$'n
            tab.'mar$'n
            tab.'apr$'n
            tab.'may$'n
           end=dne;

          totsal=sum(totsal,amount);

          if dne then  put "Sales from Jan to Apr = " totsal dollar10.2;

        run;quit;

        libname tab clear;

    2.  Which Classical Records were sold during Jan-May that are not on the Inventory Master?

        Desc
        --------------------------------------
        Bizet, Carmen
        Britten, War Requiem
        Rossini, Otello, Von Stada, Carreras


        libname mas excel "d:/xls/Classic Inventory Master.xlsx";

        data master;
         set mas.'Inventory Master$'n ;
        run;quit;

        libname mas clear;

        proc sql;
          select
             desc
          from
             allmth
          except
          select
             desc
          from
             mas
        ;quit;

    3.  Which Classic Records are on the Inventory Master but were not sold during Jan-May?

        Desc
        --------------------------
        Gounod, Romeo et Juliette

        proc sql;
          select
             desc
          from
             mas
          except
          select
             desc
          from
             allmth
        ;quit;

    /*--- end ---*/
