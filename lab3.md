# Lab 3  
I chose to work with the `less` command.  
## `-name` (source:ChatGPT)  
First off, we have the `-name` option.  
~~~
$ find technical -name preface.txt
technical/911report/preface.txt
~~~
~~~
$ find technical -name ai00134.txt
technical/government/Gen_Account_Office/ai00134.txt
~~~
This option is very useful as it returns the location of a file given its name. We can use this for locating files that are nested deep within many folders, and to easily obtain the path of a file sp that we may later use it within our code.  
## `-type` (source:ChatGPT)  
Next, we have the `-type` option.  
~~~
$ find technical -type d
technical
technical/911report
technical/biomed
technical/government
technical/government/About_LSC
technical/government/Alcohol_Problems
technical/government/Env_Prot_Agen
technical/government/Gen_Account_Office
technical/government/Media
technical/government/Post_Rate_Comm
technical/plos
~~~
~~~
$ find technical -type d -name "*me*"
technical/biomed
technical/government
~~~
This option is very useful for refining our searches to only include certain types of files. There are three possible options for the typing, `-type f` for files, `-type d` for directories, and `-type l` for symbolic links. When used alongside the `-name` option, you become able to get very specific searches, so the two make a great combination together.  
## `-size` (source:ChatGPT)  
Additionally, we have the `-size` option.
~~~
$ find technical -size -1k
technical
technical/911report
technical/biomed
technical/government
technical/government/About_LSC
technical/government/Alcohol_Problems
technical/government/Env_Prot_Agen
technical/government/Gen_Account_Office
technical/government/Media
technical/government/Post_Rate_Comm
technical/plos
~~~
~~~
$ find technical -size -2k -type f
technical/plos/pmed.0020191.txt
technical/plos/pmed.0020226.txt
~~~
~~~
$ find technical -size +300k -type f
technical/government/Gen_Account_Office/d01591sp.txt
technical/government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
~~~
This option helps us to find large batches of things that meet the size requirement, such as finding all your files that are below 1kb, or all the files above 300kb. There are two ways to use the command `-` and `+`, which determine whether you are looking for files above or below the size you specified.  
## `-exec` (source:ChatGPT)  
Finally, we have the `-exec` option.
~~~
$ find technical -size +300k -type f -exec wc -l {} \;
5695 technical/government/Gen_Account_Office/d01591sp.txt
6114 technical/government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
~~~
~~~
$ find technical -size -2k -type f -exec wc -l {} \;
17 technical/plos/pmed.0020191.txt
17 technical/plos/pmed.0020226.txt
~~~
This option allows us to run another command on the search results. This is extremely useful for things like grep, wc, and many more, as it allows us to directly act on the results of our searches instead of having to use another command to run them after we know which files we are working with. Overall it saves a lot of time and makes working with bash easier!
