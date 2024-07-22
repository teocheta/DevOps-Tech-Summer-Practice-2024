touch nameOfTheFile (this creates a new file)
ls (list of files)
-l (show in table format (long format))
--format=commas/long...
-a (+ show hidden files)
-r (show in reverse order)
-R (show recursively? all subdirectories)
-i (show inodes ?? )
-d (directories only)
--author username of the creator of the file
.. (shows parent directory files)


*Sort by time
-t / -tu / -tc order by / access time / modif time / metadata modif time /

*Sort by size
-S sort by size in bytes
-h more readable using power of 1024 (1024 bytes = 1K)

*Best Friend
man (manual)
whatis (name) = man -f (name) => see what it does

man -k ls searches for the given command through all man pages, and returns all of them as output.

man -w ls returns the location of the file from where the page is rendered.

*Work with directories

pwd . This command shows your current work directory.

/root is home directory
to go there just type cd

rmdir - remove directories
rm - remove files
everything is a file in linux but you need to force it (saftey reasons)
-r means go recursively through directories (and treat everything as file)
-f - force. Another words, do not ask, assume the user knows what he is doing.
these 2 are used together -rf

*Pipes

grep 'case' .bashrc  =>  This command will search for pattern case in a file .bashrc.

wc -l .bashrc

it will count how many lines (-l argument) are in our .bashrc file.


sort will sort the output in alphabetical order

sort numbers.txt will sort the prepared file with generated numbers.

*The pipe |
Our first structure here is pipe, which uses |.

The structure looks lie this:

command1 | command2

command1 | command2 | command3

Yes, we can combine as many pipes as we wish.

How it works? The output of command1 is taken over as input to command2. And this process can continue to the next command.

cat (file)  =>  Prints the file

> adds data to file and creates it if needed (rewrites if already exists)

>> append to existing file

print number of lines with 

wc -l numbers.txt
with the folowing we get rid of the name

wc -l numbers.txt | awk '{print $1}'

or...

awk 'END{print NR}' numbers.txt

**Read files

more (filename)
less (filename)

head -n number of lines

tail -n number of lines


** Copy and move files

tree (filename) recursively shows all the files

cp source target

copy

cp one ../targetdir/another-one

copy with changed name

copy source target/name

---------

cp file1tocopy file2copy file3tocopy targetlocation

So, last parameter describes where to copy all files listed in parameters (but last, ofc).

In Linux we have multiple widlcards. We touch here only two.

? this wildcard replaces one character. So, if we wish to copy all files, where the file name start with my and ends with file, but there is something in between, like a, g or 6, but it has to be only one character (so something like my3file, but not myFGfile), I can use ?. It will look like this my?file.
* this wildcard replaces all characters with nay length. Considering last example, if we wish to copy my1file and myFGfile, we will use my*file.

If you wish to learn more about wildcards, run man 7 glob

---------Copy the entire folder/s... -------------

and now we can copy the whole structure:

cp -R sourcedir anotherdir

-R argument means recursively. How to understand this, please take look back on top when we discussed tree

----------------Move Files-------------------------

mv file1 file2 file3 targetlocation


---other options---
cat .profile > newfilewithcontent.txt

--check diff--

diff .profile newfilewithcontent.txt

No output means that both files are the same.