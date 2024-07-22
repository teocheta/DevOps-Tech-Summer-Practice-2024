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
