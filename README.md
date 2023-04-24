# utl-how-to-rotate-a-sas-dataset-by_270-degrees
How to rotate a SAS dataset by 270 degrees? 
    %let pgm=utl-how-to-rotate-a-sas-dataset-by_270-degrees;

    How to rotate a SAS dataset by 270 degrees?

    github
    https://tinyurl.com/3xwafbxz
    https://github.com/rogerjdeangelis/utl-how-to-rotate-a-sas-dataset-by_270-degrees

    stackoverflow
    https://tinyurl.com/y6ny3nsy
    https://stackoverflow.com/questions/74727197/how-to-rotate-a-sas-dataset-by-90-degrees

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */
    libname sd1 "d:/sd1";

    data sd1.have;
     input m1-m6;
    cards4;
    1 1 1 0 0 0
    1 1 0 0 0 0
    1 0 1 0 0 0
    0 0 0 1 0 0
    0 0 0 0 1 0
    0 0 0 0 0 1
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Up to 40 obs from last table SD1.HAVE total obs=6 24APR2023:16:21:10                                                  */
    /*                                                                                                                        */
    /*  Obs    M1    M2    M3    M4    M5    M6                                                                               */
    /*                                                                                                                        */
    /*   1      1     1     1     0     0     0                                                                               */
    /*   2      1     1     0     0     0     0                                                                               */
    /*   3      1     0     1     0     0     0                                                                               */
    /*   4      0     0     0     1     0     0                                                                               */
    /*   5      0     0     0     0     1     0                                                                               */
    /*   6      0     0     0     0     0     1                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/
    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */
    %utl_submit_r64('
    library(pracma);
    library(haven);
    library(SASxport);
    want <- as.matrix(read_sas("d:/sd1/have.sas7bdat"));
    want<-as.data.frame(rot90(want,3));
    want;
    write.xport(want,file="d:/xpt/want.xpt");
    ');

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    libname xpt xport "d:/xpt/want.xpt";
    proc contents data=xpt._all_;
    run;quit;

    proc print data=xpt.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   Obs    V1    V2    V3    V4    V5    V6                                                                              */
    /*                                                                                                                        */
    /*     1     0     0     0     1     1     1                                                                              */
    /*     2     0     0     0     0     1     1                                                                              */
    /*     3     0     0     0     1     0     1                                                                              */
    /*     4     0     0     1     0     0     0                                                                              */
    /*     5     0     1     0     0     0     0                                                                              */
    /*     6     1     0     0     0     0     0                                                                              */
    /*                                                                                                                        */
    /**************************************************************************************************************************/
