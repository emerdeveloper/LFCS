# 🐧 Linux Foundation Certified Systems Administrator (LFCS) - Notas del Curso

---

## ✅ Información General
- **Curso:** Linux Foundation Certified Systems Administrator (LFCS)
- **Instructor:** Mumshad Mannambeth
- **Objetivo:** Preparación para examen práctico LFCS
- **Estado:** En progreso

---

## 📂 Índice
1. Comandos Básicos
2. Gestión de Usuarios y Grupos
3. Networking
4. Almacenamiento y Filesystem
5. SSH y Seguridad
6. Hard Links y Soft Links
7. Tips y Tareas Prácticas

---

## 📝 Notas Actuales del Curso

### Preguntas
* If the `apropos` command does not work because your manual pages are not indexed, what command can you use to manually refresh these?
`mandb`
* You are trying to use `ssh alex@localhost` to log in through SSH. Your connection is refused. ssh has a command line option to show you the verbose output. That will show a lot more status messages and help you debug why this connection is failing. What is the correct option for that? (you need not make ssh connection work at this point)
`ssh -v eme@localhost`
* You type `host` in the terminal. What keys do you press to see some suggestions about what you can type here?
`TAB` `TAB`
* What page has `System administration` commands?
`Section 8`
* How many files are hidden in `/home/bob/data/` ?
`ls --all /home/bob/data/` o `ls -a /home/bob/data/`

* SSH into `node01` host from `ubuntu-host` and create a blank file called `/home/bob/myfile` in `node01` host.
You should be able to create the file using `touch /home/bob/myfile` command.
Please find below the SSH credentials for `node01` host:
   ```bash
   Host: node01
   Username: bob
   Password: caleston123
   ```

* We are trying to run the `apropos ssh` command to get some details about the commands related to ssh, but we are getting this error:
`ssh: nothing appropriate`
Look into the issue and fix it to make the apropos ssh command work.
`sudo mandb`

* Using the `apropos` command, find out the configuration file for NFS mounts and save its name in the `/home/bob/nfs` file.
`apropos "NFS mount"`
The output will be the content of file 

---

### Notas sobre Comandos y Conceptos de Linux

#### Listing Files and directories | Listar Archivos y Directorios

```bash
ls -al    # Lista en formato largo + archivos ocultos
ls -a     # Incluye archivos ocultos
ls -l     # Formato largo/detallado (permisos, propietario, fecha)
ls -ld    # Formato largo/detallado (permisos, propietario, fecha) de directorios
ls -l -a  # Formato largo + ocultos (archivos pseudo ocultos que comienzan con .)
ls -lh    # Formato largo con tamaños legibles (human-readable)
```

#### File system tree | Estructura del Sistema de Archivos
**Árbol invertido:** La parte superior es la raíz y crecen hacia abajo ramas y hojas
```
/
├── home
│   ├── eme
│   └── ale
├── var
│   └── log
└── root
```

#### Paths | Rutas
**Ruta absoluta:** comienza desde la raíz (`/`). Ejemplo: `/home/eme/Pictures/dog.jpg`
**Ruta relativa:** comienza a partir de una directorio actual (Current working Directory)

**Comandos útiles:**
```bash
pwd       # print working directory
cd        # go to Home directory
cd /      # go to root directory
cd -      # go to previous directory
```

#### Files and Directories | Operaciones con Archivos y Directorios
```bash
touch [file.txt]              # create empty files
mkdir [directory]             # create directories
cp [source] [destination]     # copy copiar archivos
cp -r [source] [destination]  # recursive - copy directory with all content
mv [source] [destination]     # move/rename - file or directory
rm [path_file]                # remove - delete file
rm -r [path_directory]        # remove directory with all content
```

