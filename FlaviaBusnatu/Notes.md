What is ls?
This is the list command. It allows us list the content of the directory.

the colorized list of content
ls --color=no
ls --color=yes

clear - to clear the screen

What we pass after the command - these are arguments.
- one dash informs the system that we will pass one letter argument, like 'l'
-- two dashes means that argument will contain more than one letter. Most commonly it will be an english word.

ls -l -> l means long listing format.
ls -s ->  shows the short list of files and allocated space
ex: drwx------           3                  root      root        4096    Jul 22 10:19     snap
   permissions   number of hard links       Owner     Group       Size    date and time of last modification   file name

ls -a -> listed all the files(+hidden files)  
.  means the current directory of the user.
.. means parent directory.

ls -A ->will show all files, except the . and ..(almost all)

Sorting

-t -> sorts files with the last modification time, newest files come first.
-tc -> last metadata modification time- permissions change, location of the file, etc
-lS -> sorts files by size, largest are going first.
-lh  -> printed the size of the files not in bytes but in K, M, or G.
        h use the powers of 1024. So, 1K is a 1 powered by 1024.

ls --format=commas will print the files separated by commas = ls -m
ls -lQ prints the filenames in quotes
--time-style changes the way how the date is formated in long format

ls -al --author prints the username of the creator of the file
ls -ald prints directories only
ls -ali prints inodes
ls -alR recursively prints all subdirectories
ls -alr prints list in the reversed order

MAN
q -> quit
man 8 ls -> go to the page 8 for ls
man -f ls -> to see what sections/pages we have available
man -f intro -> shows us multiple sections available
whatis ls shows short description of the functionality = man -f ls
