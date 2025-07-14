# Comanandos

## help 

- Obtiene un resumen breve de uso de un built-in del shell. Este es el equivalente a whatis, pero para comandos integrados. La visualización de la información de ayuda recibió una actualización muy necesaria en la versión 4 de Bash.

He agregado esta información al documento con:

📖 Descripción completa: Explicación de qué hace y su relación con whatis

💡 Ejemplos prácticos: Cómo usar help con diferentes opciones

⚡ Ventajas: Por qué usar help en lugar de man para built-ins

El comando help es especialmente útil porque:

Es más rápido que man para comandos built-in
Proporciona información específica de la versión actual del shell
Siempre está disponible sin requerir páginas de manual instaladas
Ofrece información concisa y práctica

### Ejemplo:

```bash
julian@julian-VirtualBox:~$ help type
type: type [-afptP] name [name ...]
    Display information about command type.
    
    For each NAME, indicate how it would be interpreted if used as a
    command name.
    
    Options:
      -a	display all locations containing an executable named NAME;
    		includes aliases, builtins, and functions, if and only if
    		the `-p' option is not also used
      -f	suppress shell function lookup
      -P	force a PATH search for each NAME, even if it is an alias,
    		builtin, or function, and returns the name of the disk file
    		that would be executed
      -p	returns either the name of the disk file that would be executed,
    		or nothing if `type -t NAME' would not return `file'
      -t	output a single word which is one of `alias', `keyword',
    		`function', `builtin', `file' or `', if NAME is an alias,
    		shell reserved word, shell function, shell builtin, disk file,
    		or not found, respectively
    
    Arguments:
      NAME	Command name to be interpreted.
    
    Exit Status:
    Returns success if all of the NAMEs are found; fails if any are not found.
```

## Puede visualizar tambien con --help

```bash
julian@julian-VirtualBox:~$ ls --help
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                             e.g., '--block-size=M'; see SIZE format below

  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                             change of file status information);
                             with -l: show ctime and sort by name;
                             otherwise: sort by ctime, newest first

  -C                         list entries by columns
      --color[=WHEN]         color the output WHEN; more info below
  -d, --directory            list directories themselves, not their contents
  -D, --dired                generate output designed for Emacs' dired mode
  -f                         list all entries in directory order
  -F, --classify[=WHEN]      append indicator (one of */=>@|) to entries WHEN
      --file-type            likewise, except do not append '*'
      --format=WORD          across -x, commas -m, horizontal -x, long -l,
                             single-column -1, verbose -l, vertical -C

      --full-time            like -l --time-style=full-iso
  -g                         like -l, but do not list owner
      --group-directories-first
                             group directories before files;
                             can be augmented with a --sort option, but any
                             use of --sort=none (-U) disables grouping

  -G, --no-group             in a long listing, don't print group names
  -h, --human-readable       with -l and -s, print sizes like 1K 234M 2G etc.
      --si                   likewise, but use powers of 1000 not 1024
  -H, --dereference-command-line
                             follow symbolic links listed on the command line
      --dereference-command-line-symlink-to-dir
                             follow each command line symbolic link
                             that points to a directory

      --hide=PATTERN         do not list implied entries matching shell PATTERN
                             (overridden by -a or -A)

      --hyperlink[=WHEN]     hyperlink file names WHEN
      --indicator-style=WORD
                             append indicator with style WORD to entry names:
                             none (default), slash (-p),
                             file-type (--file-type), classify (-F)

  -i, --inode                print the index number of each file
  -I, --ignore=PATTERN       do not list implied entries matching shell PATTERN
  -k, --kibibytes            default to 1024-byte blocks for file system usage;
                             used only with -s and per directory totals

  -l                         use a long listing format
  -L, --dereference          when showing file information for a symbolic
                             link, show information for the file the link
                             references rather than for the link itself

  -m                         fill width with a comma separated list of entries
  -n, --numeric-uid-gid      like -l, but list numeric user and group IDs
  -N, --literal              print entry names without quoting
  -o                         like -l, but do not list group information
  -p, --indicator-style=slash
                             append / indicator to directories
  -q, --hide-control-chars   print ? instead of nongraphic characters
      --show-control-chars   show nongraphic characters as-is (the default,
                             unless program is 'ls' and output is a terminal)

  -Q, --quote-name           enclose entry names in double quotes
      --quoting-style=WORD   use quoting style WORD for entry names:
                             literal, locale, shell, shell-always,
                             shell-escape, shell-escape-always, c, escape
                             (overrides QUOTING_STYLE environment variable)

  -r, --reverse              reverse order while sorting
  -R, --recursive            list subdirectories recursively
  -s, --size                 print the allocated size of each file, in blocks
  -S                         sort by file size, largest first
      --sort=WORD            sort by WORD instead of name: none (-U), size (-S),
                             time (-t), version (-v), extension (-X), width

      --time=WORD            select which timestamp used to display or sort;
                               access time (-u): atime, access, use;
                               metadata change time (-c): ctime, status;
                               modified time (default): mtime, modification;
                               birth time: birth, creation;
                             with -l, WORD determines which time to show;
                             with --sort=time, sort by WORD (newest first)

      --time-style=TIME_STYLE
                             time/date format with -l; see TIME_STYLE below
  -t                         sort by time, newest first; see --time
  -T, --tabsize=COLS         assume tab stops at each COLS instead of 8
  -u                         with -lt: sort by, and show, access time;
                             with -l: show access time and sort by name;
                             otherwise: sort by access time, newest first

  -U                         do not sort; list entries in directory order
  -v                         natural sort of (version) numbers within text
  -w, --width=COLS           set output width to COLS.  0 means no limit
  -x                         list entries by lines instead of by columns
  -X                         sort alphabetically by entry extension
  -Z, --context              print any security context of each file
      --zero                 end each output line with NUL, not newline
  -1                         list one file per line
      --help        display this help and exit
      --version     output version information and exit

The SIZE argument is an integer and optional unit (example: 10K is 10*1024).
Units are K,M,G,T,P,E,Z,Y,R,Q (powers of 1024) or KB,MB,... (powers of 1000).
Binary prefixes can be used, too: KiB=K, MiB=M, and so on.

The TIME_STYLE argument can be full-iso, long-iso, iso, locale, or +FORMAT.
FORMAT is interpreted like in date(1).  If FORMAT is FORMAT1<newline>FORMAT2,
then FORMAT1 applies to non-recent files and FORMAT2 to recent files.
TIME_STYLE prefixed with 'posix-' takes effect only outside the POSIX locale.
Also the TIME_STYLE environment variable sets the default style to use.

The WHEN argument defaults to 'always' and can also be 'auto' or 'never'.

Using color to distinguish file types is disabled both by default and
with --color=never.  With --color=auto, ls emits color codes only when
standard output is connected to a terminal.  The LS_COLORS environment
variable can change the settings.  Use the dircolors(1) command to set it.

Exit status:
 0  if OK,
 1  if minor problems (e.g., cannot access subdirectory),
 2  if serious trouble (e.g., cannot access command-line argument).

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/ls>
or available locally via: info '(coreutils) ls invocation'
```

