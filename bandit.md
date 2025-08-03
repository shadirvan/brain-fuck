#### level 0 -> 1
- The password is obtained from the readme file of user bandit0 from level 0.
- in bandit1 uesr home there is a `-` file.
#### level 1 -> 2
- The password is stored in this ''-" file.
- reading the dashed file name confuses the argument so specify the full path can give the output.
#### Level 2 -> 3
- The file name is "--spaces in this filename--" this time.
- I simply used the escape sequence ''\' : `cat ~/--spaces\ in\ this\ filename--`
#### Level 3 -> 4
- The file was in the directory `inhere` cd into the directory.
- The file is hidden use `ls -al`
- `cat ...Hiding-From-You`
#### Level 4->5
- There were multiple files in `inhere` directory
- catting the `-file07` with full path gives the password.
#### Level 5 -> 6
- Three were lot of directories in `inhere`
- based on the hints the file is not executable, is 1033 bytes long.
- so we can use the command : `find ~/inhere -type f -not -executable -size 1033c`
#### Level 6->7
- The file is owned by user bandit7 , owned by a group bandit6 and has a size of 33 bytes
- So the command to find the file is :
- `find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null`
- cat the file to get the output.
#### Level 7 -> 8
- The data.txt file contains a lot of data.
- but the password is next to the word `millionth`
- use the command : `grep "millionth" data.txt`
#### Level 8 -> 9
- The password is only mention once in the data.txt file
- combining the sort and uniq command could result in the expected output.
- `cat data.txt | sort | uniq -c`
- The one with the count 1 is the password.
#### Level 9->10