#### Hard Links
**Concepto:** Un hard link apunta al mismo `Inode` que el archivo original.
```bash
stat [file]    # ver Inode de ficheros y directorios (Inode) -> referencia de de almacenamiento y seguimiento de metadatos como:  permisos y fechas de actualización 
               # ver Links - indica a cuantos usuarios del mismo ordenador está compartido el archivo, esto no lo duplica, sólo apuntan al mismo Inode. Si un usuario elimina un archivo compartido, sólo eliminará su Link referenciado al Inode, el otro usuario seguirá visualizando el archivo por que tiene su propio Link to Inode
ln [path_target_file] [path_to_link_file]    # para linkear (share) archivo con varios usuarios.
                                             # create hard link
```
**Caracteristicas y Limitaciones**
* Sólo se pueden establecer con archivos, no directorios.
* Sólo con archivos del mismo sistema, no con un almacenamiento externo.
* Tener en cuenta de tener los permisos necesarios para aceder al archivo (asignar todos los nombres de usuarios al mismo grupo)
```bash
  useradd -a -G family aron
  useradd -a -G family alex
  chmod 660 /home/aron/Pictures/picture.jpg
```

#### Soft Links | Enlaces simbólicos
**Concepto:** actúan como accesos directos al archivo o directorio.
```bash
ln -s [path_target] [path_link]    # create soft link
ls -l                              # para verificar si tiene un softlink los archivos o directorios 
                                   # start with 'l'
readlink [file]                    # Show path of original file
```
**Caracteristicas**
* Sirve con ficheros y directorios de otros almacenamientos externos (different filesystems).


#### Lab: Files, Directories, Hard and Soft Links
* What is the top-level directory in Linux?
`/`
* In what form does Linux organise files and directories?
`filesystem tree`
* What is the command to print your current working directory?
`pwd`
* What is the command to climb up one directory?
`cd ..`
* Absolute paths always start out with the root directory `/`. Then we specify the sub-directories we want to descend into; `/home/bob/Documents/Invoice.pdf` is an example of such a path. In this case, first home, then bob, and then Documents. We can see the sub-directory names are separated by a `/`, and we finally get to the file we want to access, i.e, `Invoice.pdf`. An absolute path can end with the name of a file or a directory.
As per the example above, If we'd want to delete the Documents directory, how would we specify the path?
`/home/bob/Documents/`
* Create a directory named `lfcs` under the `/home/bob` directory.
  ```bash 
  cd /home/bob
  mkdir lfcs
  ```
* Create a blank file named `lfcs.txt` under the `/home/bob/lfcs` directory.
`touch lfcs.txt`
* Copy the `/tmp/Invoice` directory (including all its contents) to the `/home/bob` directory.
`cp -r /tmp/Invoice/ /home/bob/`
* Copy the `/home/bob/myfile.txt` file to the `/home/bob/data/` directory. Make sure to preserve its attributes.
`ln myfile.txt data/`
* Copy the `/home/bob/lfcs` directory (including all its content) into the `/home/bob/old-data/` directory.
`cp -r lfcs/ old-data/`
* Delete the `/home/bob/lfcs/lfcs.txt` file.
`rm lfcs/lfcs.txt`
* Move all contents, excluding the directory itself, from `/home/bob/lfcs` to `/home/bob/new-data/ directory`.
`mv lfcs/ new-data/`
* Delete directory `/home/bob/lfcs` .
`rm -r lfcs/`
* Create a soft link to `/tmp` directory. Create this link in `/home/bob` directory and call it `link_to_tmp.`
`ln -s /tmp link_to_tmp`
* Create a hard link to `/opt/hlink` file. Create this link in `/home/bob/` directory and call it hlink.
`ln /opt/hlink hlink`
* There is a file called `/home/bob/new_file`; rename this to `/home/bob/old_file`.
`mv new_file old_file`
* Create a directory named `9` under the `/tmp/1/2/3/4/5/6/7/8` directory. Please note that the structure of sub-directories from 1 to 8 does not exist. However, mkdir has a command line option to automatically create all of these sub-directories automatically in one shot, instead of `9` consecutive commands. This option is described in the help output or manual pages as make parent directories as needed. Find out what the correct option is and use it to create the directory in one shot.
     ```bash
     mkdir --help # -p, --parents     no error if existing, make parent directories as needed
     mkdir -p /tmp/1/2/3/4/5/6/7/8/9/
     ```
