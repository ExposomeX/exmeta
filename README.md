# exmeta: Exposome Meta Module
### Author: Weinan Lin (weinanlin@pku.edu.cn)
### Date: 2022-12-2

The exmeta package mainly provides users preliminary information retrieval and screening for meta-analysis. It can also summarize the conclusions and effect values of previous studies (available in our meta database), which can help users form a preliminary view of the research topic and further validate the result from the present study. Please see the website (http://www.exposomex.cn/#/expometa) for more information. 

Users can install the package using the following code:

	if (!requireNamespace("devtools", quietly = TRUE)){

    	install.packages("devtools")
    
    	devtools::install_github('ExposomeX/exmeta',force = TRUE)
	}

	library(exmeta)


### Tips:
1. Before using the package, a user defined physical output path (i.e., OutPath) is recommended. For example

		OutPath = "D:/test" #The default path is the current working directory of R. Users can use this code to set the preferred path.
		
2. For each step, the returned values can be named as users' like by following R language requirement. 

3. All the PID must be the same with the one provided by `InitMeta` function, e.g., res$PID.


### Example codes:
##### 1. Initial Meta module:
	res <- InitMeta()
	res$PID
	
##### 2. Load data for Meta module:
    res1 <- LoadMeta(res$PID,
                     UseExample = "example#1")
                     
The exmeta package provides four main functions for users : MetaRefer, VizRef, MetaReview, and MetaEffect.

- MetaRefer: Auto-search all the relative publications from the our meta database and PubMed based on the defined keyword, which has been summarized by the machine learning method and further conveyed to the users.

- VizRefer: VizRefer provides the visual function of papers information searchced or downloaded by `MetaRefer`, showing the year and region distribution directly. 

- MetaReview: We have been building a standardized database to summarize the up-to-now knowledge about the relationship between environmental exposure and specific diseases. For each topic, the viewpoint from the animal and epidemiological studies are comprehensively summarized by well-trained researchers.

- MetaEffect: For some issues, if their epidemiological studies have been well-conducted, e.g. association between PM2.5 exposure and mortality, the meta-analysis can be conducted to summarize the effect value [e.g. odds ratio (OR), relative risk (RR), hazardous risk (HR)]. The related publications are also summarized in the same database with the “MetaReiew”.

##### 3.1 MetaRefer
MetaRefer provides the functions of paper retrieval and relevance sorting, returning the information to the user based on keywords. Please attention, PID must be got from the return result of `InitMeta()`. MetaRefer can only run successfully after successfully running InitMeta and LoadMeta functions.

    res2 <- MetaRefer(PID = res$PID,
                      OutPath = "default",
                      Mode = "search",
                      VarX = "default",
                      VarY = "default",
                      VarM = "default",
                      YearFrom = "default",
                      YearEnd = "default",
                      PMID = "default")

VizRefer function can visualize the articles' main information after `MetaRefer` function.

    res3 <- VizRefer(PID=res$PID,
                     OutPath = "default")

##### 3.2 MetaReview

MetaReview provides the functions of literature review. In the publishd papers, how many recorded that X is a protective/risky factor for Y? This questions can be solved by MetaReview function. (It can only search the papers available in our database).

    res2 <- MetaReview(PID = res$PID,
                       OutPath = "default",
                       CID = "default",
                       DID = "default")

##### 3.2 MetaEffect

MetaEffect provides the functions of effect value pooling. In the publishd papers, what is the effect value between X and Y? This questions can be solved by MetaEffect function. It can provide the combined results of fixed effect model and random effect model. (It can only search the papers available in ExpoMeta database DB_Meta).

    res2 <- MetaEffect(PID = res$PID,
                       OutPath = "default",
                       CID = "default",
                       DID = "default")

##### 4. Exit
After all the analysis is done, please run the "FuncExit()" function to delete the data uploaded to the server.

	FuncExit(PID = res$PID)





