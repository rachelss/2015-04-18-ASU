#Etherpad notes

##Shell

http://files.software-carpentry.org/gShell webpage:  http://swcarpentry.github.io/shell-novice/01-filedir.html  
Shell webpage 2: http://swcarpentry.github.io/shell-novice/02-create.html  
Shell webpage 3: http://swcarpentry.github.io/shell-novice/03-pipefilter.html  
Shell webpage 4: http://swcarpentry.github.io/shell-novice/04-loop.html  

Why do we use the shell?  
 - Shell allows for better automation  
 - Running programs on numerous datasets simultaneously 


$pwd to find out where you are. (print working directory). This is where you start from.  
$cd (changing directory) to establish new directory

Use tab completion for ease of use - autofills directory info

You can list the contents of the directory with ls command

Use arrows up or down to bring up previously used commands 

Different flags:

$ls -F delineates Files and Folders (Folders demarcated by a /)  
Can list files in a subfolder with ls -F <foldername>  
$ls ../.. provides list for two folders up in directory  
$ls -r displays files/folders in reverse alphabetical order  
$ls -r -F (displays files/folders in reverse alphabetical order and Flags files vs. folders)  

$ls -lh (l: long listing - h; give me file size in human language - in bytes)  
gives you permissions (group and user), ownership (user and group), file size, last modified date, name  
$ls -R -lh -t (lists files recursively, provides long listing, and orders by time last modified)

$man <command> gives you the manual/documentation for that command (will only work in macs - not in the default windows - use google)  
type q to get out of the manual page

space is the official separator in Shell (dont name files with spaces in them)  
 
Example quiz: ls ../backup:    
ls: list directory  
..: go back two levels  
/backup: the folder to list its directory  

-r is to display things in reverse   
Note: Shell is caps sensitive 

command, flags, argument <-that's the order, but the order flags doesn't matter  

cd: changes the working directory to the user's home directory. preferred location to put all of your stuff.  

$cd ~/Desktop - changes to Desktop directory  
$cd -    changes directory to your previous working directory (like a back button)  
$cd .. moves up folder in directory

mkdir <name> makes new directory  
$touch <filename> creates new file

$nano <filename> takes you to nano which is a text editor. you can use this to write information in this file.   
 - ctrl + x will exit the file (and gives you an option for saving)  
 - ctrl + o will save the file (write-out option)  
write out is the same as saving file. 

$cat <filename> prints (or concatenates) the contents of the file to the screen  
$mv <filename> <new_filename> moves the contents of the file; essentially used for renaming  
$rm <filename> deletes the file  
$rm -r <directory> deletes all files and the directory/folder recursively  
in linux - use command "file" to determine type of file with the file as an argument 

rm -i is a safer command it will ask you if you are sure you want to delete the file  

When using cp, always include a directory at the end of the command to move files to - maybe?  If you don't include a directory, doesn't it just copy in the current directory? Oh yeah, thanks. You have to give it a different name though.  

including an l in the commands will give you the long explanation more details   

$wc <filename> gives word count  
lists no. of lines, words, and characters in the file

$wc *.pdb  
This will give the word count for all files that end in .pdb

Reminder: Use arrows up or down to bring up previously used commands  

Also you can type history to view a list of your previous commands  

<command> > lines.txt  
will print the output of the command to the file lines.txt  
<command> >> lines.txt  
will append the output of the command to the file lines.txt

(Ctrl) + C breaks you out of the current command if you mistype something

$head -2 <filename> will give you only the first two lines of your file  
$tail -2 <filename> will give you the last two lines of your file

sort -n <filename> | head -2  
| = piping; helps you string your commands together  
Default $sort <filename> sorts by first character  
$sort -n <filename> sorts numerically

The use of * * is helpful to search (filtering)for files - but this only helps if you have your data very well organized. It can also help you search for all of your files.  

$cut -d , -f 2 <filename>  
the -d flag will cut based on the comma as a delimiter (you can specify any delimiter)  
then you can specify which field you want to print to the screen using the -f flag (2 specifies second field)

[note: "argument" is like a parameter]

Here is a helpful site http://explainshell.com/