* `ls -l` shows you the time when a file has been last modified, but it only shows you the hour and the minute, usually in a form like `17:53`. Find another way to make ls display the full/exact last modified time for the files in `/home/bob` directory.
At what exact time was `important_file` created/modified?
     ```bash
     ls --help # --full-time            like -l --time-style=full-iso
     ls -l --time-style=full-iso
     ```


### Owners and Groups

* Sólo el usurio propierario del archivo o directorio puede cambiar los permisos además del usuario `root`
* Sólo el usuario root puede cambiar el propietario de un archivo o directorio

```bash
ls -l 
# output: -rw-r--r--@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
# emer is owmer of configmap.yaml file
```
```bash
chgrp [group_name] [file/directory] # chage group of file/directory
chgrp family configmap # -rw-r--r--@ 1 emer  family   234455 Oct 29 08:57 configmap.yaml
groups # show which groups our current user belongs to
sudo chown [user_name] [file/directory] # change the owner of file/directory
sudo chown lex configmap.yaml # -rw-r--r--@ 1 lex  staff   234455 Oct 29 08:57 configmap.yaml
sudo chown [user:family] [file/Directory] # revert the owner
sudo chown emer:staff configmap.yaml # -rw-r--r--@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
```

### File and Directory Permissions
```bash
ls -l 
# output: -rw-r--r--@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
```
First character tell us the type : 
`d` - directory
`l` - soft link
`-` - regular file

The next 9 characters tell us the permissions:
first 3 characters: owner permissions: `rw-`
next 3 characters: group permissions: `r--`
last 3 characters: other users permissions: `r--`

**Characters for files purposes**
 
 
| bit | Purpose        | 
| ----|----------------|
| r   | Read File      |
| w   | Write to File  |
| x   | Execute (run)  |
| -   | No permissions |

**Characters for files purposes**

| bit | Purpose        | 
| ----|----------------|
| r   | Read content Directory |
| w   | Write into Directory  |
| x   | Execute into (run)  |
| -   | No permissions |

**Adding Permissions**
```bash
chmod u+[permissions] [file/directory] # change permissions
chmod u+x configmap.yaml # -rwxr--r--@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
```
|   | option   | example |
|---|----------|---------|
|user| u+      | u+w / u+rw / u+rwx |
|group| g+     | g+w / g+rw / g+rwx |
|others| o+    | o+w / o+rw / o+rwx |

**Removing Permissions**
```bash
chmod u-[permissions] [file/directory] # change permissions
chmod u-x configmap.yaml # -rw-r--r--@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
```
|   | option   | example |
|---|----------|---------|
|user| u-      | u-w / u-rw / u-rwx |
|group| g-     | g-w / g-rw / g-rwx |
|others| o-    | o-w / o-rw / o-rwx |

**Setting exact Permissions**
```bash
chmod u=[permissions] [file/directory] # change permissions
chmod u=x configmap.yaml # -r--r--r--@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
```
|   | option   | example |
|---|----------|---------|
|user| u=      | u= / u=w / u=rw / u=rwx |
|group| g=     | g= / g=w / g=rw / g=rwx |
|others| o=    | o= / o=w / o=rw / o=rwx |

both command have the same effect: 
```bash
chmod g= configmap.yaml
chmod g-rwx configmap.yaml
#result: -r--r-----@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
```

we can mix options:
```bash
chmod u+rw, g=r, o= configmap.yaml
#result: -rw-r-----@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
```

**Octal Permissions**

|permissions|value|
|-----------|-----|
|r          |4    |
|w          |2    |
|x          |1    |

|user|group|others|
|----|-----|------|
|rw- | r-- |  --- |
| 6  |  4  |   0  |
|rwx | r-x |  r-x |
| 7  |  5  |   5  |
|rwx | rwx |  rwx |
| 7  |  7   |   7  |

