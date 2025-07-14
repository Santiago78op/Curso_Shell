# COMANDOS LINUX SHELL - GUÍA COMPLETA

## ¿Qué son los Comandos?

### Definición

Un **comando** es una instrucción que le das al shell para que ejecute una tarea específica. Los comandos pueden ser:

- **Programas ejecutables** almacenados en el sistema de archivos
- **Comandos built-in** (integrados) del shell
- **Funciones** definidas por el usuario
- **Aliases** (atajos) personalizados

### Anatomía de un Comando

```
comando [parametros] [argumentos]
├─ programa a ejecutar
├─ modificadores del comportamiento  
└─ datos sobre los que operar

Ejemplo: ls -la /home/usuario
         │  │   └─ argumento (directorio)
         │  └─ parametros (-l = lista larga, -a = mostrar ocultos)
         └─ comando base
```

## Tipos de Comandos

### 1. Comandos Built-in (Integrados)

**Definición**: Comandos que forman parte del shell mismo, no son programas externos.

**Características**:
- Se ejecutan directamente por el shell
- Más rápidos (no requieren cargar programa externo)
- Pueden acceder y modificar el entorno del shell
- Varían entre diferentes shells

**Ejemplos comunes**:
```bash
cd          # Cambiar directorio
pwd         # Mostrar directorio actual
echo        # Mostrar texto
export      # Definir variables de entorno
alias       # Crear atajos
history     # Mostrar historial de comandos
jobs        # Listar trabajos en background
kill        # Terminar procesos
source      # Ejecutar script en el shell actual
type        # Mostrar tipo de comando
```

### 2. Comandos Externos (Programas)

**Definición**: Programas ejecutables almacenados en el sistema de archivos.

**Características**:
- Archivos binarios en directorios como `/bin`, `/usr/bin`, `/usr/local/bin`
- Se ejecutan como procesos separados
- Universales entre diferentes shells
- Pueden ser instalados/desinstalados

**Ejemplos comunes**:
```bash
ls          # Listar archivos (/bin/ls)
cp          # Copiar archivos (/bin/cp)
mv          # Mover archivos (/bin/mv)
grep        # Buscar texto (/bin/grep)
find        # Buscar archivos (/usr/bin/find)
vim         # Editor de texto (/usr/bin/vim)
```

### 3. Funciones

**Definición**: Comandos personalizados definidos por el usuario.

```bash
# Definir función
mifuncion() {
    echo "Hola $1"
    ls -la
}

# Usar función
mifuncion mundo
```

### 4. Aliases

**Definición**: Atajos o nombres alternativos para comandos.

```bash
# Definir alias
alias ll='ls -la'
alias la='ls -A'
alias ..='cd ..'

# Usar alias
ll          # equivale a 'ls -la'
```

## Comando `type` - Identificando Comandos

### ¿Qué hace `type`?

El comando `type` te dice **qué tipo de comando** es algo y **dónde se encuentra**.

### Sintaxis y Ejemplos

```bash
type comando [comando...]

# Ejemplos prácticos:

# Comando built-in
type cd
# cd is a shell builtin

# Comando externo
type ls
# ls is /bin/ls

# Alias
type ll
# ll is aliased to `ls -la'

# Función
type mifuncion
# mifuncion is a function

# Múltiples comandos
type cd ls echo grep
# cd is a shell builtin
# ls is /bin/ls  
# echo is a shell builtin
# grep is /bin/grep
```

### Opciones de `type`

```bash
# Solo mostrar el tipo
type -t cd
# builtin

type -t ls  
# file

# Mostrar toda la información
type -a echo
# echo is a shell builtin
# echo is /bin/echo

# Modo silencioso (solo código de salida)
type -q comando && echo "existe" || echo "no existe"
```

## ¿Cambian los Comandos entre Shells?

### Comandos Built-in: SÍ Cambian

**Bash Built-ins**:
```bash
# Comandos específicos de Bash
history         # Historial de comandos
dirs           # Pila de directorios  
pushd/popd     # Navegación con pila
complete       # Autocompletado
shopt          # Opciones de shell
```

**Zsh Built-ins**:
```bash
# Comandos específicos de Zsh
autoload       # Cargar funciones automáticamente
vared          # Editor de variables
zmv            # Renombrado avanzado de archivos
```

**Fish Built-ins**:
```bash
# Comandos específicos de Fish
fish_config    # Configuración web
funced         # Editor de funciones
```

### Comandos Externos: NO Cambian

Los programas externos como `ls`, `cp`, `mv`, `grep` son los **mismos en todos los shells** porque son programas independientes del shell.

### Diferencias Importantes

**1. Sintaxis de Arrays**
```bash
# Bash
array=(uno dos tres)
echo ${array[1]}

