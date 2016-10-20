# ComBot

It is a slack bot that discovers relationships between source codes and developers by mining GitHub repositories. It uses repository contributions for creating file-to-developer mappings & facilitates quick communication via Slack.

##Use Cases
###Use Case 1 - Retrieving the top N contributors of a file  
**1 Preconditions**  
User must have fetched the repository’s commit history using the fetch command.  
**2 Main Flow**  
User will specify the filename that he/she wishes to query [S1]. Bot performs a lookup on the file-to-developer mapping to obtain the number of commits by each contributor [S2]. Bot returns top N contributors for the specified file. [S3].  
**3 Subflows**  
[S1] User provides the name of the file that he/she wishes to query using the following  command format:  
`file [filename] top [n]`  
[S2] Bot determines the number of commits by each contributor by performing a lookup on the file-to-developer mapping generated in the ‘fetch’ phase.  
[S3] Bot returns top N contributors for the specified file in descending order of number of commits.  

**4 Alternative Flows**  
[E1] There are no commits in the repository.

###Use Case 2: Retrieving the recent N contributors of a file
**1 Preconditions**  
User must have fetched the repository’s commit history using the fetch command.  
**2 Main Flow**  
User will specify the filename that he/she wishes to query [S1]. Bot performs a lookup on the file-to-developer mapping to obtain the most recent commit by each contributor [S2]. Bot returns recent N contributors for the specified file. [S3].  
**3 Subflows**   
[S1] User provides the name of the file that he/she wishes to query using the following  command format:    
`file [filename] recent [n]`  
[S2] Bot determines the most recent commit by each contributor by performing a lookup on the file-to-developer mapping generated in the ‘fetch’ phase.    
[S3] Bot returns the most recent N contributors of the specified file in descending order of commit times.    

**4 Alternative Flows**  
[E1] There are no commits in the repository.  


###Use Case 3: Retrieving the company wise contribution count for an open source project repository  
**1 Preconditions**  
User must have fetched the repository’s commit history using the fetch command.  
**2 Main Flow**  
User will specify the filename that he/she wishes to query [S1]. Bot generates a dictionary mapping contributors to their organizations[S2]. Bot performs a lookup on the file-to-developer mapping to obtain the contributor and the number of commits[S3]. The bot then looks up the dictionary and adds the number of commits of the contributor to his organisations contributions[S3]. Bot returns this summary of organizations and their count. [S4].  
**3 Subflows**  
[S1] User provides the name of the file that he/she wishes to query using the following  command format:  
`orgContributors [filename]`  
[S2] Bot makes REST calls for each contributor for getting his company and generates a dictionary.  
[S3] Bot then iterates over the list of users for the company by using the FileMappings and then updates the count of contributions for his/her company.  
[S4] Bot then returns the company and its total contributions made to that file.    

**4 Alternative Flows**  
[E1] There are no commits in the repository.

