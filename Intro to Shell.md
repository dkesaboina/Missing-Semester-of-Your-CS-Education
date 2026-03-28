[source](https://missing.csail.mit.edu/)
[full class notes](https://missing.csail.mit.edu/2026/course-shell/)
### What is Shell?
Computers have a bunch of interfaces that we use to interact with them. We are familiar with GUIs (Graphic User Interfaces). Shell or Terminal is the textual interface to a computer. Here you can chain commands and combine commands however you want to create new functionality that is impossible on a GUI. 

On Linux (including Pop Os) we get access to something called 
"BASH" (Born Again Shell). In Mac, you get access to something called "ZSh" (Z Shell). 

* Zsh is a bash compatible shell that is things that are compatible in BASH are compatible in Zsh
* Zsh has ergonomic/aesthetic improvements to Bash that makes it more attractive. 
* Bash is pretty old and has no significant feature improvements in recent times. 
* On Windows you will not get a Bash compatible prompt you will either get a Batch or Powershell

### Why should you get comfortable with Shell?
It is usually much faster than clicking around in GUI to get some work done. One can write fairly complicated expressions to get some work done on Shell, sometimes these actions are slower to execute or impossible to execute on a GUI. 

In the Shell, you can automate. Hence Shell > GUI.

One of the impressive things Shell can pull off is to ability to combine programs. That is to take the output of one program to serve as input to another program. 

Shell also gives the user the ability to understand and contribute to open source projects. 

### What is the shell?
The prompt is the main interface to the shell. 
```
# returns current datetime with day of week
date

# shell's print is called echo
echo hello world

```


**Argument Parsing**
Argument parsing in Bash is that you take the text the  user gave you and you split it at whitespace boundaries. 

**Manual (MAN)**
Man allows you to pass the name of another program and it explains how to use that program. 

**CD**
change directory. 
```
cd /bin
cd /
```

**Relative Path**
Any path that does not use `/`
`.` - Current directory
`..` - Parent directory
`~` - Home directory

**Tab**
Tab in Bash gives you auto complete (useful to auto fill directory or file names)

### What is available in the Shell?
When you type a program in Shell, how does the computer know where to look for this program? PATH. 

#### PATH
PATH is an environment variable set across the whole shell. It contains variables to value mappings (names to strings). 

```shell
echo $PATH
```

PATH is a collection of folder directories that is trying to look for a program you have called in these directories. It will jump from one directory to another in search of the program you are calling. Remember when you had to add programs to PATH in Mac and Linux (even Windows maybe)?

#### WHICH
WHICH  is a program that will walk through the PATH and spit out the first instance of when it finds `date` function. Go ahead and run `which date` now. 

PATH helps us reduce effort by not having to type the full path of the program all the time. Much like a desktop shortcut. Convenience. 

#### Some more useful functions to explore
A file called `sample_data` is created using the command `vi sample_data`. There is a tiny version of vim pre-installed in Pop OS. 
```shell
# display contents of files 
cat sample_data
# sort and remove duplicates
sort -u sample_data
head -n3 sample_data
tail -n5 sample_data
# matching
grep 3 sample_data
# look for the string grep (recursively) starting from the current directory
grep -r grep . 


```

Shells do not support regular expressions for searching paths; for this purpose you can use a glob. 

### Glob
a glob is a pattern-matching technique used to find sets of files or directories based on specific characters.

While "Regular Expressions" (Regex) are like a surgical scalpel for finding text inside files, Globs are the blunt instruments used for finding the files themselves.
1. Common Glob Wildcards

You’ve likely already used globs in the terminal without calling them by name. Here are the characters that make them work:

    * (The Asterisk): Matches any number of characters (including zero).

        Example: ls *.sql finds every SQL file in your folder.

    ? (The Question Mark): Matches exactly one character.

        Example: ls model_?.sql would find model_1.sql and model_a.sql, but not model_10.sql.

    [ ] (Square Brackets): Matches any one character listed inside.

        Example: ls data_[abc].csv finds data_a.csv, data_b.csv, or data_c.csv.

    ** (The Double Asterisk/Globstar): Matches directories recursively.

        Example: ls **/main.py finds every main.py file in the current folder and every subfolder beneath it.

#### Note to self
Master regular expressions. 

#### find
Another useful function that lets you look files under specific conditions. `find` has a large directory of arguments that lets you do very granular searches like files that are at least this large or at most this large etc. Files that are directories, files that are links etc can also be found. 

```
# look up files in directory which are atleast 30 days old
find ~/Downloads -type f -mtime +30

# find can be very advanced
# find all files in my Downloads directory that are at least a 100MB
# for each such file, show ls -lh
# exec takes a command terminated by a stand alone ;
find ~/Downloads -type f -size 100M -exec ls -lh {} \;

# find all python files that have TODO in them. 
find . -name "*.py" -exec grep -l "TODO" {} \;
```

 > find is recursive by nature. When you run `find` it looks for everything in that directory for the file/object you are looking for including other directories.
 > 
 > `find` has an argument called `maxdepth` which can dictate how deep you want find to go in a search. If `maxdepth` is 1 then it means search is limited to the current directory. 


#### awk
 `awk` like `sed` is a program which has its own programming language built in. Where `sed` is for editing files, `awk` is for parsing files. `awk` will by default split a file by lines and white space and will let you write expressions over the result of parsing it that way. 

 
> `awk` is very useful for pulling/parsing data from semi structured files

```shell
# print second column from each row
awk '{print $2}' sample_data

# same as above for a csv file
awk -F, '{print $2}' sample_data
```

### Putting these together
```shell
ssh myserver 'journalctl -u sshd -b-1 | grep "Disconnected from"' \
  | sed -E 's/.*Disconnected from .* user (.*) [^ ]+ port.*/\1/' \
  | sort | uniq -c \
  | sort -nk1,1 | tail -n10 \
  | awk '{print $2}' | paste -sd,
```

`ssh` is a way to run a command on a remote machine. 

> You can add data to a file using commands like 
> ```shell
> -- write tot he file 
date >thedate.txt
 --append to the file
>date >> thedate.txt
>
>```

> 0 is a successful exit status in Linux

#### if

```shell
if grep 2026 thedate.txt; then echo "It's 2026"; echo "HELLO"; fi
```

`test` or `[` can be used to compare variables 

```shell
if [ "hello" = "world" ]; then echo "equal"; else echo "not equal"; fi
if [ -f thedate.txt ]; then echo 'thedate exists'; fi
```
#### while
```shell
# don't run this
while grep 2026 thedate.txt; do echo "It's still 2026"; date > thedate.txt; sleep 10; done
```

#### for
```shell
for varname in a b c d; do echo "$varname"; done
for varname in $(seq 1 10); echo "$varname"; done
```

> `#!` signifies a shebang. When a shell script has this at the start it means it is an `executable`. What is cool about the shell script is that you can change the shebang at the top to `#!usr/bin/python` and the shell script executes a python program from the shell script! In fact you can use this for any programming language that uses textual language as programming input (Python, Julia, Ruby work great). 

> `ls -l` is used to get the rights on a file (executable, write, read etc)