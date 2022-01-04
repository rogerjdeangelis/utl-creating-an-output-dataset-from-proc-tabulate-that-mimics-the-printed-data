# utl-creating-an-output-dataset-from-proc-tabulate-that-mimics-the-printed-data
Creating an output dataset from proc tabulate that mimics the printed data 
   %let pgm=utl-creating-an-output-dataset-from-proc-tabulate-that-mimics-the-printed-data;

    Creating an output dataset from proc tabulate that mimics the printed data

    Problem:
       I want a SAS dataset from proc tabulate not printer output

    This is what I do not want

    ------------------------------------------------------------------------------------------------------------------------------
    |              |                                         YEAR                                          |                      |
    |              |---------------------------------------------------------------------------------------|                      |
    |              |      2015           |      2016           |      2017           |      2018           |        All           |
    |              |---------------------+---------------------+---------------------+---------------------+----------------------|
    |              | N      |  ColPctN   | N      |  ColPctN   | N      |  ColPctN   | N      |  ColPctN   |  N      |  ColPctN   |
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |Sex           |        |            |        |            |        |            |        |            |         |            |
    |--------------|        |            |        |            |        |            |        |            |         |            |
    |0             |    3.00|       50.00|    1.00|       33.33|    2.00|       66.67|    3.00|       37.50|     9.00|       45.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |1             |    3.00|       50.00|    2.00|       66.67|    1.00|       33.33|    5.00|       62.50|    11.00|       55.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |Region        |        |            |        |            |        |            |        |            |         |            |
    |--------------|        |            |        |            |        |            |        |            |         |            |
    |East          |    1.00|       16.67|    2.00|       66.67|       .|           .|       .|           .|     3.00|       15.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |North         |    2.00|       33.33|    1.00|       33.33|    1.00|       33.33|    2.00|       25.00|     6.00|       30.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |South         |    3.00|       50.00|       .|           .|    2.00|       66.67|    4.00|       50.00|     9.00|       45.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |West          |       .|           .|       .|           .|       .|           .|    2.00|       25.00|     2.00|       10.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |Group         |        |            |        |            |        |            |        |            |         |            |
    |--------------|        |            |        |            |        |            |        |            |         |            |
    |1             |    2.00|       33.33|    1.00|       33.33|    1.00|       33.33|    3.00|       37.50|     7.00|       35.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |2             |    2.00|       33.33|    1.00|       33.33|    1.00|       33.33|    3.00|       37.50|     7.00|       35.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |3             |    2.00|       33.33|    1.00|       33.33|    1.00|       33.33|    2.00|       25.00|     6.00|       30.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |Condition     |        |            |        |            |        |            |        |            |         |            |
    |--------------|        |            |        |            |        |            |        |            |         |            |
    |0             |       .|           .|       .|           .|    2.00|       66.67|    8.00|      100.00|    10.00|       50.00|
    |--------------+--------+------------+--------+------------+--------+------------+--------+------------+---------+------------|
    |1             |    6.00|      100.00|    3.00|      100.00|    1.00|       33.33|       .|           .|    10.00|       50.00|
    -------------------------------------------------------------------------------------------------------------------------------


      Two Solutions (These solutions produce datasets instead og printed output)

           1. Proc corresp
           2, Proc tabulate (first proposed by
                 Bartosz Jablonski
                 yabwon@gmail.com )
              I need to clean it up?
    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data have;
        input  (ID Sex Year Region Group Condition) (: $8.);
    cards4;
    1 1 2015 North 1 1
    2 0 2015 North 2 1
    3 0 2015 South 3 1
    4 1 2015 South 1 1
    5 0 2015 South 2 1
    6 1 2015 East 3 1
    7 1 2016 East 1 1
    8 1 2016 East 2 1
    9 0 2016 North 3 1
    10 0 2017 North 1 1
    11 0 2017 South 2 0
    12 1 2017 South 3 0
    13 1 2018 South 1 0
    14 1 2018 South 2 0
    15 0 2018 South 3 0
    16 1 2018 South 1 0
    17 1 2018 North 2 0
    18 1 2018 North 3 0
    19 0 2018 West 1 0
    20 0 2018 West 2 0
    ;;;;
    run;quit


    Up to 40 obs WORK.HAVE total obs=20 03JAN2022:16:59:05

    Obs    ID    Sex    Year    Region    Group    Condition

      1    1      1     2015    North       1          1
      2    2      0     2015    North       2          1
      3    3      0     2015    South       3          1
      4    4      1     2015    South       1          1
      5    5      0     2015    South       2          1
      6    6      1     2015    East        3          1
      7    7      1     2016    East        1          1
      8    8      1     2016    East        2          1
      9    9      0     2016    North       3          1
     10    10     0     2017    North       1          1
     11    11     0     2017    South       2          0
     12    12     1     2017    South       3          0
     13    13     1     2018    South       1          0
     14    14     1     2018    South       2          0
     15    15     0     2018    South       3          0
     16    16     1     2018    South       1          0
     17    17     1     2018    North       2          0
     18    18     1     2018    North       3          0
     19    19     0     2018    West        1          0
     20    20     0     2018    West        2          0

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_    ___ ___  _ __ _ __ ___  ___ _ __
     / _ \| | | | __| `_ \| | | | __|  / __/ _ \| `__| `__/ _ \/ __| `_ \
    | (_) | |_| | |_| |_) | |_| | |_  | (_| (_) | |  | | |  __/\__ \ |_) |
     \___/ \__,_|\__| .__/ \__,_|\__|  \___\___/|_|  |_|  \___||___/ .__/
                    |_|                                            |_|
    */

    Up to 40 obs WORK.WANT_COR total obs=11 03JAN2022:18:44:59

    Obs    type         Label     npct2015      npct2016     npct2017      npct2018      npctSum

      1    SEX          0        3 (50.00)     1 (33.33)     2 (66.67)    3 (37.50)     9 (45.00)
      2    SEX          1        3 (50.00)     2 (66.67)     1 (33.33)    5 (62.50)     11 (55.00)
      3    REGION       East     1 (16.67)     2 (66.67)     0 (0.00)     0 (0.00)      3 (15.00)
      4    REGION       North    2 (33.33)     1 (33.33)     1 (33.33)    2 (25.00)     6 (30.00)
      5    REGION       South    3 (50.00)     0 (0.00)      2 (66.67)    4 (50.00)     9 (45.00)
      6    REGION       West     0 (0.00)      0 (0.00)      0 (0.00)     2 (25.00)     2 (10.00)
      7    GROUP        1        2 (33.33)     1 (33.33)     1 (33.33)    3 (37.50)     7 (35.00)
      8    GROUP        2        2 (33.33)     1 (33.33)     1 (33.33)    3 (37.50)     7 (35.00)
      9    GROUP        3        2 (33.33)     1 (33.33)     1 (33.33)    2 (25.00)     6 (30.00)
     10    CONDITION    0        0 (0.00)      0 (0.00)      2 (66.67)    8 (100.00)    10 (50.00)
     11    CONDITION    1        6 (100.00)    3 (100.00)    1 (33.33)    0 (0.00)      10 (50.00)

    /*           _               _     _        _
      ___  _   _| |_ _ __  _   _| |_  | |_ __ _| |__
     / _ \| | | | __| `_ \| | | | __| | __/ _` | `_ \
    | (_) | |_| | |_| |_) | |_| | |_  | || (_| | |_) |
     \___/ \__,_|\__| .__/ \__,_|\__|  \__\__,_|_.__/
                    |_|
    */

    * Enhanced Image of Tabulate printed output, merge count and percent;
    Up to 40 obs WORK.WANT_TAB total obs=15 03JAN2022:18:45:48

    Obs    type         npct2015      npct2016      npct2017     npct2018       npctSum

      1    Sex
      2    0            3 (50.00)     1 (33.33)     2 (66.67)    3 (37.50)     9 (45.00)
      3    1            3 (50.00)     2 (66.67)     1 (33.33)    5 (62.50)     11 (55.00)
      4    Region
      5    East         1 (16.67)     2 (66.67)     . (.)        . (.)         3 (15.00)
      6    North        2 (33.33)     1 (33.33)     1 (33.33)    2 (25.00)     6 (30.00)
      7    South        3 (50.00)     . (.)         2 (66.67)    4 (50.00)     9 (45.00)
      8    West         . (.)         . (.)         . (.)        2 (25.00)     2 (10.00)
      9    Group
     10    1            2 (33.33)     1 (33.33)     1 (33.33)    3 (37.50)     7 (35.00)
     11    2            2 (33.33)     1 (33.33)     1 (33.33)    3 (37.50)     7 (35.00)
     12    3            2 (33.33)     1 (33.33)     1 (33.33)    2 (25.00)     6 (30.00)
     13    Condition
     14    0            . (.)         . (.)         2 (66.67)    8 (100.00)    10 (50.00)
     15    1            6 (100.00)    3 (100.00)    1 (33.33)    . (.)         10 (50.00)

    /*
     _ __  _ __ ___   ___ ___  ___ ___    ___ ___  _ __ _ __ ___  ___ _ __
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|  / __/ _ \| `__| `__/ _ \/ __| `_ \
    | |_) | | | (_) | (_|  __/\__ \__ \ | (_| (_) | |  | | |  __/\__ \ |_) |
    | .__/|_|  \___/ \___\___||___/___/  \___\___/|_|  |_|  \___||___/ .__/
    |_|                                                              |_|
    */
    proc datasets lib=work ;
     delete jyn npcts pct_: cnt_: want_cor;
    run;quit;

    ods exclude all;
    %array(vs,values=Sex Region Group Condition);

    %do_over(vs,phrase=%str(
         ods output observed=cnt_?(rename=(_2015-_2018=cnt2015-cnt2018 sum=tot) where=(label ne 'Sum'));
         ods output colprofilespct=pct_?(rename=(_2015-_2018=pct2015-pct2018));
         proc corresp data=have dim=1 observed print=both all cross=both;
            tables ?, year;
         run;quit;

         proc sql;
            create
               table jyn as
            select
               upcase("?") as type length=16
              ,l.label as label length=16
              ,l.*
              ,r.*
              ,100*l.tot/(select sum(tot) from cnt_?) as pctSum
            from
               cnt_? as l left join pct_?(rename=label=lbl) as r
            on
               l.label = r.lbl
         ;quit;

         data npcts(keep=type label npct:);
           set jyn;
           array pcts      pct2015-pct2018 pctSum;
           array cnts      cnt2015-cnt2018 tot ;
           array npct  $16 npct2015-npct2018 npctSum ;
           do i=1 to dim(npct);
              npct[i]=cats(put(cnts[i],4.),' (',put(pcts[i],6.2),')');
           end;
         run;
         proc append data=npcts base=want_cor;
         run;quit;
         ));
    ods select all;


    /*                                   _        _
     _ __  _ __ ___   ___ ___  ___ ___  | |_ __ _| |__
    | `_ \| `__/ _ \ / __/ _ \/ __/ __| | __/ _` | `_ \
    | |_) | | | (_) | (_|  __/\__ \__ \ | || (_| | |_) |
    | .__/|_|  \___/ \___\___||___/___/  \__\__,_|_.__/
    |_|
    */


    options ls=255;
    %utl_odstab(setup);
    proc tabulate data=have;
       title "|type| n2015| p2015| n2016| p2016 | n2017| p2017 | n2018| p2018 | nAll| pall |";
       class Sex Year Region Group Condition;
       table
          Sex Region Group Condition
          ,
          Year*(n colpctn) All*(n colpctn) ;
       ;
    run;quit;
    %utl_odstab(outdsn=want_odsrpt);


    /*
    * Intermediate datasets;

    Up to 40 obs WORK.WANT_ODSRPT total obs=18 03JAN2022:17:01:53

    Obs    type         n2015    p2015      n2016    p2016      n2017     p2017     n2018     p2018     nAll      pall

      1                 Year
      2                 2015     2016       2017     2018       All
      3                 N        ColPctN    N        ColPctN    N        ColPctN    N        ColPctN    N        ColPctN
      4    Sex
      5    0            3.00     50.00      1.00     33.33      2.00     66.67      3.00     37.50      9.00     45.00
      6    1            3.00     50.00      2.00     66.67      1.00     33.33      5.00     62.50      11.00    55.00
      7    Region
      8    East         1.00     16.67      2.00     66.67                                              3.00     15.00
      9    North        2.00     33.33      1.00     33.33      1.00     33.33      2.00     25.00      6.00     30.00
     10    South        3.00     50.00                          2.00     66.67      4.00     50.00      9.00     45.00
     11    West                                                                     2.00     25.00      2.00     10.00
     12    Group
     13    1            2.00     33.33      1.00     33.33      1.00     33.33      3.00     37.50      7.00     35.00
     14    2            2.00     33.33      1.00     33.33      1.00     33.33      3.00     37.50      7.00     35.00
     15    3            2.00     33.33      1.00     33.33      1.00     33.33      2.00     25.00      6.00     30.00
     16    Condition
     17    0                                                    2.00     66.67      8.00     100.00     10.00    50.00
     18    1            6.00     100.00     3.00     100.00     1.00     33.33                          10.00    50.00

    */

    data want_tab(drop=p2: n2: nall pall);
      set want_odsrpt(where=(type ne ""));
           array pcts  $16    p2015-p2018 pall;
           array cnts  $16    n2015-n2018 nall ;
           array npct  $16    npct2015-npct2018 npctSum ;
           do i=1 to dim(npct);
             if nall ne "" then  npct[i]=cats(put(input(cnts[i],best.),4.),' (',put(input(pcts[i],best.),6.2),')');
           end;
           drop i;
    run;quit;

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

    /*
     _ __ ___   __ _  ___ _ __ ___
    | `_ ` _ \ / _` |/ __| `__/ _ \
    | | | | | | (_| | (__| | | (_) |
    |_| |_| |_|\__,_|\___|_|  \___/

    */

    %macro utl_odstab(outdsn,datarow=0,getnames=yes);

       %if %qupcase(&outdsn)=SETUP %then %do;

            filename _tmp1_ clear;  * just in case;

            %utlfkil(%sysfunc(pathname(work))/_tmp1_.txt);
            %utlfkil(%sysfunc(pathname(work))/_tmp2_.txt);

            filename _tmp1_ "%sysfunc(pathname(work))/_tmp1_.txt";

            %let _ps_= %sysfunc(getoption(ps));
            %let _fc_= %sysfunc(getoption(formchar));

            OPTIONS ls=max ps=32756  FORMCHAR='|'  nodate nocenter;

            title; footnote;

            proc printto print=_tmp1_;
            run;quit;

       %end;
       %else %do;

            /* %let outdsn=tst; %let datarow=0; %let bars=10; */

            proc printto;
            run;quit;

            filename _tmp1_ "%sysfunc(pathname(work))/_tmp1_.txt";
            filename _tmp2_ "%sysfunc(pathname(work))/_tmp2_.txt";

            proc datasets lib=work nolist;  *just in case;
             delete &outdsn;
            run;quit;

            data _null_;
              retain n remHed 0 ;
              infile _tmp1_ length=l ;
              input lyn $varying32756. l;
              lyn=compress(lyn);
              if countc(lyn,'|')>3;
              n=n+1;
              if n ge %eval(&datarow + 1)  then do;
                 file "%sysfunc(pathname(work))/_tmp2_.txt";
                 if compress(lyn,'|')  ne "" then do;putlog lyn;put lyn;end;
              end;
            run;quit;

            proc printto;
            run;quit;

            proc import
               datafile="%sysfunc(pathname(work))/_tmp2_.txt"
               dbms=dlm
               out=&outdsn(drop=var:)
               replace;
               delimiter='|';
               getnames=&getnames;
            run;quit;

            filename _tmp1_ clear;
            filename _tmp2_ clear;

            %utlfkil(%sysfunc(pathname(work))/_tmp1_.txt);
            %utlfkil(%sysfunc(pathname(work))/_tmp2_.txt);

            options FORMCHAR='|----|+|---+=|-/\<>*';

       %end;

    %mend utl_odstab;
