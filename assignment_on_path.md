# PATH
* Is an environment variable that keeps track of certain directories.
* Has the following locations; 
 ```
 /usr/bin
 /usr/sbin
 /usr/local/bin
 /usr/local/sbin
 /bin
 /sbin
 /snap/bin  #if snap is installed
 ```
 * To see what directories are currently registered under PATH on your Terminal...use
```bash
$ echo $PATH
```
![image](https://linuxhint.com/wp-content/uploads/2020/02/1-15-810x95.png)
```bash
$ - denotes a variable.
echo - this command prints the value of the PATH variable.
```
---
# BASHRC
* The .bashrc file is a script file that's executed when a user log in.
* The file itself contains a series of configurations for the terminal session.
* It is a hiddedn file and _ls_ command won't show file.
* To view hidden files you run...
```bash
ls -a
```
![image](https://www.journaldev.com/wp-content/uploads/2020/06/ls-a-command.png.webp)

* To view the bashrc file...
```bash
$ cat .bashrc
```
![image](https://www.journaldev.com/wp-content/uploads/2020/06/cat-bashrc-1.png)
---
## Adding directory to PATH
* To add a custom directory to PATH, we'll use the help of bashrc file.
* Open bashrc file in a text editor.
```bash
$ nano ~/.bashrc
```
* Here it's the default bashrc that comes with Ubuntu. Go to the last of the file and add:
```bash
$ export PATH="$PATH:/<TARGET DIRECTORY>"
```
* Here the new value of PATH variable will be the old variable along with the new directory.
* Save the file and tell bash to reload it. Use..
```bash
$ source ~/.bashrc
```
* To verify if the new path was added, use..
```bash
$ echo $PATH
```