For Loop:   
$for file in *txt  
> do   
> echo mv $file new-$file   
> done
    
$for file in *txt; do  echo mv $file new-$file ; done  

Running a script on our files:  
$for file in *txt; do echo $file; bash goostats $file $file.stats; done  
- This will display the name of each file in the loop (using echo) and run the bash script goostats on each file in our for loop. It also specifies the outfile that will contain the filename followed by stats. The output of the script for each file will be saved in <filename>.txt.stats  

If your script is in a different directory than your file, then you will need to specify the path to that script.   

If you just use cat, it prints to the screen.  
If you use cat >> <filename>, it is only going to write to the file, not the screen

##R

Data Processing in R  
https://github.com/swcarpentry/r-novice-inflammation/archive/gh-pages.zip

Set working directory in R with: setwd()  
Example: setwd("/Users/Desktop/r-novice-inflammation-gh-pages/data")  
OR you can navigate within R studio: Session > Set Working Directory > To Files Pane Location

To read in the cvs file: read.csv("filename.csv")   

To view a variable in a separate window: View(<variable name>)

apply(<var>,<dimension>,<function>): allow us to apply a function on a or several specific dimensions in a matrix; when dimension = 1, it means by row; 2 means by column. 

apply(mydata,1,mean)  
- This will apply the function mean to all rows of the variable mydata  
- if you do 2 in place of 1, it will apply it to columns

[1, is your first row  
,1] is your first column 

Functions in R:  example of a function to convert temperatures

fahr_to_cel = function(temp) { 
        celsius = (temp - 32) * (5/9)
        return(celsius)
        }

Function components: name = function (input element) {  
        variable = (what its actually going to do)  
        return (variable that it returns to the user)  
        }

Function to analyze your files and print output to a pdf -

analyze = function(filename) {
  dat = read.csv(filename,header=FALSE)
  avg_day=apply(dat,2,mean)
  min_day=apply(dat,2,min)
  max_day=apply(dat,2,max)
  pdf(paste(filename,".pdf",sep=""))
  plot(avg_day)
  plot(min_day)
  plot(max_day)
  dev.off()
}
mylist = list.files(pattern="infla")
for (f in mylist){
  analyze (f)
}

##Git

GitHub
http://swcarpentry.github.io/git-novice/01-setup.html

Git
- Allows version control
- Allows you to do a thing similar to Track Changes to files
- You decide when the tracking is taken
- It allows you to describe the history of the project you are working on

You need to type these three lines only once for initial set-up -

$git config --global user.name "Firstname Lastname"
$git config --global user.email "your_email_address"
$git config --global color.ui "auto"

You can use whatever text editor you want -
$git config --global core.editor "nano -w"

Make a new directory and go into it (using cd).

$git init
- Use this to initialize an empty git repository

Make a new file called draft.txt and save it

$git status
- Gives you untracked files
- You should be able to see draft.txt here

$git add draft.txt
- This keeps track of the changes that you will make to your file draft.txt

$git commit -m "initial commit"
- This will commit whatever changes you make to your draft.txt

&git log 
- This is to see the progress of your git

http://swcarpentry.github.io/git-novice/03-changes.html

$cat <file name>
$less <file name>
- To view the contents of the file

$git commit -am "made more changes"
- Combines the separate git add and git commit steps into one step
- Can be useful if you are in the middle of a project and have forgotten to do git add
- It will do this for every file that you have changed though 

$git diff <unique_id_number>
- This will give you the changes you made corresponding to this ID number and the last committed version.

Quiz Question:
Which command(s) below would save changes of myfile.txt to my local Git repository?
$ git add myfile.txt
$ git commit -m "my recent changes"

Example to make the "bio"
$mkdir bio
$cd bio
$git init
$nano me.txt - you can also create the file with $touch me.txt
-write three sentences in nano, save and close.
$git status
$git add me.txt
$git commit -m "initial commit"
$nano me.txt
$git diff
$git commit -am "added a line"
$git log

for specific differences add the first characters of the commit unique code.

$git checkout HEAD~1 draft.txt
$cat draft.txt
- Allows you to look at the previous version
- You can do a $git commit -am "roll back" here if you actually want to work with this previous version. 

