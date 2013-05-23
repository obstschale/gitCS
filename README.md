# gitCS

gitCS is my cheat sheet repo. There are so many nice git commands, scripts and tweaks out there to improve your git experience. But I cannot remember all of them so I will collect them here.

If you know a nice git command or maybe you have a good script feel free to send a pull request.

---
## git aliases

**pretty online log**

`git log --all --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit`

![pretty git log](images/git-log.png)

## one liner (cmd)

**count lines of all files in git repo**

* outputs the total number of loc
	* `git ls-files | xargs cat | wc -l`
* outputs loc for each file & sum
	* `git ls-files | xargs wc -l`

## scripts

all scripts can be found in the `scripts` folder

### git-loglive
Shows and updates the git log live.

```sh
#!/bin/bash
 
while :
do
    clear
    git --no-pager log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%ci) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative --all
    sleep 1
done
```

### generaterandomchanges

Will generate random files and commit them. Good for seminars and workshops.

Usage: `generaterandomchanges <filecount> <filenamebase> <filenameextension>`

```sh
#!/bin/bash
 
#Ensure we have the quantity specified on the CLI
if [ -z "$3" ]; then ARG_ERR=ERR; fi
if [ -z "$2" ]; then ARG_ERR=ERR; fi
if [ -z "$1" ]; then ARG_ERR=ERR; fi
if [ -n "$ARG_ERR" ];
then
    echo "Usage: <filecount> <filenamebase> <filenameextension>"
    exit
fi
 
count=$1
filenamebase=$2
filenameextension=$3
for (( filenumber = 1; filenumber <= $count ; filenumber++ )); do
    echo "Some new random text: $RANDOM" >> $filenamebase$filenumber.$filenameextension
    git add $filenamebase$filenumber.$filenameextension
    git commit -m"A random change of $RANDOM to $filenamebase$filenumber.$filenameextension"
done
```

---
### Sources

* [@tlberglund](https://github.com/tlberglund) → [git-loglive](https://gist.github.com/tlberglund/3714970)
* [@matthewmccullough](https://github.com/matthewmccullough) → [generaterandomchanges](https://github.com/matthewmccullough/scripts/blob/master/generaterandomchanges)
