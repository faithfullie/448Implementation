448Implementation
=================

Implementation of "Explore-by-Example: An Automatic Query Steering Framework for Interactive Data Exploration"[1]

Independent study project by Alexia Lou, under supervision of Professor Rachel Pottinger at University of British Columbia
  		
  

####Instruction:  
1. start the program:  
    to run from runnable .jar file: double click explore-by-example.jar    
    to run from source .jar file: extract files from explore-by-example-src.jar, import the project into Eclipse, run UI.java     
2. dataset    
    choose where to import the dataset (i.e. local file or MySQL database server)     
  * for the complete PhotoObjectAll dataset, please send a request using [this page](http://skyserver.sdss3.org/contact/default.asp?subject=CasJobs+Issue:+&smtp=mail.pha.jhu.edu&helpdesk=helpdesk@sdss3.org&url=http%3a%2f%2fskyserver.sdss3.org%2fcasjobs%2fdefault.aspx)     
  * databaset I used is attached seperately    
  * for dataset with size less than 5G,    
    1. please login [this page](http://skyserver.sdss3.org/casjobs/default.aspx) (see login.txt)    
    2. select "DR9" under *Contest*    
    3. click \[submit\] to send query   
    4. retrieved dataset will be saved in "MyDB"     
    5. to download the dataset: select "MyDB", then the table with to download, in the table detail on the right, click \[download\], then go to "Output"    
3. wait for data to be imported intp the program, after which a window will display with samples retrieved from the data base    
4. select relevant samples, click \[confirm\] [^1]     
5. after the program finish retrieving next set of samples, another sample selection window will display, alone with another window displaying variable information about the model trained using current labeled samples    
6. press \[exit\] at any time to exit the program, labeled samples and trained model will be saved autometically in the directory where the program is saved.     



####Acceptable Input Format:  
1. local file format: Arff, C4.5, CSV, libsvm, svm light, Binary serialized instances, XRFF  
2. remote database server: MySQL  
		
	

####Parameter Input:  
* cluster base: number of clusters to divide the dataset into at the first iteration  
* cluster growth factor:  factor by which the number of cluster grow at each iteration  
* FN penalty: number of extra samples retrieved around each false negative data object. (used when total number of relevant objects discovered during discovery phrase <= number of false negative predictions made at current iteration)  
* FN distance: minimum distance from false negative cluster center to retrieve samples from. (used when total number of relevant objects discovered during discovery phrase > number of false negative predictions made at current iteration)  
* max boundaries: maximum number of samples retrieved around each boundary  
  		

  		
####Output:  
* at each iteration:  
  - all samples labeled so far  
  - prediction stats of current classifier  
  - decision tree built based on current training data  
* when exit the program (stored in the same directory as the program files):  
  - trained classifier (output.model)  
  - training set labeled by user (train.csv)  
  		
  

####Other:  
* The implementation is based on the optimized version of each space exploration phrase  
* "Error, not in CLASSPATH?":    
	please refer to [this web page](http://weka.wikispaces.com/Trying+to+add+JDBC+driver...+-+Error,+not+in+CLASSPATH%3F) for detail information  
	
* Known cause(s) of exception:    
  1. if the original dataset has attribute named "class" or "cluster"  
  2. may throw exception for dataset containing non-numeric data  
  		

        

####Reference:  
[1]. Dimitriadou, Kyriaki, Olga Papaemmanouil, and Yanlei Diao. "Explore-by-Example: An Automatic Query Steering Framework for Interactive Data Exploration." (2014).




[^1] query used to select Relevant_Samples.csv from PhotoObjAllTop3000.csv: 
        SELECT DISTINCT * from PhotoObjAllTop3000 	    
        WHERE   
            (rowc between 1165.711 and 1199.086 and not (colc between 344.8247 and 399.4847) and not (ra between 336.566699604645 and 336.572752552481))   
            or (colc between 344.8247 and 399.4847 and not (rowc between 1165.711 and 1199.086) and not (ra between 336.566699604645 and 336.572752552481))    
            or (ra between 336.566699604645 and 336.572752552481 and not(rowc between 1165.711 and 1199.086) and not (colc between 344.8247 and 399.4847)))    