$git checkout master
$cat draft.txt
- Allows you  to go to the latest committed version again after you have finished looking at a previous version


$ echo "add new text" >> me.txt 
- will add new text without having to go in the file using nano

checkout HEAD: goes to prev committed version, so just go to the HEAD to recover previously committed version. or use the unique ID of the last committed version.

http://rachelss.github.io/2015-04-18-ASU/

$git log | grep commit | wc -l
- This will basically count the lines that have the word "commit" in them from the git log. 
- This is to help you determine how many commits you have done. 
-  grep is a bash command that searches for the regular expression that you give it , for eg. commit

Go to github.com and create your account
Create a new repository (for eg. swc_testing)


Here are the codes to push:

Éor push an existing repository from the command line onto GitHub

$git remote add origin <your HTTPS link for example https://github.com/...>  
$git push -u origin master

add your user name and password 

$git pull origin master   
- This will pull down stuff from GitHub onto your local repository

Article  on Citation Advantage of Open Access Articles  
http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.0040157

##SQL

SQL is for managing databases not flat files. Databases are used for large datasets where there is no physical copy to a database but instead you interact with an interface and you ask it questions about the data. SQL = structured query language 


$sqlite3 survey.db

>.schema

Recommended to use CAPS for commands. 
SQL is not cap sensitive 
 
>SELECT * FROM Person;

A command is not ended until you give it the semi colon 

You can also select two columns from a table:
>SELECT ident, family FROM Person;

>SELECT DISTINCT quant FROM Survey;  
This will give you a list of unique items from the column quant of the table Survey

>SELECT * FROM Survey ORDER BY reading;  
This will sort the data by default in an ascending manner.

You can sort it in descending order by using  
>SELECT * FROM Survey ORDER BY reading DESC;

Filtering the entries: 
>SELECT * FROM Survey WHERE person='dyer'; 
This will give you the entries only where the entry in the person column is dyer

>SELECT * FROM Survey WHERE taken!=619;  
This will give you the entries where the entry in the taken column is NOT equal to 619 (the ! before the equal means "not")

>SELECT * FROM Survey WHERE reading<2 AND reading >-2;  
This will give you entries where the reading is less than 2 and not equal to 2

>SELECT * FROM Visited WHERE dated is NULL;  
This is the way to get any entry which does not have any data for the column dated.

>SELECT * FROM Visited WHERE dated is not NULL; 
This will give you all the entries where the dated column is not blank/without data

>SELECT count(*) FROM Survey;  
Will count the entries from Survey

>SELECT avg(reading) FROM Survey;  
- Gives you the average of all the readings from the table Survey  
- Also works with min and max  

>SELECT (reading-32)*5/9 FROM Survey WHERE quant='temp';
Basically you can write queries to do mathematical operations on the entries. 

>SELECT * FROM Survey GROUP BY quant,person;
This allows you to do groupings

>SELECT * FROM Survey JOIN Person ON Survey.person=Person.ident;
This gives us only the matched entries for the information in column person of table Survey and column ident of table Person

>SELECT Survey.quant,Survey.reading,Person.personal
   ...> FROM Survey JOIN Person
   ...> ON Survey.person=Person.ident
   ...> WHERE Survey.person='dyer';
Writing a long query. 

Exercise to join two not directly connected tables: SELECT Survey.quant, Survey.reading, Visited.site FROM survey join Visited ON Survey.taken=visited.ident;

SELECT Survey.quant, Survey.reading, Visited.site, Site.lat, Site.long
   ...> FROM Survey JOIN Visited JOIN Site
   ...> ON Survey.taken=Visited.ident
   ...> AND Visited.site=Site.name;

>.quit exits the sqlite3 program


An alternate way to do it:
SELECT Survey.quant, Survey.reading, Site.lat, Site.long FROM Survey JOIN Visited ON Survey.taken=Visited.ident JOIN Site ON Visited.site=Site.name;

Querying from R:

> install.packages("RSQLite")  
> library(RSQLite)  
> connect = dbConnect(dbDriver("SQLite"),dbname="C:/Users/Tanvi/Desktop/survey.db")  
> dbGetQuery(connect,"SELECT * FROM Site")