```bash
chmod 640 configmap.yaml
#result: -rw-r-----@ 1 emer  staff   234455 Oct 29 08:57 configmap.yaml
```

### SUID, SGID and Sticky Bit

**SUID** A special permission that allow users to run an executable with the permissions of the executable's owner.

```bash
ls -l executableFileSUID
# Result: -rw-rw-r--@ 1 emer  staff   234455 Oct 29 08:57 executableFileSUID
chmod 4664 executableFileSUID # set 4 to indicate bit SUID for user
# Result: -rwSrw-r--@ 1 emer  staff   234455 Oct 29 08:57 executableFileSUID
# The capital S allows us to know that the SUID is active for this file,
# But there is not executable permission
chmod 4764 executableFileSUID # set 4 to indicate bit SUID 
# Result: -rwsrw-r--@ 1 emer  staff   234455 Oct 29 08:57 executableFileSUID
# The lower s allows us to know that the SUID is active for this file,
# And  there is executable permission
```

If anyone else runs the file, it would run as emer's user  instead of the user who ran it

**Find file** with `SUID`permision
```bash
find . -perm /4000
# Result: executableFileSUID
```


 **SGID** Is similar to SUID but, appies to both executable and directories.

```bash
chmod 2664 executableFileSGID # set 2 to indicate bit SGID for group
# Result: -rw-rwSr--@ 1 emer  staff   234455 Oct 29 08:57 executableFileSGID
chmod 2674 executableFileSGID # set 2 to indicate bit SGID for group
# Result: -rw-rwsr--@ 1 emer  staff   234455 Oct 29 08:57 executableFileSGID
```

**Find file** with `SGID`permision
```bash
find . -perm /2000
# Result: executableFileSGID
```

**Set SUID and SGID at same time**

```bash
chmod 6664 executableFileBoth # set 6 to indicate 4+2 SUID and SGID
# Result: -rwSrwSr--@ 1 emer  staff   234455 Oct 29 08:57 executableFileBoth
chmod 6674 executableFileBoth # set 6 to indicate 4+2 SUID and SGID
# Result: -rwSrwsr--@ 1 emer  staff   234455 Oct 29 08:57 executableFileBoth
```
**Find file** with `SGID or SUID`permision
```bash
find . -perm /6000
# Result: 
# executableFileBoth
# executableFileSGID
# executableFileSUID
```

 **Sticky Bit** A especial permission that can be set on directories. It restricts file deletion in that directory.
 Only File owner, Directory owner or s uperuser (root) can delete it.

```bash
ls -ld stickyDir/
# Result: drwxrwxr-x@ 1 emer  staff   234455 Oct 29 08:57 stickyDir/
chmod 1777 stickyDir/ # set 1 to indicate Sticky Bit
# Result: drwxrwxrwt@ 1 emer  staff   234455 Oct 29 08:57 stickyDir/ 
chmod 1666 stickyDir/ # set 1 to indicate Sticky Bit
# Result: drw-rw-rwT@ 1 emer  staff   234455 Oct 29 08:57 stickyDir/ 
```

### Search Files
```
/
├── usr
│   ├── share
├── var
│   └── log
├── etc
│   └── ssh
└── root
``` 

**find**
To search files
* Name
```bash
find [path_directory/] [search_parameters]
find /bin/ -name file1.txt
find [search_parameters] # With no path -> search in current directory
find -name file1.txt
find -iname file1 # ignore case sensitive
find -name "f*" # match all names starting with f 
```

* Modified Time (content/data)
Modificaton = Create or Edit 
```bash
find -mmin [minute]
find -mmin 5 # exactly modified 5 minutes ago 
find -mmin -5 # modified from now to last 5 minutes 
find -mmin +5 # modified from last 5 minutes to older 
find -mtime [24h_period]
find -mtime 2 # work with 24h periods
```
* Modified Time (metadata)
example: change permissions
```bash
find -cmin [minute]
find -ctime [24h_period]
```

