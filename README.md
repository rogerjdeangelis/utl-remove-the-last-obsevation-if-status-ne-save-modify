# utl-remove-the-last-obsevation-if-status-ne-save-modify
Remove the last obsevation if code ne save modify 

    Remove the last obsevation if code ne save modify                                                     
                                                                                                          
    github                                                                                                
    https://tinyurl.com/yxjdjltw                                                                          
    https://github.com/rogerjdeangelis/utl-remove-the-last-obsevation-if-status-ne-save-modify            
                                                                                                          
    SAS Forum                                                                                             
    https://tinyurl.com/yyuh3gbn                                                                          
    https://communities.sas.com/t5/SAS-Programming/Delete-last-record-conditionally/m-p/590495            
                                                                                                          
    *_                   _                                                                                
    (_)_ __  _ __  _   _| |_                                                                              
    | | '_ \| '_ \| | | | __|                                                                             
    | | | | | |_) | |_| | |_                                                                              
    |_|_| |_| .__/ \__,_|\__|                                                                             
            |_|                                                                                           
    ;                                                                                                     
                                                                                                          
    data have;                                                                                            
    format mydate date9.;                                                                                 
    input ln_no $ status $ mydate date9.;                                                                 
    cards4;                                                                                               
    1123 save 1jun2018                                                                                    
    1123 save 11jun2018                                                                                   
    1123 save 15jun2018                                                                                   
    1123 save 12jun2018                                                                                   
    1123 save 9jun2018                                                                                    
    1123 save 3jun2018                                                                                    
    1123 save 3May2018                                                                                    
    1123 remove 12jun2017                                                                                 
    ;;;;                                                                                                  
    run;quit;                                                                                             
                                                                                                          
    /*                                                                                                    
     WORK.HAVE total obs=8         |  RULES                                                               
                                   |                                                                      
       MYDATE      LN_NO   STATUS  |                                                                      
                                   |                                                                      
      01JUN2018    1123     save   |                                                                      
      11JUN2018    1123     save   |                                                                      
      15JUN2018    1123     save   |                                                                      
      12JUN2018    1123     save   |                                                                      
      09JUN2018    1123     save   |                                                                      
      03JUN2018    1123     save   |                                                                      
      03MAY2018    1123     save   |                                                                      
      12JUN2017    1123     remove |  * since remove is not equal save                                    
                                   |    remove the record                                                 
    */                                                                                                    
                                                                                                          
    *            _               _                                                                        
      ___  _   _| |_ _ __  _   _| |_                                                                      
     / _ \| | | | __| '_ \| | | | __|                                                                     
    | (_) | |_| | |_| |_) | |_| | |_                                                                      
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                     
                    |_|                                                                                   
    ;                                                                                                     
                                                                                                          
     WORK.HAVE total obs=8                                                                                
                                                                                                          
       MYDATE      LN_NO   STATUS                                                                         
                                                                                                          
      01JUN2018    1123     save                                                                          
      11JUN2018    1123     save                                                                          
      15JUN2018    1123     save                                                                          
      12JUN2018    1123     save                                                                          
      09JUN2018    1123     save                                                                          
      03JUN2018    1123     save                                                                          
      03MAY2018    1123     save                                                                          
                                  missing last ob                                                         
                                                                                                          
    *                                                                                                     
     _ __  _ __ ___   ___ ___  ___ ___                                                                    
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                   
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                   
    | .__/|_|  \___/ \___\___||___/___/                                                                   
    |_|                                                                                                   
    ;                                                                                                     
                                                                                                          
    data have;                                                                                            
    format mydate date9.;                                                                                 
    input ln_no $ status $ mydate date9.;                                                                 
    cards4;                                                                                               
    1123 save 1jun2018                                                                                    
    1123 save 11jun2018                                                                                   
    1123 save 15jun2018                                                                                   
    1123 save 12jun2018                                                                                   
    1123 save 9jun2018                                                                                    
    1123 save 3jun2018                                                                                    
    1123 save 3May2018                                                                                    
    1123 remove 12jun2017                                                                                 
    ;;;;                                                                                                  
    run;quit;                                                                                             
                                                                                                          
    data have;                                                                                            
                                                                                                          
      if _n_=0 then do; %let rc %sysfunc(dosubl('                                                         
           proc sql noprint; select count(*) into :obs trimmed from have;quit;                            
           '));                                                                                           
      retain ob1 &obs;  * has to be dome before _n_=0;                                                    
      end;                                                                                                
                                                                                                          
      modify have point=ob1;                                                                              
      if status ne 'save' then remove;                                                                       
                                                                                                          
      stop;                                                                                               
                                                                                                          
    run;quit;                                                                                             
                                                                                                          
