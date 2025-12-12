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
* If the apropos command does not work because your manual pages are not indexed, what command can you use to manually refresh these?
`mandb`
* You are trying to use `ssh alex@localhost` to log in through SSH. Your connection is refused. ssh has a command line option to show you the verbose output. That will show a lot more status messages and help you debug why this connection is failing. What is the correct option for that? (you need not make ssh connection work at this point)
`ssh -v eme@localhost`
* You type `host` in the terminal. What keys do you press to see some suggestions about what you can type here?
`TAB` `TAB`
* What page has System administration commands?
`Section 8`
* How many files are hidden in `/home/bob/data/` ?
`ls --all /home/bob/data/`o `ls -a /home/bob/data/`

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
**Ruta absoluta:** comienza desde la raíz (/). Ejemplo: `/home/eme/Pictures/dog.jpg`
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
rm -r [path_directory]             # remove directory with all content
```

#### Hard Links
**Concepto:** Un hard link apunta al mismo `Inode` que el archivo original.
```bash
stat [file]    # ver Inode de ficheros y directorios (Inode) -> referencia de de almacenamiento y seguimiento de metadatos como:  permisos y fechas de actualización 
               # ver Links - indica a cuantos usuarios del mismo ordenador está compartido el archivo, esto no lo duplica, sólo apuntan al mismo Inode. Si un usuario elimina un archivo compartido, sólo eliminará su Link referenciado al Inode, el otro usuario seguirá visualizando el archivo por que tiene su propio Link to Inode
ln [path_target_file] [path to link file]    # para linkear (share) archivo con varios usuarios.
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


### Lab: Files, Directories, Hard and Soft Links
* What is the top-level directory in Linux?
/
* In what form does Linux organise files and directories?
filesystem tree
* What is the command to print your current working directory?
pwd
* What is the command to climb up one directory?
cd ..
* Absolute paths always start out with the root directory /. Then we specify the sub-directories we want to descend into; /home/bob/Documents/Invoice.pdf is an example of such a path. In this case, first home, then bob, and then Documents. We can see the sub-directory names are separated by a /, and we finally get to the file we want to access, i.e, Invoice.pdf. An absolute path can end with the name of a file or a directory.
As per the example above, If we'd want to delete the Documents directory, how would we specify the path?
/home/bob/Documents/
* Create a directory named lfcs under the /home/bob directory.
cd /home/bob
mkdir lfcs
* Create a blank file named lfcs.txt under the/home/bob/lfcs directory.
touch lfcs.txt
* Copy the /tmp/Invoice directory (including all its contents) to the /home/bob directory.
cp -r /tmp/Invoice/ /home/bob/
* Copy the /home/bob/myfile.txt file to the/home/bob/data/ directory. Make sure to preserve its attributes.
ln myfile.txt data/
* Copy the /home/bob/lfcs directory (including all its content) into the /home/bob/old-data/ directory.
cp -r lfcs/ old-data/
* Delete the /home/bob/lfcs/lfcs.txt file.
rm lfcs/lfcs.txt
* Move all contents, excluding the directory itself, from /home/bob/lfcs to /home/bob/new-data/ directory.
mv lfcs/ new-data/
* Delete directory /home/bob/lfcs .
rm -r lfcs/
* Create a soft link to /tmp directory. Create this link in /home/bob directory and call it link_to_tmp.
ln -s /tmp link_to_tmp
* Create a hard link to /opt/hlink file. Create this link in /home/bob/ directory and call it hlink.
ln /opt/hlink hlink
* There is a file called /home/bob/new_file; rename this to /home/bob/old_file.
mv new_file old_file
* Create a directory named 9 under the /tmp/1/2/3/4/5/6/7/8 directory. Please note that the structure of sub-directories from 1 to 8 does not exist. However, mkdir has a command line option to automatically create all of these sub-directories automatically in one shot, instead of 9 consecutive commands. This option is described in the help output or manual pages as make parent directories as needed. Find out what the correct option is and use it to create the directory in one shot.
     ```bash
     mkdir --help # -p, --parents     no error if existing, make parent directories as needed
     mkdir -p /tmp/1/2/3/4/5/6/7/8/9/
     ```
* ls -l shows you the time when a file has been last modified, but it only shows you the hour and the minute, usually in a form like 17:53. Find another way to make ls display the full/exact last modified time for the files in /home/bob directory.
At what exact time was important_file created/modified?
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