* Size
```bash
find -size [size]
# c -> bytes
# k -> kilobytes
# M -> megabytes
# G -> gigabytes
find -size 512k # exactly 512 kb
find -size +512k # greater than 512 kb
find -size -512k # less than 512 kb
```

* Combine expresions
```bash
find -name "f*" -size 512k # AND operator 
find -name "f*" -o  -size 512k # OR operator 
find -not -name "f*" # NOT Operator - exclude
find \! -name "f*" # NOT Operator - exclude
```

* Permissions 
```bash
Permissions: 664 = u+rw, g+rw, o+r
find -perm 664 # find files with exactly 664 permissions
find -perm u+rw,g+rw,o+r # find files with exactly 664 permissions. 
find -perm -664 # find files with at least 664 permissions
find -perm /664 # find files with any of these permissions

find -perm 600 # find files where owner user only can read
find -perm -100 # find files where owner user at least can execute
find \! -perm -o=r # find files where others can read
find -pem /u=r,g=r,o=r # find files where evereyone can read
```

#### Lab - File Permissions, Search for Files
* What command can be used to find files and directoriesmodified in the last 5 minutes in the `/dev` directory?
`find /dev/ -mmin -5`
* What command removes the write permission for the group from a file?
`chmod g-w some_file`
* Find files/directories under the `/var/log/` directory that the group can write to, but others cannot read or write to it. Save the list of the files/directories (with complete parent path) in the `/home/bob/data.txt` file.

   You can use the redirection to save your command's output in a file i.e `[your-command] > /home/bob/data.txt`


   To make this easier to understand, the logic of the command can be broken down like this:

   - Permissions for the group have to be at least `w`. If there's also an extra `r or x` in there, it will still match.

   - Permissions for others have not to be `r or w`. That means, if any of these two permissions, `r or w`, match for others, the result has to be excluded.

     ```bash
     find /var/log/ -perm /g+w,o-rw > /home/bob/data.txt
     find /var/log/ -perm -g=w,o-rw > /home/bob/data.txt
     ```

* Find our secret file under `/home/bob`. You can either look for a file that is exactly `213 kilobytes` or a file that has permission `402 in octal`.


  Save the name (including the parent directory path) of this file in the `/home/bob/secfile.txt` file.

  You can use the redirection to save your command's output in a file: `[your-command] > /home/bob/secfile.txt`

     ```bash
     find /home/bob/ -size 213k > /home/bob/secfile.txt
     find /home/bob/ -perm 402 > /home/bob/secfile.txt
     ```

* In our lessons, we briefly mentioned the `setuid`, `setgid`, and `sticky bit` special permissions. Consider that `setuid` is short `for set user id` and `setgid` is short for `set group id`.


  Add the permissions for `setuid`, `setgid`, and `sticky bit` on the `/home/bob/datadir` directory.

     ```bash
     ls -ld /home/bob/datadir/
     #result: drwxr-xr-x 2 bob bob 4096 Dec 13 03:06 /home/bob/datadir/
     chmod 7755 /home/bob/datadir/
     # result: drwsr-sr-t 2 bob bob 4096 Dec 13 03:06 /home/bob/datadir/
     ```

* Find the `dogs.txt` file under the `/usr/share` directory.

  Save the location of the file in the `/home/bob/dogs` file.

  `find /usr/share/ -name dogs.txt > /home/bob/dogs`

* Find the `cats.txt` file under `bob's` home directory and copy it into the `/opt` directory.

     ```bash
     find /home/bob/ -name cats.txt
     # Result: /home/bob/.etc/h/e/r/cats.txt
     sudo cp /home/bob/.etc/h/e/r/cats.txt /opt/
     ls -l /opt/
     # Result: -rw-r--r-- 1 root root    5 Dec 13 03:25 cats.txt
     ```

* Find all directories named pets in the `/var/directory` and save the output (along with directory path) in the `/home/bob/pets.txt` file.
  You should be able to save the output in a file using redirection: `<your-command> > /home/bob/pets.txt`

     `sudo find /var/ -name pets > /home/bob/pets.txt`