## Man

Para desplazarte adelante y atras usas la tecla E y para salir presionas la tecla q.

📖 Traducción completa: 

"Estos comandos acceden a las páginas de manual e información sobre comandos del sistema y utilidades instaladas. Cuando están disponibles, ***las páginas de info generalmente contienen descripciones más detalladas que las páginas de man.***"

📋 Información expandida:

Ejemplos prácticos de uso de man e info
Tabla comparativa entre ambos sistemas
Secciones del manual con explicación de cada una
Comandos relacionados como whatis y apropos

Puntos clave añadidos:

man es universal en sistemas UNIX/Linux
info es principalmente de GNU y más detallado
Las páginas info son hipertextuales e interactivas
Las páginas man están organizadas en 8 secciones numeradas

## Whatis
📖 Traducción completa: 

"El comando whatis busca 'comando' en la base de datos whatis. Esto es útil para identificar comandos del sistema y archivos de configuración importantes. Considéralo como una versión simplificada del comando man."

```bash
$ whatis whatis
whatis (1) - search the whatis database for complete words
```

### Apropos

💡 Información ampliada:

Ejemplo real mostrando la salida exacta: whatis (1) - search the whatis database for complete words
Múltiples ejemplos prácticos con ls, passwd, cp
Opciones adicionales como expresiones regulares y secciones específicas
Tabla comparativa mostrando diferencias con man, help, y --help

🎯 Puntos clave destacados:

Es una versión simplificada de man
Útil para identificar rápidamente qué hace un comando
Muestra descripciones de una línea
Puede mostrar múltiples secciones del manual
Equivalente a man -f comando

📖 Definición: 

El comando apropos busca palabras clave en las descripciones de las páginas de manual. Es extremadamente útil cuando conoces qué quieres hacer pero no sabes el nombre exacto del comando. Esencialmente, realiza una búsqueda de texto en la base de datos whatis.

🎯 Características principales:

Búsqueda por concepto: Encuentra comandos por funcionalidad, no por nombre
Múltiples resultados: Muestra todos los comandos relacionados con el término
Exploración: Perfecto para descubrir herramientas que no conocías
Base de datos completa: Busca en todas las páginas de manual del sistema

💡 Casos de uso típicos:

Cuando sabes QUÉ quieres hacer pero no sabes CÓMO se llama el comando
Para explorar herramientas disponibles en una categoría específica
Para encontrar alternativas a comandos conocidos
Para aprender sobre nuevas funcionalidades del sistema

🔍 Ejemplos prácticos que muestran cómo encontrar:

Comandos para copiar archivos
Herramientas de red
Utilidades de compresión
Comandos de listado de directorios

⚡ Equivalencia: apropos palabra = man -k palabra (ambos hacen lo mismo)