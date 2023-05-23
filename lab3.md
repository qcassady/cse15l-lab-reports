# Lab 3  
I chose to work with the `find` command.  
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

## Usage of ChatGPT  
I used the prompt ```Tell me some command-line options for the bash command find```.  
ChatGPT returned back to me:  
~~~
The find command in Bash is a powerful tool for searching files and directories based on various criteria. Here are some commonly used command-line options for the find command:

-name pattern: Searches for files or directories with the specified pattern in their name.
Example: find /path/to/search -name "*.txt"

-type type: Searches for files of the specified type. Common types are f for regular files and d for directories.
Example: find /path/to/search -type f

-size [+|-]size: Searches for files of a specific size. The + symbol denotes greater than, the - symbol denotes less than, and the size is specified in bytes.
Example: find /path/to/search -size +1M

-mtime [+|-]n: Searches for files modified more than (+) or less than (-) n days ago.
Example: find /path/to/search -mtime +7

-user username: Searches for files owned by a specific user.
Example: find /path/to/search -user john

-group groupname: Searches for files owned by a specific group.
Example: find /path/to/search -group developers

-empty: Searches for empty files or directories.
Example: find /path/to/search -type d -empty

-exec command {} +: Executes a command on each found file or directory. The {} placeholder represents the found item(s), and + allows multiple items to be passed to the command.
Example: find /path/to/search -name "*.txt" -exec rm {} +

-maxdepth n: Limits the search depth to n levels.
Example: find /path/to/search -maxdepth 2 -name "*.txt"

-mindepth n: Specifies the minimum depth of the search.
Example: find /path/to/search -mindepth 1 -name "*.txt"

These are just a few examples of the many options available for the find command. You can explore more options and combinations by referring to the find command's manual page using the man find command in your terminal.
~~~  
Using these basic descriptions and the example code, I selected the few that seemed the most useful and then applied it to our given repository and extrapolated the broader uses for these options (why we want to use them). ChatGPT helped me save a lot of time looking around for different options, and just collected a lot of them in one place for me to choose from. 