* Find all the files whose permissions are `0777` in `/var` directory.
      `find /var/ -perm 0777`

* Find all the files whose permissions are `0640` in `/usr/` directory and save the output (along with parent path) in `/home/bob/.opt/permissions.txt` file.
You should be able to save the output in a file using redirection: `<your-command> > /home/bob/.opt/permissions.txt`

     ```bash
      sudo find /usr/ -perm 0640
      # /usr/local/test.txt
      # /usr/games
      # /usr/games/test2.txt
      # /usr/games/test.txt
      # /usr/src/test.txt
      sudo find /usr/ -perm 0640 -name "test*" > /home/bob/.opt/permissions.txt
      sudo find /usr/ -type f -perm 0640 > /home/bob/.opt/permissions.txt
     ```

* Find all the files which have been modified in the last 2 hours in `/usr` directory.
`sudo find /usr/ -type f -mmin -120`

* Find all the files which have been modified in the last 30 minutes in the `/var` directory.
  `sudo find /var/ -type f -mmin -30`

* Find all the files with size `20MB` in `/var` directory.
  `sudo find /var/ -type f -size 20M`

* Find all files between `5mb` and `10mb` in the `/usr` directory and save the output (along with parent path) in the`/home/bob/size.txt` file.

  You should be able to save the output in a file using redirection: `<your-command> > /home/bob/size.txt`
  `sudo find /usr/ -type f -size -10M -size +5M > /home/bob/size.txt`

* create `LFCS` directory under `bob's` home directory and update permissions to owner permissions only `read` and groups and others `have not to be r, w, x`

  ```bash
  mkdir /home/bob/LFCS
  chmod 100 /home/bob/LFCS/
  ls -ld /home/bob/LFCS/
  # result: d--x------ 2 bob bob 4096 Dec 15 23:25 /home/bob/LFCS/
  ```

* Update the permissions for `some_directory` to `rwxr-xr-x`
   ```bash
   sudo find -name some_directory # ./some_directory
   ls -ld ./some_directory # d--------- 2 bob bob 4096 Dec 15 23:24 ./some_directory
   chmod 755 ./some_directory
   ls -ld ./some_directory # drwxr-xr-x 2 bob bob 4096 Dec 15 23:24 ./some_directory
  ```


### Compare and manipulate file content

**cat**
Show file content from the up to bottom
`cat [file_path]`

**tac**
Show file content from then bottom to up
`tac [file_path]`

**tail**
By default show the last 10 lines.
We can indicate how many lines to show.
```bash 
tail [file_path] # By default show the last 10 lines.
tail -n 20 [file_path] # indicate how many lines to show
```

**head**
By default show the first 10 lines.
We can indicate how many lines to show.
```bash 
head [file_path] # By default show the first 10 lines.
head -n 20 [file_path] # indicate how many lines to show
```

**sed** - **s**tream **ed**itor
Search and replace all the requiered text
```bash 
sed 's/canda/canada/g' [file_path] # previsualize changes without save it
# s/ -> search
# /g -> global
# will search and reaplce canda to canada in all file content

sed 's/canda/canada/' [file_path] # previsualize changes without save it
# will search and reaplce canda to canada in the first one coincidence

sed -i 's/canda/canada/g' [file_path]  # edit file with changes and save it
# -i -> --in-place

sed -i 's/disabled/enabled/gi' /home/bob/values.conf # ignore case sensitive
sed -i '500,2000s/enabled/disabled/g' /home/bob/values.conf # search and replace in file from line number 500 to 2000
sed -i 's~#%$2jh//238720//31223~$2//23872031223~g' /home/bob/data.txt # search and replace values contains / to don't confuse use ~
```

**cut**
cut file content with delimiter
```bash
cut -d ' ' -f 1 [file_path]
# -d ' '  -> delimiter
# -f 1    -> specify the fields we want to extract
# will cut the first word of file and show the previsualize

cut -d ',' -f 3 [file_path] > [file_path]
# will cut the third colunm of file and save result in another file
```

