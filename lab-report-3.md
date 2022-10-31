# Lab Report 3 #

## Variations of Find ##

## -name ##
* First we want to be in the working directory, and for this case is **docsearch**. It contains the directory *technical* and will contain multiple subdirectories and files within. 
* This will be the working directory where we will execute the command-line, *find* on, and the multiple uses it has.

* Something that we are familiar with while using find is **-name**, this option allows us to search the name of the files with a specific string search.

~~~
{
    twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch (main)
$ find technical/911report -type f -name  "*.txt"
technical/911report/chapter-1.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
technical/911report/chapter-12.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
...
}
~~~

* What this command is doing is that it traverses through the **technical** directory and the **911report** sub-directory and searches for files with a .txt in the name using the extension indicator as "". 
* What's outputted is all the files with .txt in the file name within the 911report sub-directory. This is useful if we want to find the files that have a specific extension such as .pdf or .txt

* A unique variation of **find** is very similar to the last option but with **-iname**.

~~~
{
twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch (main)
$ find technical/911report -type f -iname  "*.TXT"
technical/911report/chapter-1.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
technical/911report/chapter-12.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-2.txt
technical/911report/chapter-3.txt
technical/911report/chapter-5.txt
technical/911report/chapter-6.txt
technical/911report/chapter-7.txt
technical/911report/chapter-8.txt
technical/911report/chapter-9.txt
technical/911report/preface.txt
}
~~~

* What's happening here is that it searches through files the same way **-name** does but is not case-sensitive. 
* Although the files are lowercase, if we used **-iname** and *.TXT, it still returns the same output as it's a case-insensitive search. This is useful if we want to search through many files that have different text cases.

* We can also use **-name** to search for the exact file name itself rather than extensions.

~~~
{
twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch (main)
$ find technical/911report -type f -iname preface.txt

technical/911report/preface.txt
}
~~~

* In this case instead of searching for an extension, we're looking for it's exact file name. What's outputted is the file that has the exact string we searched for. 
* This is useful if we already know the name of a specific file and want to grab it directly.

## -size ##

* We're going to explore the variations of the option **-size** within **find**.

~~~
{
twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch (main)
$ find technical/ .type f -size -2k

technical/
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
technical/plos/pmed.0020191.txt
technical/plos/pmed.0020226.txt
find: ‘.type’: No such file or directory
find: ‘f’: No such file or directory
}
~~~

* What **-size** is doing is that it searches for files within a directory that has less than 2 kilobytes. **-2k** indicates that the memory should be a kilobyte and less than 2.
* What it outputs is all the files with less than 2 kilobytes of memory.
* This is useful for finding any files that havent reached the  memory threshold or is too small.

* Another variation of **-size** is using a range for the size of memory. 

~~~
{
    twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch (main)
$ find technical/ .type f -size +10k -size 21k

technical/biomed/1471-2105-3-12.txt
technical/biomed/1471-2105-4-25.txt
technical/biomed/1471-2156-3-11.txt
technical/biomed/1471-2164-2-6.txt
technical/biomed/1471-2164-3-23.txt
technical/biomed/1471-2164-3-26.txt
technical/biomed/1471-2164-3-34.txt
...
}
~~~

* The input is searching for files with a file size greater than 10 and less than 21 kilobytes such -size twice and + and - to indicate greater or less than. 
* The output is all the files with greater than 10 and less than 21 kilobytes of size. This is useful if we wanted to find all the files that are within a size threshold and the files that are not.

* A third variation of **-size** is finding a file with the exact amount of memory size.

~~~
{
twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch (main)
$ find technical/ .type f -size 2k

technical/government/Media/Campaign_Pays.txt
technical/government/Media/Court_Keeps_Judge_From.txt
technical/government/Media/Fire_Victims_Sue.txt
technical/government/Media/It_Pays_to_Know.txt
technical/government/Media/Justice_requests.txt
technical/government/Media/Lawyer_Web_Survey.txt
technical/government/Media/Self-Help_Website.txt
...
}
~~~

* Instead of checking if the files are greater or less than a size, we can directly check if a file matches an exact memory size without the use of a - or +. 
* What's outputted is the size of the all the files with exactly 2 kilobytes. This is useful if we knew exactly how much memory size we wanted to look for.

## -type ##

* With this option within **find**, **-type** outputs a file or directory of the specific type.

~~~
{
    twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch/technical (main)
$ find -type d

.
./911report
./biomed
./government
./government/About_LSC
./government/Alcohol_Problems
./government/Env_Prot_Agen
./government/Gen_Account_Office
./government/Media
./government/Post_Rate_Comm
./plos
}
~~~

* While in the technical directory, we are going to recursively search through all the subdirectories in technical with the use of **-type d**. *d* indicates that a directory should be looked for. 
* What's outputted is all the subdirectories within technical. This is useful if we wanted to see all the subdirectories within a working directory.

* A second example is showing how different sub-directories are shown based off the user location.

~~~
{
twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch (main)
$ cd technical/government

twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch/technical/government (main)
$ find -type d

.
./About_LSC
./Alcohol_Problems
./Env_Prot_Agen
./Gen_Account_Office
./Media
}
~~~

* In this case we move from the docsearch working directory to the government subdirectory inside of technical. We then run the same command and see that it's only showing the subdirectories within the government subdirectory compared to the last command.
* This is useful again in seeing specific subdirectories based on the user location.

* We can also search for a different type with the similar commands.

~~~
{
    
twist@LAPTOP-P7G30CON MINGW64 ~/OneDrive/Documents/GitHub/docsearch (main)
$ find technical/government/About_LSC -type f

technical/government/About_LSC/Comments_on_semiannual.txt
technical/government/About_LSC/commission_report.txt
technical/government/About_LSC/conference_highlights.txt
technical/government/About_LSC/CONFIG_STANDARDS.txt
technical/government/About_LSC/diversity_priorities.txt
technical/government/About_LSC/LegalServCorp_v_VelazquezDissent.txt
technical/government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt
technical/government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt
...
}
~~~

* The input is navigating through technical,governnment, and About_LSC subdirectories to where files are stored. We then use **-type f** to find all the files within the sub-directory. 
* What's outputted is all the names of type f, file. This is useful when searching for a specific file type.

## This concludes the different options and variations -find has in linux. ##

