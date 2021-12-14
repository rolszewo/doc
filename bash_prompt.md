# customizing the bash prompt

```bash
# see the git branch
gitPS1(){  
 gitps1=$(git branch 2>/dev/null | grep '*')  
 gitps1="${gitps1:+ (${gitps1/#\* /})}"  
 echo "$gitps1"  
}  
 
# -ANSI-COLOR-CODES- #  
Color_Off="\033[0m"  
Red="\033[0;31m"  
Green="\033[0;32m"  
Yellow="\033[0;33m"  

# see, if last command was sucessful 
__stat() {  
 if [ $? -eq 0 ]; then  
   echo -en "$Green OK $Color_Off "  
 else  
   echo -en "$Red NOK $Color_Off "  
 fi  
}  

# set PS1
if [ "$color_prompt" = yes ]; then  
   PS1='$(__stat)${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$(gitPS1)\$ '  
else  
   PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '  
fi 
```