**uniq**
remove the repeated lines that are next to each other
`uniq countires.txt`

**sort**
sort entries the files alphanumeric
`sort countires.txt`

```bash
sort countires.txt | uniq
# send the sort command output to uniq comand with pipe |
```

**diff: Comparing files**
**diff**erences
`diff [file1] [file2]`

**c**ontent
`diff -c [file1] [file2]`

**s**yde-by-side **diff**
```bash
sdiff [file1] [file2]
diff -y [file1] [file2]
# are the same command
```

### Pagers and Vi

**less**
Open file in a pager
```bash
less [file_path] # show file
# with / -> search words in file 
# with n -> navigate to next coincidence (down)
# with n -> navigate to previous coincidence (up)
# with /[word]\c -> search words with not case sesitive
```
**more**
Works similar to **less**
`more [file_path]`

**vim**
To create or edit files
```bash
vim [file] # create or open file to edit it
# with i       -> insert text in file
# with i       -> insert text in file 
# with :wq     -> Write and quick - save and exit
# with :q!     -> exit without save
# with /[word] -> search words in file 
# with /[word]\c  -> search words with not case sesitive
# with yy      -> copy entire line
# with dd      -> cut entire line
# with p       -> paste text 
# with :[number] -> go to number line
# with [number]dd -> select the first [number] lines and delete it
```

### Searh with grep

```bash
grep -i --color '[word]' [path_file] # -i -> ignore case sensitive
grep -i -c '[word]' [path_file] # -c -> context: return number of coincidences 
grep -r '[word]' [path_directory] # -r -> recursive option 
# search throw all files that exists in directory and subdirectories
grep -r -c'[word]' [path_directory] # -c -> context: return files and number of coincidences  
grep -ri '[word]' [path_directory] # -i -> ignore case sensitive
grep -vi '[word]' [path_file] # -v -> invert-macth: search lines when don't contain the text 
grep -wi '[word]' [path_file] # -w -> words : seach exactly coincidence
grep -oi '[word]' [path_file] # -o -> only-matching : return only the word if exists 
```

### Regular Expressions

|Operators|Action| Example | Extended |
|---------|------|----------|---------|
|^        | The line begins with | grep '^PASS ' /etc/login.defs |
|$        | The line ends with | grep 'mail$' /etc/login.defs |
|.        | Match any one character | grep -r  'c.t' /etc/ |
|\        | Escaping for special characters| grep -r  '\\.' /etc/loign.defs | grep -Er '.' /etc/  <br> egrep -r '. ' /etc/ |
|*        | Match the previous element 0 or more times| grep -r 'let*' /etc/loing.defs |
|+ special| Match the previous element 1 or more times | grep -r '0\\+' /etc/ |grep -Er '0+' /etc/  <br> egrep -r '0+' /etc/|
|?        | Make the previous element optional (0 o 1 times )| | egrep -r 'disabled?' /etc/|
|\|       | Match one thing or the other (left or right)| | egrep -r 'enable\ |disabled' /etc/|
|[]       | Ranges or sets [a-z] [0-9]| | egrep -r 'c[au]t' /etc/| 
|()       | Subexpressions (hierarchy)| | egrep -r '/dev/(([a-z])*[0-9]?)*' /etc/ <br> egrep -r '/dev/(([a-z]\|[A-Z])*[0-9]?)*' /etc/ | 
|[^]      | Negated Ranges or sets | | egrep -r 'https[^:]' /etc/ <br> egrep -r 'http[^s:]' /etc/ <br> egrep -r '/[^a-z]' /etc/  |
|{[min],[max]} <br> {[exactly]}       | Previous element can exist this many times | | egrep -r '0{3,}' /etc/ <br> egrep -r '10{,3}' /etc/ <br> egrep -r '0{ 3}' /etc/|