# Zsh (similar a Bash)
array=(uno dos tres)  
echo $array[2]        # Zsh indexa desde 1

# Fish (completamente diferente)
set array uno dos tres
echo $array[2]
```

**2. Sintaxis de Funciones**
```bash
# Bash/Zsh
function mifunc() {
    echo $1
}

# Fish
function mifunc
    echo $argv[1]
end
```

**3. Variables de Entorno**
```bash
# Bash/Zsh
export VAR=valor

# Fish
set -gx VAR valor
```

## Comandos Más Utilizados

### 1. Navegación y Listado

#### `ls` - Listar Archivos
```bash
ls                    # Listado básico
ls -l                 # Formato largo (permisos, tamaño, fecha)
ls -la                # Incluir archivos ocultos
ls -lh                # Tamaños legibles (KB, MB, GB)
ls -lt                # Ordenar por fecha de modificación
ls -lS                # Ordenar por tamaño
ls -R                 # Recursivo (subdirectorios)
ls --color=auto       # Con colores
ls -1                 # Un archivo por línea
```

#### `cd` - Cambiar Directorio
```bash
cd /ruta/absoluta     # Ir a ruta específica
cd ruta/relativa      # Relativa al directorio actual
cd                    # Ir al directorio home
cd ~                  # Ir al directorio home
cd ..                 # Directorio padre
cd -                  # Directorio anterior
cd ../..              # Dos niveles arriba
```

#### `pwd` - Mostrar Directorio Actual
```bash
pwd                   # Ruta completa del directorio actual
pwd -P                # Ruta física (resuelve links simbólicos)
```

### 2. Manipulación de Archivos

#### `cp` - Copiar Archivos
```bash
cp archivo destino               # Copiar archivo
cp archivo1 archivo2 destino/    # Copiar múltiples archivos
cp -r directorio/ destino/       # Copiar directorio recursivamente
cp -i archivo destino            # Preguntar antes de sobrescribir
cp -u archivo destino            # Solo si es más nuevo
cp -p archivo destino            # Preservar permisos y timestamps
cp -v archivo destino            # Verbose (mostrar lo que hace)
cp -a directorio/ destino/       # Preservar todo (archive mode)
```

#### `mv` - Mover/Renombrar
```bash
mv archivo destino               # Mover o renombrar archivo
mv archivo1 archivo2 destino/    # Mover múltiples archivos
mv -i archivo destino            # Preguntar antes de sobrescribir
mv -u archivo destino            # Solo si es más nuevo
mv -v archivo destino            # Verbose
```

#### `rm` - Eliminar
```bash
rm archivo                       # Eliminar archivo
rm -i archivo                    # Preguntar confirmación
rm -f archivo                    # Forzar (sin preguntar)
rm -r directorio/                # Eliminar directorio recursivamente
rm -rf directorio/               # Forzar eliminación recursiva
rm *.txt                         # Eliminar todos los .txt
```

### 3. Creación y Visualización

#### `mkdir` - Crear Directorios
```bash
mkdir directorio                 # Crear directorio
mkdir -p ruta/completa/nueva     # Crear ruta completa
mkdir -m 755 directorio          # Con permisos específicos
mkdir dir1 dir2 dir3             # Múltiples directorios
```

#### `touch` - Crear Archivos/Actualizar Timestamps
```bash
touch archivo                    # Crear archivo vacío
touch archivo1 archivo2          # Múltiples archivos
touch -t 202401151430 archivo    # Timestamp específico
```

#### `cat` - Mostrar Contenido
```bash
cat archivo                      # Mostrar contenido completo
cat archivo1 archivo2            # Concatenar archivos
cat > archivo                    # Crear archivo con entrada estándar
cat >> archivo                   # Agregar al final del archivo
cat -n archivo                   # Con números de línea
```

### 4. Búsqueda y Filtrado

#### `grep` - Buscar Texto
```bash
grep "patrón" archivo            # Buscar patrón en archivo
grep -i "patrón" archivo         # Case insensitive
grep -r "patrón" directorio/     # Búsqueda recursiva
grep -n "patrón" archivo         # Mostrar números de línea
grep -v "patrón" archivo         # Invertir (mostrar NO coincidencias)
grep -c "patrón" archivo         # Contar coincidencias
grep -l "patrón" *.txt           # Solo nombres de archivos
```

#### `find` - Buscar Archivos
```bash
find . -name "*.txt"             # Buscar por nombre
find . -type f                   # Solo archivos
find . -type d                   # Solo directorios
find . -size +100M               # Archivos mayores a 100MB
find . -mtime -7                 # Modificados en últimos 7 días
find . -name "*.log" -delete     # Buscar y eliminar
```

### 5. Información del Sistema

#### `ps` - Procesos
```bash
ps                               # Procesos del usuario actual
ps aux                           # Todos los procesos
ps -ef                           # Formato extendido
ps aux | grep programa           # Buscar proceso específico
```

#### `top`/`htop` - Monitor de Procesos
```bash
top                              # Monitor en tiempo real
htop                             # Versión mejorada (si está instalada)
```

#### `df` - Espacio en Disco
```bash
df                               # Uso de discos
df -h                            # Formato legible
df -T                            # Mostrar tipo de sistema de archivos
```

#### `du` - Uso de Directorio
```bash
du directorio/                   # Uso del directorio
du -h directorio/                # Formato legible
du -s directorio/                # Solo resumen
du -sh *                         # Resumen de cada elemento
```

## Diferencias Importantes entre Comandos

### `type` vs `which` vs `whereis`

#### `type` (Built-in)
```bash
type comando
# Muestra: built-in, alias, función, o ubicación del ejecutable
# Información más completa sobre el comando
```

#### `which` (Comando externo)
```bash
which comando
# Solo muestra la ubicación del ejecutable en PATH
# No detecta built-ins, aliases, o funciones
```

#### `whereis` (Comando externo)
```bash
whereis comando
# Busca ejecutable, código fuente, y páginas de manual
# Información más amplia sobre archivos relacionados
```

**Ejemplo Comparativo**:
```bash
# Para 'cd' (built-in):
type cd        # cd is a shell builtin
which cd       # (sin salida - no está en PATH)
whereis cd     # cd: /usr/bin/cd /usr/share/man/man1/cd.1.gz

