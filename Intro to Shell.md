[source](https://missing.csail.mit.edu/)

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



