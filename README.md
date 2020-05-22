# utl-transpose-sets-of-variables-with-a-compound-identification-Arts-macro
Transpose sets of variables with a compound identification Arts macro    
    Transpose sets of variables with a compound identification Arts macro                                                       
                                                                                                                                
    Arts macro is faster than transpose and handles the common case of transposing sets of variables.                           
                                                                                                                                
    I made a slight change and caculated the compound id, yearQtr. Arts macro does not handle compound ids.                     
                                                                                                                                
    github                                                                                                                      
    https://tinyurl.com/ydcu4tx8                                                                                                
    https://github.com/rogerjdeangelis/utl-transpose-sets-of-variables-with-a-compound-identification-Arts-macro                
                                                                                                                                
    SAS Forum                                                                                                                   
    https://tinyurl.com/y86z3j46                                                                                                
    https://communities.sas.com/t5/New-SAS-User/Creating-New-Variables-With-Dynamic-Suffix/m-p/649992                           
                                                                                                                                
    Arts Macro                                                                                                                  
    filename tr url "https://raw.githubusercontent.com/art297/transpose/master/transpose.sas";                                  
    %inc tr;                                                                                                                    
                                                                                                                                
    *_                   _                                                                                                      
    (_)_ __  _ __  _   _| |_                                                                                                    
    | | '_ \| '_ \| | | | __|                                                                                                   
    | | | | | |_) | |_| | |_                                                                                                    
    |_|_| |_| .__/ \__,_|\__|                                                                                                   
            |_|                                                                                                                 
    ;                                                                                                                           
                                                                                                                                
    data have;                                                                                                                  
    input product : $ production_year quarter amount count;                                                                     
      yearQtr=catx('_',production_year,quarter);                                                                                
    cards4;                                                                                                                     
    A 1984 0 100 1                                                                                                              
    A 1984 1 200 2                                                                                                              
    A 1984 2 300 3                                                                                                              
    A 1985 0 400 4                                                                                                              
    A 1985 1 500 5                                                                                                              
    B 1984 0 100 1                                                                                                              
    B 1984 1 200 2                                                                                                              
    B 1984 2 300 3                                                                                                              
    B 1985 0 400 4                                                                                                              
    B 1985 1 500 5                                                                                                              
    ;;;;                                                                                                                        
    run;quit;                                                                                                                   
                                                                                                                                
    WORK.HAVE total obs=10                                                                                                      
                                                     ** added this variable **                                                  
                PRODUCTION_                                                                                                     
     PRODUCT        YEAR       QUARTER    AMOUNT    COUNT    YEARQTR                                                            
                                                                                                                                
        A           1984          0         100       1      1984_0                                                             
        A           1984          1         200       2      1984_1                                                             
        A           1984          2         300       3      1984_2                                                             
        A           1985          0         400       4      1985_0                                                             
        A           1985          1         500       5      1985_1                                                             
        B           1984          0         100       1      1984_0                                                             
        B           1984          1         200       2      1984_1                                                             
        B           1984          2         300       3      1984_2                                                             
        B           1985          0         400       4      1985_0                                                             
        B           1985          1         500       5      1985_1                                                             
                                                                                                                                
    *            _               _                                                                                              
      ___  _   _| |_ _ __  _   _| |_                                                                                            
     / _ \| | | | __| '_ \| | | | __|                                                                                           
    | (_) | |_| | |_| |_) | |_| | |_                                                                                            
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                           
                    |_|                                                                                                         
    ;                                                                                                                           
                                                                                                                                
              AMOUNT_    COUNT_    AMOUNT_    COUNT_    AMOUNT_    COUNT_    AMOUNT_    COUNT_    AMOUNT_    COUNT_             
    PRODUCT    1984_0    1984_0     1984_1    1984_1     1984_2    1984_2     1985_0    1985_0     1985_1    1985_1             
                                                                                                                                
      A         100         1        200         2        300         3        400         4        500         5               
      B         100         1        200         2        300         3        400         4        500         5               
                                                                                                                                
    *                                                                                                                           
     _ __  _ __ ___   ___ ___  ___ ___                                                                                          
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                         
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                         
    | .__/|_|  \___/ \___\___||___/___/                                                                                         
    |_|                                                                                                                         
    ;                                                                                                                           
                                                                                                                                
    %transpose(data=have, out=want, by=product, id=YEARQTR, delimiter=_, var=amount count)                                      
                                                                                                                                
                                                                                                                                