# Para 'ls' (comando externo):
type ls        # ls is /bin/ls
which ls       # /bin/ls
whereis ls     # ls: /bin/ls /usr/share/man/man1/ls.1.gz
```

### `cp` vs `mv` - Diferencias Clave

#### `cp` (Copiar)
```bash
# COPIA archivos (original permanece)
cp archivo destino
# Resultado: 'archivo' existe, 'destino' existe (copia)

# Opciones importantes:
cp -r directorio/ destino/       # Recursivo para directorios
cp -p archivo destino            # Preservar atributos
cp -u archivo destino            # Solo si es más nuevo
cp -i archivo destino            # Interactivo (preguntar)
```

#### `mv` (Mover/Renombrar)
```bash
# MUEVE archivos (original desaparece)
mv archivo destino
# Resultado: 'archivo' NO existe, 'destino' existe

# NO necesita -r para directorios (los mueve completos)
mv directorio/ nuevo_nombre/

# Opciones importantes:
mv -i archivo destino            # Interactivo (preguntar)
mv -u archivo destino            # Solo si es más nuevo
mv -v archivo destino            # Verbose
```

**Diferencias Clave**:

| Aspecto | `cp` | `mv` |
|---------|------|------|
| **Archivo original** | Se mantiene | Se elimina |
| **Uso de espacio** | Duplica espacio | No usa espacio extra |
| **Velocidad** | Más lento (copia datos) | Más rápido (solo cambia metadatos) |
| **Entre sistemas de archivos** | Siempre funciona | Puede requerir copia+eliminación |
| **Directorios** | Requiere `-r` | No requiere opciones especiales |

## Comandos por Categorías

### 📁 Gestión de Archivos y Directorios

```bash
# Navegación
cd, pwd, ls