**Combine operators**
```bash
# .*
grep '/.*/' /etc/login.defs
# Begins with /
# Has 0 or more characters between
# ends with a /
#Result: 
# /usr/ 
# /usr/share

grep -r '/dev/.*' /etc/ # many coincidences
grep -r '/dev/[a-z]*' /etc/
# * amplify the search 
grep -r '/dev/[a-z]*[0-9]' /etc/ # results must end with a number
grep -r '/dev/[a-z]*[0-9]?' /etc/ # make optional end with a  number
```

#### Lab: File Content, Regular Expressions

* Which of the following commands can be used to manipulate strings in a file?
`sed`

* Which of the following commands will you use to display the top 5 lines of a file called `myfile`?
`head -5 myfile`

* Which of the following commands can you use to filter out the lines that contain a particular pattern?
`grep`

* How can we ignore the case (small or capital) differences while comparing two files using the `diff` command?
`diff -i`

* You have the following content in `/home/bob/testfile` (this is just an example file):
  ```
  a;b;c;d
  x;y;z
  ```
  How would you extract/print the `b` and the `y`?
  `cut -d ';' -f 2 testfile`

* Change all values `enabled` to `disabled` in the `/home/bob/values.conf` config file.
 `sed -i 's/enable/disabled/g' /home/bob/values.conf`

* Change all values `disabled` to `enabled` in the `/home/bob/values.conf` config file, ignoring the case sensitivity.

  For example, any string like `disabled`, `DISABLED`, `Disabled`, etc., must match and should be replaced with `enabled`.

  `sed -i 's/disabled/enabled/gi' /home/bob/values.conf`

* Change all values `enabled` to `disabled` in the `/home/bob/values.conf` config file from line number `500` to `2000`.

  `sed -i '500,2000s/enabled/disabled/g' /home/bob/values.conf`

* Replace all occurrences of string `#%$2jh//238720//31223` with `$2//23872031223` in the `/home/bob/data.txt` file.
  `sed -i 's~#%$2jh//238720//31223~$2//23872031223~g' /home/bob/data.txt`

* Open the `/home/bob/testfile` file in any editor (vi, nano etc) and move the line present on line no:`1049` to line no: `5`.
  ```bash
  vim /home/bob/testfile
  :1049
  yy
  :1
  p
  :wq
  ```
* Delete the first `1000` lines from the `/home/bob/testfile` file.
   ```bash
   vim /home/bob/testfile
   :1,1000d
   :wq
   ```

* In the `/home/bob/textfile` file, there's a number that has `5 digits`. Save the number in the `/home/bob/number` file.

  `egrep -r '[0-9]{5}' /home/bob/textfile > /home/bob/number`

* How many numbers in `/home/bob/textfile` begin with the number `2`. Save the count in the `/home/bob/count` file.

  `egrep -rc '^2' /home/bob/textfile > /home/bob/count`

* How many lines in the /home/bob/testfile file begin with string Section, regardless of case.
Save the count in the /home/bob/count_lines file.

  `egrep -rci '^Section' /home/bob/testfile > /home/bob/count_lines`

* Find all lines in the/home/bob/testfile file that contain string man; it must be an exact match.

  For example, the line like # before /usr/man or NOCACHE keeps man should match but # given manpath for For a manpath must not match.


  Save the filtered lines in the /home/bob/man_filtered file.

  `grep -w man /home/bob/testfile >  /home/bob/man_filtered`

* Save the last 500 lines of the /home/bob/textfile file in the /home/bob/last file.
  `tail -500 /home/bob/textfile > /home/bob/last`

--- 

## 🔹 Tips para el examen
- Usa `hostnamectl` para cambiar el hostname.
- Si `apropos` falla, ejecuta `sudo mandb`.
- Para debug en SSH: `ssh -v usuario@host`.
- Comandos de administración → sección 8 del manual.

---

## ✅ Recursos recomendados
- [Linux Journey](https://linuxjourney.com)
- [Linux Foundation Free Courses](https://training.linuxfoundation.org/resources/free-courses/)
- [Arch Wiki](https://wiki.archlinux.org)
