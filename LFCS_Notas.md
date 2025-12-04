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