# Creación
mkdir, touch, mktemp

# Copia y movimiento  
cp, mv, rsync

# Eliminación
rm, rmdir

# Enlaces
ln, readlink

# Permisos
chmod, chown, chgrp

# Atributos
stat, file
```

### 🔍 Búsqueda y Filtrado

```bash
# Búsqueda de archivos
find, locate, which, whereis

# Búsqueda en contenido
grep, egrep, fgrep, rg (ripgrep)

# Filtrado de texto
sort, uniq, cut, awk, sed

# Comparación
diff, comm, cmp
```

### 📄 Visualización y Edición

```bash
# Visualización
cat, less, more, head, tail

# Editores
nano, vim, emacs

# Información de archivos
wc, file, stat, du
```

### 🔧 Sistema y Procesos

```bash
# Procesos
ps, top, htop, jobs, kill, killall

# Sistema
df, du, free, uptime, uname

# Usuarios
who, w, id, su, sudo

# Red
ping, wget, curl, ssh, scp
```

### 🔗 Pipes y Redirección

```bash
# Pipes
comando1 | comando2

# Redirección
comando > archivo         # Sobrescribir
comando >> archivo        # Agregar
comando < archivo         # Entrada desde archivo
comando 2> archivo        # Errores a archivo
comando &> archivo        # Todo a archivo
```

## Trucos y Consejos

### 1. Combinaciones Útiles

```bash
# Buscar y eliminar archivos antiguos
find . -name "*.log" -mtime +30 -delete

# Copiar con progreso
rsync -av --progress origen/ destino/

# Ver archivos más grandes
du -sh * | sort -hr | head -10

# Procesos que más CPU consumen
ps aux | sort -k3 -nr | head -10
```

### 2. Atajos de Teclado Importantes

```bash
Ctrl+C          # Cancelar comando actual
Ctrl+Z          # Suspender proceso
Ctrl+D          # EOF / Salir
Ctrl+L          # Limpiar pantalla
Ctrl+R          # Búsqueda en historial
Ctrl+A          # Inicio de línea
Ctrl+E          # Final de línea
Tab             # Autocompletar
!!              # Último comando
!comando        # Último comando que empieza con "comando"
```

### 3. Variables y Expansión

```bash
# Variables importantes
$HOME           # Directorio home
$PATH           # Rutas de búsqueda de comandos
$USER           # Usuario actual
$PWD            # Directorio actual
$$              # PID del shell
$?              # Código de salida del último comando

# Expansión de llaves
echo archivo_{1..5}.txt         # archivo_1.txt archivo_2.txt ...
cp archivo.txt{,.bak}           # Copia archivo.txt a archivo.txt.bak

# Expansión de wildcards
*.txt           # Todos los archivos .txt
?.txt           # Un solo carácter + .txt
[abc].txt       # a.txt, b.txt, o c.txt
```

## Mejores Prácticas

### 1. Seguridad

```bash
# Usar opciones interactivas para operaciones peligrosas
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Verificar comandos antes de ejecutar
type comando                    # Verificar qué comando se ejecutará
which comando                   # Encontrar ubicación del ejecutable
```

### 2. Eficiencia

```bash
# Usar autocompletado
Tab                             # Completar comandos y rutas

# Crear aliases para comandos frecuentes
alias ll='ls -la'
alias ..='cd ..'
alias grep='grep --color=auto'

# Usar historial eficientemente
Ctrl+R                          # Búsqueda en historial
!!                              # Repetir último comando
!n                              # Ejecutar comando número n del historial
```

### 3. Debugging

```bash
# Verificar sintaxis de comandos
bash -n script.sh               # Verificar sintaxis sin ejecutar

# Modo verbose para debugging
set -x                          # Mostrar comandos ejecutados
comando -v                      # Modo verbose (si disponible)

# Verificar códigos de salida
echo $?                         # Código de salida del último comando
```

Los comandos son la base fundamental de Linux. Entender la diferencia entre built-ins y comandos externos, saber cómo identificarlos con `type`, y dominar los comandos más utilizados te dará una base sólida para trabajar eficientemente en cualquier sistema Linux, independientemente del shell que uses.