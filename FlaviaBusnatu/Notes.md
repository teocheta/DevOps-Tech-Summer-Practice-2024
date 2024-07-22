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
ex: drwx------           3                  root      root        4096    Jul 22 10:19     snap
   permissions   number of hard links       Owner     Group       Size    date and time of last modification   file name

ls -a -> listed all the files(+hidden files)  
.  means the current directory of the user.
.. means parent directory.

ls -A ->will show all files, except the . and ..(almost all)

