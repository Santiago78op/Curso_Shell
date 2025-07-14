# SHELL Y PROMPT EN LINUX - GUÍA COMPLETA

## ¿Qué es el Shell?

### Definición y Función

El **shell** es un programa que actúa como **interfaz entre el usuario y el kernel** del sistema operativo. Es el intérprete de comandos que:

- **Interpreta y ejecuta comandos** del usuario
- **Proporciona un entorno de trabajo** interactivo
- **Gestiona la entrada y salida** de programas
- **Facilita la automatización** mediante scripts
- **Maneja variables de entorno** y configuraciones

### Arquitectura del Shell

```
┌─────────────────────────────────────────┐
│                USUARIO                  │
└─────────────────┬───────────────────────┘
                  │ Comandos de texto
┌─────────────────▼───────────────────────┐
│                SHELL                    │ ← Intérprete de comandos
│         (bash, zsh, fish, etc.)         │
└─────────────────┬───────────────────────┘
                  │ System calls
┌─────────────────▼───────────────────────┐
│               KERNEL                    │ ← Núcleo del sistema
└─────────────────┬───────────────────────┘
                  │ Hardware access
┌─────────────────▼───────────────────────┐
│              HARDWARE                   │
└─────────────────────────────────────────┘
```

## Historia de los Shells

### Shell Bourne (sh) - 1977

**Desarrollado por Stephen Bourne** en Bell Labs
- **Primer shell estándar** de UNIX
- **Scripting potente** con estructuras de control
- **Variables y funciones** básicas
- **Base de shells modernos**

**Características**
- Control de flujo: if, while, for
- Variables de entorno
- Redirección de entrada/salida
- Pipes para conectar comandos

### C Shell (csh) - 1978

**Desarrollado por Bill Joy** en Berkeley
- **Sintaxis similar a C**
- **Historia de comandos**
- **Alias de comandos**
- **Control de trabajos**

**Mejoras**
- Historial con `!!` y `!n`
- Autocompletado básico
- Expresiones matemáticas
- Arrays y variables indexadas

### Korn Shell (ksh) - 1983

**Desarrollado por David Korn** en Bell Labs
- **Compatible con Bourne Shell**
- **Características de C Shell**
- **Edición de línea de comandos**
- **Funciones avanzadas**

**Innovaciones**
- Edición vi/emacs en línea de comandos
- Aritmética entera built-in
- Arrays asociativos
- Coprocessos

## Bash - Bourne Again Shell

### Historia y Desarrollo

**Desarrollado por Brian Fox** (1989) para el proyecto GNU
- **Sustituto libre** del Bourne Shell
- **Combina características** de sh, csh, y ksh
- **Shell por defecto** en la mayoría de distribuciones Linux
- **Continúa en desarrollo activo**

### Características Principales

**Compatibilidad**
- **Totalmente compatible** con Bourne Shell (sh)
- **Ejecuta scripts** de sh sin modificación
- **Estándar POSIX** compliance
- **Portable** entre sistemas UNIX-like

**Funcionalidades Avanzadas**
- **Autocompletado** inteligente (Tab completion)
- **Historia de comandos** persistente
- **Edición de línea** (vi/emacs modes)
- **Expansión de llaves** `{a,b,c}`
- **Expansión de parámetros** avanzada
- **Arrays** indexados y asociativos

### Configuración de Bash

**Archivos de Configuración**

| Archivo | Scope | Cuándo se ejecuta | Propósito |
|---------|-------|-------------------|-----------|
| `/etc/profile` | Sistema | Login shell | Configuración global |
| `~/.bash_profile` | Usuario | Login shell | Configuración personal de login |
| `~/.bashrc` | Usuario | Interactive shell | Configuración interactiva |
| `~/.bash_logout` | Usuario | Logout | Cleanup al salir |

**Ejemplo de ~/.bashrc**
```bash
# Historial
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTCONTROL=ignoredups:erasedups

# Aliases útiles
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias grep='grep --color=auto'
alias ..='cd ..'
alias ...='cd ../..'

# Variables de entorno
export EDITOR=nano
export PAGER=less
export PATH="$HOME/bin:$PATH"

# Prompt personalizado
PS1='\u@\h:\w\$ '
```

## Shells Modernos

### Zsh (Z Shell)

**Desarrollado por Paul Falstad** (1990)
- **Altamente personalizable**
- **Autocompletado poderoso**
- **Temas y plugins**
- **Compatible con bash**

**Características Destacadas**
- **Corrección automática** de comandos
- **Glob patterns** avanzados
- **Sharing de historial** entre sesiones
- **Framework Oh My Zsh** popular

**Ejemplo de configuración**
```zsh
# ~/.zshrc
# Oh My Zsh
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="agnoster"
plugins=(git docker kubectl)
source $ZSH/oh-my-zsh.sh

# Configuración personalizada
setopt AUTO_CD              # cd automático
setopt CORRECT             # corrección de comandos
setopt HIST_VERIFY         # verificar expansión de historial
```

### Fish (Friendly Interactive Shell)

**Desarrollado por Axel Liljencrantz** (2005)
- **Sintaxis clara** y consistente
- **Autocompletado inteligente**
- **Syntax highlighting** en tiempo real
- **No POSIX compatible** (intencionalmente diferente)

**Filosofía**
- **"Funciona out of the box"**
- **Sin configuración compleja**
- **Experiencia de usuario moderna**
- **Retroalimentación visual**

**Características Únicas**
```fish
# Syntax highlighting en tiempo real
ls -la /home/user/Documents

# Autocompletado basado en historial
git ch[TAB] # sugiere "checkout" si se usó antes

# Funciones simples
function mkcd
    mkdir $argv && cd $argv
end
```

### Otras Shells Especializadas

**tcsh** - Enhanced C Shell
- Versión mejorada de csh
- Edición de línea de comandos
- Programable y personalizable

**dash** - Debian Almquist Shell
- Shell minimalista
- Rápido y ligero
- Usado para scripts del sistema

**xonsh** - Python-powered Shell
- Combina Python con shell
- Sintaxis mixta
- Ideal para programadores Python

## El Prompt - Interfaz de Usuario

### ¿Qué es el Prompt?

El **prompt** es la cadena de texto que el shell muestra para **indicar que está listo para recibir comandos** del usuario.

**Funciones del Prompt**
- **Indicar estado** del shell
- **Mostrar información contextual** (usuario, directorio, hora)
- **Proporcionar feedback visual**
- **Facilitar navegación** y orientación

### Anatomía del Prompt

```
┌── Usuario ── Host ─── Directorio ─── Indicador ──┐
│                                                  │
user@hostname:/current/directory$ comando
│    │        │                  │
│    │        │                  └─ Prompt symbol
│    │        └─ Current working directory
│    └─ Hostname
└─ Username
```

### Variable PS1 en Bash

**PS1** (Prompt String 1) controla el prompt principal

**Códigos de Escape Comunes**

| Código | Descripción | Ejemplo |
|--------|-------------|---------|
| `\u` | Nombre de usuario | `john` |
| `\h` | Hostname (corto) | `laptop` |
| `\H` | Hostname (completo) | `laptop.domain.com` |
| `\w` | Directorio actual (completo) | `/home/john/Documents` |
| `\W` | Directorio actual (basename) | `Documents` |
| `\d` | Fecha | `Mon Jan 15` |
| `\t` | Hora (24h) | `14:30:25` |
| `\T` | Hora (12h) | `02:30:25` |
| `\$` | # si root, $ si usuario normal | `$` |
| `\n` | Nueva línea | |
| `\\` | Backslash literal | `\` |

**Ejemplos de PS1**

```bash
# Prompt simple
PS1='\u@\h:\w\$ '
# Resultado: user@hostname:/current/dir$ 

# Prompt con colores
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
# Resultado: user@hostname:/current/dir$ (con colores)

# Prompt multi-línea
PS1='\[\033[01;33m\]\u@\h\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\]\n\$ '
# Resultado:
# user@hostname /current/dir
# $ 

# Prompt con hora
PS1='[\t] \u@\h:\w\$ '
# Resultado: [14:30:25] user@hostname:/current/dir$ 
```

### Colores en el Prompt

**Códigos de Color ANSI**

| Color | Código | Negrita |
|-------|--------|---------|
| Negro | `\033[30m` | `\033[01;30m` |
| Rojo | `\033[31m` | `\033[01;31m` |
| Verde | `\033[32m` | `\033[01;32m` |
| Amarillo | `\033[33m` | `\033[01;33m` |
| Azul | `\033[34m` | `\033[01;34m` |
| Magenta | `\033[35m` | `\033[01;35m` |
| Cian | `\033[36m` | `\033[01;36m` |
| Blanco | `\033[37m` | `\033[01;37m` |
| Reset | `\033[00m` | |

**Prompt Colorizado Avanzado**
```bash
# Prompt con información de Git
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
```

### Variables de Prompt Adicionales

**PS2** - Prompt de continuación
```bash
PS2='> '  # Aparece cuando el comando continúa en la siguiente línea
```

**PS3** - Prompt para comando `select`
```bash
PS3='Seleccione una opción: '
```

**PS4** - Prompt para modo debug
```bash
PS4='+ '  # Aparece cuando se ejecuta 'set -x'
```

## Funcionalidades Avanzadas del Shell

### Historia de Comandos

**Configuración del Historial**
```bash
# Tamaño del historial en memoria
HISTSIZE=10000

# Tamaño del archivo de historial
HISTFILESIZE=20000

# Control de duplicados
HISTCONTROL=ignoredups:erasedups

# Ignorar comandos específicos
HISTIGNORE="ls:ll:cd:pwd:clear:history"

# Agregar timestamp al historial
HISTTIMEFORMAT='%F %T '
```

**Comandos de Historial**

| Comando | Descripción |
|---------|-------------|
| `history` | Mostrar historial completo |
| `!!` | Ejecutar último comando |
| `!n` | Ejecutar comando número n |
| `!string` | Ejecutar último comando que empieza con string |
| `^old^new` | Reemplazar 'old' por 'new' en último comando |
| `Ctrl+R` | Búsqueda reversa en historial |

### Autocompletado (Tab Completion)

**Tipos de Autocompletado**
- **Comandos**: Nombres de programas en PATH
- **Archivos y directorios**: Basado en filesystem
- **Variables**: Variables de entorno y shell
- **Hostnames**: Para ssh, scp, etc.
- **Usuarios**: Para su, mail, etc.

**Configuración Avanzada**
```bash
# Habilitar autocompletado case-insensitive
bind 'set completion-ignore-case on'

# Mostrar múltiples opciones inmediatamente
bind 'set show-all-if-ambiguous on'

# Completado programable personalizado
complete -W "start stop restart status" service
```

### Aliases y Funciones

**Aliases Útiles**
```bash
# Navegación
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# Listado de archivos
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias lt='ls -ltr'  # Ordenado por tiempo

# Comandos con colores
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# Seguridad
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Utilidades
alias h='history'
alias j='jobs -l'
alias ports='netstat -tulanp'
```

**Funciones Avanzadas**
```bash
# Crear directorio y entrar en él
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extraer archivos comprimidos
extract() {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar e $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)     echo "'$1' no se puede extraer" ;;
        esac
    else
        echo "'$1' no es un archivo válido"
    fi
}

# Buscar y matar procesos
pk() {
    ps aux | grep $1 | grep -v grep | awk '{print $2}' | xargs kill -9
}
```

## Redirección y Pipes

### Redirección de Entrada/Salida

**Redirección Básica**
```bash
# Redirección de salida
comando > archivo          # Sobrescribir
comando >> archivo         # Agregar

# Redirección de entrada
comando < archivo

# Redirección de error estándar
comando 2> error.log       # Solo errores
comando &> archivo         # Salida y errores
comando > archivo 2>&1     # Salida y errores (compatible)
```

**Redirección Avanzada**
```bash
# Here documents
cat << EOF > archivo.txt
Este es el contenido
del archivo
EOF

# Here strings
grep "patrón" <<< "texto a buscar"

# Redirección a múltiples archivos
comando | tee archivo1.txt archivo2.txt
```

### Pipes y Filtros

**Filosofía UNIX**: "Do one thing and do it well"

```bash
# Cadena de pipes básica
ps aux | grep python | wc -l

# Análisis de logs
cat /var/log/apache/access.log | \
    grep "404" | \
    awk '{print $1}' | \
    sort | \
    uniq -c | \
    sort -nr | \
    head -10

# Procesamiento de texto
cat archivo.txt | \
    tr '[:upper:]' '[:lower:]' | \
    sed 's/old/new/g' | \
    sort | \
    uniq > resultado.txt
```

## Control de Trabajos

### Gestión de Procesos

**Comandos de Control**
```bash
# Ejecutar en background
comando &

# Suspender proceso actual
Ctrl+Z

# Listar trabajos
jobs

# Traer trabajo a foreground
fg %1

# Enviar trabajo a background
bg %1

# Terminar trabajo
kill %1
```

**Ejemplo Práctico**
```bash
# Iniciar editor en background
nano archivo.txt &

# Verificar trabajos
jobs
# [1]+  Running    nano archivo.txt &

# Traer a foreground cuando sea necesario
fg %1
```

### Signals y Control de Procesos

**Signals Comunes**

| Signal | Número | Descripción |
|--------|--------|-------------|
| SIGTERM | 15 | Terminación normal |
| SIGKILL | 9 | Terminación forzada |
| SIGSTOP | 19 | Suspender proceso |
| SIGCONT | 18 | Continuar proceso |
| SIGINT | 2 | Interrupción (Ctrl+C) |

```bash
# Terminar proceso por PID
kill 1234
kill -15 1234  # Equivalente

# Forzar terminación
kill -9 1234

# Terminar por nombre
killall firefox
pkill python
```

## Personalización Avanzada

### Frameworks de Shell

**Oh My Zsh** (para Zsh)
```bash
# Instalación
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Configuración ~/.zshrc
ZSH_THEME="agnoster"
plugins=(git docker kubectl auto-suggestions syntax-highlighting)
```

**Oh My Bash** (para Bash)
```bash
# Instalación
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

**Starship** (Cross-shell)
```bash
# Instalación
curl -sS https://starship.rs/install.sh | sh

# Agregar a ~/.bashrc o ~/.zshrc
eval "$(starship init bash)"  # para bash
eval "$(starship init zsh)"   # para zsh
```

### Prompt Inteligente

**Prompt con Información de Git**
```bash
# Función para mostrar branch de Git
git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

# Función para mostrar estado de Git
git_status() {
    if git rev-parse --git-dir > /dev/null 2>&1; then
        if [[ $(git status --porcelain) ]]; then
            echo "*"
        fi
    fi
}

# Prompt con información completa
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(git_branch)\[\033[01;33m\]$(git_status)\[\033[00m\]\$ '
```

**Prompt con Código de Salida**
```bash
# Mostrar código de salida del último comando
PS1='$(if [[ $? == 0 ]]; then echo "\[\033[01;32m\]✓"; else echo "\[\033[01;31m\]✗"; fi)\[\033[00m\] \u@\h:\w\$ '
```

### Variables de Entorno Importantes

**Variables del Sistema**
```bash
# Path de búsqueda de comandos
echo $PATH

# Directorio home del usuario
echo $HOME

# Usuario actual
echo $USER

# Editor por defecto
export EDITOR=nano

# Pager por defecto
export PAGER=less

# Idioma del sistema
export LANG=en_US.UTF-8
```

**Variables del Shell**
```bash
# Shell actual
echo $SHELL

# Opciones del shell
echo $SHELLOPTS

# PID del shell
echo $$

# Último directorio
echo $OLDPWD
```

## Scripting Básico

### Estructura de un Script

```bash
#!/bin/bash
# Shebang - especifica el intérprete

# Comentarios empiezan con #

# Variables
nombre="Juan"
edad=25

# Uso de variables
echo "Hola $nombre, tienes $edad años"
echo "En 10 años tendrás $((edad + 10)) años"

# Lectura de entrada
read -p "¿Cómo te llamas? " nombre_usuario
echo "Hola $nombre_usuario"
```

### Estructuras de Control

```bash
# Condicionales
if [ "$edad" -ge 18 ]; then
    echo "Eres mayor de edad"
elif [ "$edad" -ge 13 ]; then
    echo "Eres adolescente"
else
    echo "Eres niño"
fi

# Bucles
for i in {1..5}; do
    echo "Iteración $i"
done

# While
contador=1
while [ $contador -le 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done

# Case
case $1 in
    start)
        echo "Iniciando servicio..."
        ;;
    stop)
        echo "Deteniendo servicio..."
        ;;
    *)
        echo "Uso: $0 {start|stop}"
        ;;
esac
```

## Mejores Prácticas

### Seguridad

```bash
# Usar comillas para prevenir word splitting
nombre="Juan Pérez"
echo "$nombre"  # Correcto
echo $nombre    # Incorrecto

# Verificar existencia de archivos
if [ -f "$archivo" ]; then
    cat "$archivo"
fi

# Usar -n y -z para verificar strings
if [ -n "$variable" ]; then  # No vacía
    echo "Variable tiene contenido"
fi

if [ -z "$variable" ]; then  # Vacía
    echo "Variable está vacía"
fi
```

### Optimización

```bash
# Usar funciones para código repetitivo
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1"
}

# Usar arrays para múltiples valores
frutas=("manzana" "naranja" "plátano")
for fruta in "${frutas[@]}"; do
    echo "Me gusta la $fruta"
done

# Manejo de errores
set -e  # Salir si algún comando falla
set -u  # Error si variable no definida
set -o pipefail  # Error si falla algún comando en pipe
```

### Documentación

```bash
#!/bin/bash
#
# Nombre: backup.sh
# Descripción: Script para hacer backup de directorios
# Autor: Usuario
# Versión: 1.0
# Fecha: 2024-01-15
#
# Uso: ./backup.sh <directorio_origen> <directorio_destino>
#

# Verificar argumentos
if [ $# -ne 2 ]; then
    echo "Uso: $0 <origen> <destino>"
    exit 1
fi

# Variables
ORIGEN="$1"
DESTINO="$2"
FECHA=$(date +%Y%m%d_%H%M%S)

# Función principal
main() {
    echo "Iniciando backup..."
    tar -czf "${DESTINO}/backup_${FECHA}.tar.gz" "$ORIGEN"
    echo "Backup completado: backup_${FECHA}.tar.gz"
}

# Ejecutar función principal
main
```

## Troubleshooting y Debugging

### Técnicas de Debug

```bash
# Modo verbose
set -x  # Mostrar comandos ejecutados
set +x  # Desactivar modo verbose

# Debug de scripts
bash -x script.sh

# Verificar sintaxis sin ejecutar
bash -n script.sh

# Mostrar expansión de variables
set -v
```

### Problemas Comunes

**Permisos**
```bash
# Hacer script ejecutable
chmod +x script.sh

# Verificar permisos
ls -l script.sh
```

**PATH Issues**
```bash
# Verificar PATH
echo $PATH

# Encontrar ubicación de comando
which comando
type comando
```

**Variable Issues**
```bash
# Verificar si variable está definida
[ -n "$VARIABLE" ] && echo "Definida" || echo "No definida"

# Mostrar todas las variables
env
set
```

## Recursos y Herramientas

### Herramientas de Terminal

**Multiplexores**
- **tmux**: Terminal multiplexer moderno
- **screen**: Multiplexer tradicional
- **byobu**: Wrapper amigable para tmux/screen

**Mejoras de Terminal**
- **fzf**: Fuzzy finder
- **ripgrep**: Búsqueda de texto rápida
- **exa**: Reemplazo moderno de ls
- **bat**: cat con syntax highlighting

### Documentación

**Manuales**
```bash
man bash          # Manual de bash
info bash         # Info de GNU bash
help cd           # Ayuda built-in de bash
type comando      # Información sobre comando
```

**Recursos Online**
- **Advanced Bash-Scripting Guide**: Guía completa
- **ShellCheck**: Linter para shell scripts
- **Bash Reference Manual**: Documentación oficial
- **ExplainShell**: Explicación interactiva de comandos

El dominio del shell y el prompt es fundamental para la productividad en Linux. La personalización adecuada puede transformar la experiencia de línea de comandos de intimidante a poderosa y eficiente.

# SHELL Y PROMPT EN LINUX - GUÍA COMPLETA

## ¿Qué es el Shell?

### Definición y Función

El **shell** es un programa que actúa como **interfaz entre el usuario y el kernel** del sistema operativo. Es el intérprete de comandos que:

- **Interpreta y ejecuta comandos** del usuario
- **Proporciona un entorno de trabajo** interactivo
- **Gestiona la entrada y salida** de programas
- **Facilita la automatización** mediante scripts
- **Maneja variables de entorno** y configuraciones

### Arquitectura del Shell

```
┌─────────────────────────────────────────┐
│                USUARIO                  │
└─────────────────┬───────────────────────┘
                  │ Comandos de texto
┌─────────────────▼───────────────────────┐
│                SHELL                    │ ← Intérprete de comandos
│         (bash, zsh, fish, etc.)         │
└─────────────────┬───────────────────────┘
                  │ System calls
┌─────────────────▼───────────────────────┐
│               KERNEL                    │ ← Núcleo del sistema
└─────────────────┬───────────────────────┘
                  │ Hardware access
┌─────────────────▼───────────────────────┐
│              HARDWARE                   │
└─────────────────────────────────────────┘
```

## Historia de los Shells

### Shell Bourne (sh) - 1977

**Desarrollado por Stephen Bourne** en Bell Labs
- **Primer shell estándar** de UNIX
- **Scripting potente** con estructuras de control
- **Variables y funciones** básicas
- **Base de shells modernos**

**Características**
- Control de flujo: if, while, for
- Variables de entorno
- Redirección de entrada/salida
- Pipes para conectar comandos

### C Shell (csh) - 1978

**Desarrollado por Bill Joy** en Berkeley
- **Sintaxis similar a C**
- **Historia de comandos**
- **Alias de comandos**
- **Control de trabajos**

**Mejoras**
- Historial con `!!` y `!n`
- Autocompletado básico
- Expresiones matemáticas
- Arrays y variables indexadas

### Korn Shell (ksh) - 1983

**Desarrollado por David Korn** en Bell Labs
- **Compatible con Bourne Shell**
- **Características de C Shell**
- **Edición de línea de comandos**
- **Funciones avanzadas**

**Innovaciones**
- Edición vi/emacs en línea de comandos
- Aritmética entera built-in
- Arrays asociativos
- Coprocessos

## Bash - Bourne Again Shell

### Historia y Desarrollo

**Desarrollado por Brian Fox** (1989) para el proyecto GNU
- **Sustituto libre** del Bourne Shell
- **Combina características** de sh, csh, y ksh
- **Shell por defecto** en la mayoría de distribuciones Linux
- **Continúa en desarrollo activo**

### Características Principales

**Compatibilidad**
- **Totalmente compatible** con Bourne Shell (sh)
- **Ejecuta scripts** de sh sin modificación
- **Estándar POSIX** compliance
- **Portable** entre sistemas UNIX-like

**Funcionalidades Avanzadas**
- **Autocompletado** inteligente (Tab completion)
- **Historia de comandos** persistente
- **Edición de línea** (vi/emacs modes)
- **Expansión de llaves** `{a,b,c}`
- **Expansión de parámetros** avanzada
- **Arrays** indexados y asociativos

### Configuración de Bash

**Archivos de Configuración**

| Archivo | Scope | Cuándo se ejecuta | Propósito |
|---------|-------|-------------------|-----------|
| `/etc/profile` | Sistema | Login shell | Configuración global |
| `~/.bash_profile` | Usuario | Login shell | Configuración personal de login |
| `~/.bashrc` | Usuario | Interactive shell | Configuración interactiva |
| `~/.bash_logout` | Usuario | Logout | Cleanup al salir |

**Ejemplo de ~/.bashrc**
```bash
# Historial
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTCONTROL=ignoredups:erasedups

# Aliases útiles
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias grep='grep --color=auto'
alias ..='cd ..'
alias ...='cd ../..'

# Variables de entorno
export EDITOR=nano
export PAGER=less
export PATH="$HOME/bin:$PATH"

# Prompt personalizado
PS1='\u@\h:\w\$ '
```

## Shells Modernos

### Zsh (Z Shell)

**Desarrollado por Paul Falstad** (1990)
- **Altamente personalizable**
- **Autocompletado poderoso**
- **Temas y plugins**
- **Compatible con bash**

**Características Destacadas**
- **Corrección automática** de comandos
- **Glob patterns** avanzados
- **Sharing de historial** entre sesiones
- **Framework Oh My Zsh** popular

**Ejemplo de configuración**
```zsh
# ~/.zshrc
# Oh My Zsh
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="agnoster"
plugins=(git docker kubectl)
source $ZSH/oh-my-zsh.sh

# Configuración personalizada
setopt AUTO_CD              # cd automático
setopt CORRECT             # corrección de comandos
setopt HIST_VERIFY         # verificar expansión de historial
```

### Fish (Friendly Interactive Shell)

**Desarrollado por Axel Liljencrantz** (2005)
- **Sintaxis clara** y consistente
- **Autocompletado inteligente**
- **Syntax highlighting** en tiempo real
- **No POSIX compatible** (intencionalmente diferente)

**Filosofía**
- **"Funciona out of the box"**
- **Sin configuración compleja**
- **Experiencia de usuario moderna**
- **Retroalimentación visual**

**Características Únicas**
```fish
# Syntax highlighting en tiempo real
ls -la /home/user/Documents

# Autocompletado basado en historial
git ch[TAB] # sugiere "checkout" si se usó antes

# Funciones simples
function mkcd
    mkdir $argv && cd $argv
end
```

### Otras Shells Especializadas

**tcsh** - Enhanced C Shell
- Versión mejorada de csh
- Edición de línea de comandos
- Programable y personalizable

**dash** - Debian Almquist Shell
- Shell minimalista
- Rápido y ligero
- Usado para scripts del sistema

**xonsh** - Python-powered Shell
- Combina Python con shell
- Sintaxis mixta
- Ideal para programadores Python

## El Prompt - Interfaz de Usuario

### ¿Qué es el Prompt?

El **prompt** es la cadena de texto que el shell muestra para **indicar que está listo para recibir comandos** del usuario.

**Funciones del Prompt**
- **Indicar estado** del shell
- **Mostrar información contextual** (usuario, directorio, hora)
- **Proporcionar feedback visual**
- **Facilitar navegación** y orientación

### Anatomía del Prompt

```
┌── Usuario ── Host ─── Directorio ─── Indicador ──┐
│                                                  │
user@hostname:/current/directory$ comando
│    │        │                  │
│    │        │                  └─ Prompt symbol
│    │        └─ Current working directory
│    └─ Hostname
└─ Username
```

### Variable PS1 en Bash

**PS1** (Prompt String 1) controla el prompt principal

**Códigos de Escape Comunes**

| Código | Descripción | Ejemplo |
|--------|-------------|---------|
| `\u` | Nombre de usuario | `john` |
| `\h` | Hostname (corto) | `laptop` |
| `\H` | Hostname (completo) | `laptop.domain.com` |
| `\w` | Directorio actual (completo) | `/home/john/Documents` |
| `\W` | Directorio actual (basename) | `Documents` |
| `\d` | Fecha | `Mon Jan 15` |
| `\t` | Hora (24h) | `14:30:25` |
| `\T` | Hora (12h) | `02:30:25` |
| `\$` | # si root, $ si usuario normal | `$` |
| `\n` | Nueva línea | |
| `\\` | Backslash literal | `\` |

**Ejemplos de PS1**

```bash
# Prompt simple
PS1='\u@\h:\w\$ '
# Resultado: user@hostname:/current/dir$ 

# Prompt con colores
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
# Resultado: user@hostname:/current/dir$ (con colores)

# Prompt multi-línea
PS1='\[\033[01;33m\]\u@\h\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\]\n\$ '
# Resultado:
# user@hostname /current/dir
# $ 

# Prompt con hora
PS1='[\t] \u@\h:\w\$ '
# Resultado: [14:30:25] user@hostname:/current/dir$ 
```

### Colores en el Prompt

**Códigos de Color ANSI**

| Color | Código | Negrita |
|-------|--------|---------|
| Negro | `\033[30m` | `\033[01;30m` |
| Rojo | `\033[31m` | `\033[01;31m` |
| Verde | `\033[32m` | `\033[01;32m` |
| Amarillo | `\033[33m` | `\033[01;33m` |
| Azul | `\033[34m` | `\033[01;34m` |
| Magenta | `\033[35m` | `\033[01;35m` |
| Cian | `\033[36m` | `\033[01;36m` |
| Blanco | `\033[37m` | `\033[01;37m` |
| Reset | `\033[00m` | |

**Prompt Colorizado Avanzado**
```bash
# Prompt con información de Git
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
```

### Variables de Prompt Adicionales

**PS2** - Prompt de continuación
```bash
PS2='> '  # Aparece cuando el comando continúa en la siguiente línea
```

**PS3** - Prompt para comando `select`
```bash
PS3='Seleccione una opción: '
```

**PS4** - Prompt para modo debug
```bash
PS4='+ '  # Aparece cuando se ejecuta 'set -x'
```

## Funcionalidades Avanzadas del Shell

### Historia de Comandos

**Configuración del Historial**
```bash
# Tamaño del historial en memoria
HISTSIZE=10000

# Tamaño del archivo de historial
HISTFILESIZE=20000

# Control de duplicados
HISTCONTROL=ignoredups:erasedups

# Ignorar comandos específicos
HISTIGNORE="ls:ll:cd:pwd:clear:history"

# Agregar timestamp al historial
HISTTIMEFORMAT='%F %T '
```

**Comandos de Historial**

| Comando | Descripción |
|---------|-------------|
| `history` | Mostrar historial completo |
| `!!` | Ejecutar último comando |
| `!n` | Ejecutar comando número n |
| `!string` | Ejecutar último comando que empieza con string |
| `^old^new` | Reemplazar 'old' por 'new' en último comando |
| `Ctrl+R` | Búsqueda reversa en historial |

### Autocompletado (Tab Completion)

**Tipos de Autocompletado**
- **Comandos**: Nombres de programas en PATH
- **Archivos y directorios**: Basado en filesystem
- **Variables**: Variables de entorno y shell
- **Hostnames**: Para ssh, scp, etc.
- **Usuarios**: Para su, mail, etc.

**Configuración Avanzada**
```bash
# Habilitar autocompletado case-insensitive
bind 'set completion-ignore-case on'

# Mostrar múltiples opciones inmediatamente
bind 'set show-all-if-ambiguous on'

# Completado programable personalizado
complete -W "start stop restart status" service
```

### Aliases y Funciones

**Aliases Útiles**
```bash
# Navegación
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# Listado de archivos
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias lt='ls -ltr'  # Ordenado por tiempo

# Comandos con colores
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# Seguridad
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Utilidades
alias h='history'
alias j='jobs -l'
alias ports='netstat -tulanp'
```

**Funciones Avanzadas**
```bash
# Crear directorio y entrar en él
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extraer archivos comprimidos
extract() {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar e $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)     echo "'$1' no se puede extraer" ;;
        esac
    else
        echo "'$1' no es un archivo válido"
    fi
}

# Buscar y matar procesos
pk() {
    ps aux | grep $1 | grep -v grep | awk '{print $2}' | xargs kill -9
}
```

## Redirección y Pipes

### Redirección de Entrada/Salida

**Redirección Básica**
```bash
# Redirección de salida
comando > archivo          # Sobrescribir
comando >> archivo         # Agregar

# Redirección de entrada
comando < archivo

# Redirección de error estándar
comando 2> error.log       # Solo errores
comando &> archivo         # Salida y errores
comando > archivo 2>&1     # Salida y errores (compatible)
```

**Redirección Avanzada**
```bash
# Here documents
cat << EOF > archivo.txt
Este es el contenido
del archivo
EOF

# Here strings
grep "patrón" <<< "texto a buscar"

# Redirección a múltiples archivos
comando | tee archivo1.txt archivo2.txt
```

### Pipes y Filtros

**Filosofía UNIX**: "Do one thing and do it well"

```bash
# Cadena de pipes básica
ps aux | grep python | wc -l

# Análisis de logs
cat /var/log/apache/access.log | \
    grep "404" | \
    awk '{print $1}' | \
    sort | \
    uniq -c | \
    sort -nr | \
    head -10

# Procesamiento de texto
cat archivo.txt | \
    tr '[:upper:]' '[:lower:]' | \
    sed 's/old/new/g' | \
    sort | \
    uniq > resultado.txt
```

## Control de Trabajos

### Gestión de Procesos

**Comandos de Control**
```bash
# Ejecutar en background
comando &

# Suspender proceso actual
Ctrl+Z

# Listar trabajos
jobs

# Traer trabajo a foreground
fg %1

# Enviar trabajo a background
bg %1

# Terminar trabajo
kill %1
```

**Ejemplo Práctico**
```bash
# Iniciar editor en background
nano archivo.txt &

# Verificar trabajos
jobs
# [1]+  Running    nano archivo.txt &

# Traer a foreground cuando sea necesario
fg %1
```

### Signals y Control de Procesos

**Signals Comunes**

| Signal | Número | Descripción |
|--------|--------|-------------|
| SIGTERM | 15 | Terminación normal |
| SIGKILL | 9 | Terminación forzada |
| SIGSTOP | 19 | Suspender proceso |
| SIGCONT | 18 | Continuar proceso |
| SIGINT | 2 | Interrupción (Ctrl+C) |

```bash
# Terminar proceso por PID
kill 1234
kill -15 1234  # Equivalente

# Forzar terminación
kill -9 1234

# Terminar por nombre
killall firefox
pkill python
```

## Personalización Avanzada

### Frameworks de Shell

**Oh My Zsh** (para Zsh)
```bash
# Instalación
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Configuración ~/.zshrc
ZSH_THEME="agnoster"
plugins=(git docker kubectl auto-suggestions syntax-highlighting)
```

**Oh My Bash** (para Bash)
```bash
# Instalación
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

**Starship** (Cross-shell)
```bash
# Instalación
curl -sS https://starship.rs/install.sh | sh

# Agregar a ~/.bashrc o ~/.zshrc
eval "$(starship init bash)"  # para bash
eval "$(starship init zsh)"   # para zsh
```

### Prompt Inteligente

**Prompt con Información de Git**
```bash
# Función para mostrar branch de Git
git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

# Función para mostrar estado de Git
git_status() {
    if git rev-parse --git-dir > /dev/null 2>&1; then
        if [[ $(git status --porcelain) ]]; then
            echo "*"
        fi
    fi
}

# Prompt con información completa
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(git_branch)\[\033[01;33m\]$(git_status)\[\033[00m\]\$ '
```

**Prompt con Código de Salida**
```bash
# Mostrar código de salida del último comando
PS1='$(if [[ $? == 0 ]]; then echo "\[\033[01;32m\]✓"; else echo "\[\033[01;31m\]✗"; fi)\[\033[00m\] \u@\h:\w\$ '
```

### Variables de Entorno Importantes

**Variables del Sistema**
```bash
# Path de búsqueda de comandos
echo $PATH

# Directorio home del usuario
echo $HOME

# Usuario actual
echo $USER

# Editor por defecto
export EDITOR=nano

# Pager por defecto
export PAGER=less

# Idioma del sistema
export LANG=en_US.UTF-8
```

**Variables del Shell**
```bash
# Shell actual
echo $SHELL

# Opciones del shell
echo $SHELLOPTS

# PID del shell
echo $$

# Último directorio
echo $OLDPWD
```

## Scripting Básico

### Estructura de un Script

```bash
#!/bin/bash
# Shebang - especifica el intérprete

# Comentarios empiezan con #

# Variables
nombre="Juan"
edad=25

# Uso de variables
echo "Hola $nombre, tienes $edad años"
echo "En 10 años tendrás $((edad + 10)) años"

# Lectura de entrada
read -p "¿Cómo te llamas? " nombre_usuario
echo "Hola $nombre_usuario"
```

### Estructuras de Control

```bash
# Condicionales
if [ "$edad" -ge 18 ]; then
    echo "Eres mayor de edad"
elif [ "$edad" -ge 13 ]; then
    echo "Eres adolescente"
else
    echo "Eres niño"
fi

# Bucles
for i in {1..5}; do
    echo "Iteración $i"
done

# While
contador=1
while [ $contador -le 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done

# Case
case $1 in
    start)
        echo "Iniciando servicio..."
        ;;
    stop)
        echo "Deteniendo servicio..."
        ;;
    *)
        echo "Uso: $0 {start|stop}"
        ;;
esac
```

## Mejores Prácticas

### Seguridad

```bash
# Usar comillas para prevenir word splitting
nombre="Juan Pérez"
echo "$nombre"  # Correcto
echo $nombre    # Incorrecto

# Verificar existencia de archivos
if [ -f "$archivo" ]; then
    cat "$archivo"
fi

# Usar -n y -z para verificar strings
if [ -n "$variable" ]; then  # No vacía
    echo "Variable tiene contenido"
fi

if [ -z "$variable" ]; then  # Vacía
    echo "Variable está vacía"
fi
```

### Optimización

```bash
# Usar funciones para código repetitivo
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1"
}

# Usar arrays para múltiples valores
frutas=("manzana" "naranja" "plátano")
for fruta in "${frutas[@]}"; do
    echo "Me gusta la $fruta"
done

# Manejo de errores
set -e  # Salir si algún comando falla
set -u  # Error si variable no definida
set -o pipefail  # Error si falla algún comando en pipe
```

### Documentación

```bash
#!/bin/bash
#
# Nombre: backup.sh
# Descripción: Script para hacer backup de directorios
# Autor: Usuario
# Versión: 1.0
# Fecha: 2024-01-15
#
# Uso: ./backup.sh <directorio_origen> <directorio_destino>
#

# Verificar argumentos
if [ $# -ne 2 ]; then
    echo "Uso: $0 <origen> <destino>"
    exit 1
fi

# Variables
ORIGEN="$1"
DESTINO="$2"
FECHA=$(date +%Y%m%d_%H%M%S)

# Función principal
main() {
    echo "Iniciando backup..."
    tar -czf "${DESTINO}/backup_${FECHA}.tar.gz" "$ORIGEN"
    echo "Backup completado: backup_${FECHA}.tar.gz"
}

# Ejecutar función principal
main
```

## Troubleshooting y Debugging

### Técnicas de Debug

```bash
# Modo verbose
set -x  # Mostrar comandos ejecutados
set +x  # Desactivar modo verbose

# Debug de scripts
bash -x script.sh

# Verificar sintaxis sin ejecutar
bash -n script.sh

# Mostrar expansión de variables
set -v
```

### Problemas Comunes

**Permisos**
```bash
# Hacer script ejecutable
chmod +x script.sh

# Verificar permisos
ls -l script.sh
```

**PATH Issues**
```bash
# Verificar PATH
echo $PATH

# Encontrar ubicación de comando
which comando
type comando
```

**Variable Issues**
```bash
# Verificar si variable está definida
[ -n "$VARIABLE" ] && echo "Definida" || echo "No definida"

# Mostrar todas las variables
env
set
```

## Shell y Prompt con Usuario Administrador (Root)

### Diferencias Fundamentales

**SÍ, el shell y prompt cambian significativamente** cuando trabajas como usuario administrador (root):

#### Cambios en el Prompt

**Usuario Normal vs Root**
```bash
# Usuario normal
user@hostname:/home/user$ comando

# Usuario root
root@hostname:/root# comando
```

**El símbolo del prompt cambia:**
- **Usuario normal**: `# SHELL Y PROMPT EN LINUX - GUÍA COMPLETA

## ¿Qué es el Shell?

### Definición y Función

El **shell** es un programa que actúa como **interfaz entre el usuario y el kernel** del sistema operativo. Es el intérprete de comandos que:

- **Interpreta y ejecuta comandos** del usuario
- **Proporciona un entorno de trabajo** interactivo
- **Gestiona la entrada y salida** de programas
- **Facilita la automatización** mediante scripts
- **Maneja variables de entorno** y configuraciones

### Arquitectura del Shell

```
┌─────────────────────────────────────────┐
│                USUARIO                  │
└─────────────────┬───────────────────────┘
                  │ Comandos de texto
┌─────────────────▼───────────────────────┐
│                SHELL                    │ ← Intérprete de comandos
│         (bash, zsh, fish, etc.)         │
└─────────────────┬───────────────────────┘
                  │ System calls
┌─────────────────▼───────────────────────┐
│               KERNEL                    │ ← Núcleo del sistema
└─────────────────┬───────────────────────┘
                  │ Hardware access
┌─────────────────▼───────────────────────┐
│              HARDWARE                   │
└─────────────────────────────────────────┘
```

## Historia de los Shells

### Shell Bourne (sh) - 1977

**Desarrollado por Stephen Bourne** en Bell Labs
- **Primer shell estándar** de UNIX
- **Scripting potente** con estructuras de control
- **Variables y funciones** básicas
- **Base de shells modernos**

**Características**
- Control de flujo: if, while, for
- Variables de entorno
- Redirección de entrada/salida
- Pipes para conectar comandos

### C Shell (csh) - 1978

**Desarrollado por Bill Joy** en Berkeley
- **Sintaxis similar a C**
- **Historia de comandos**
- **Alias de comandos**
- **Control de trabajos**

**Mejoras**
- Historial con `!!` y `!n`
- Autocompletado básico
- Expresiones matemáticas
- Arrays y variables indexadas

### Korn Shell (ksh) - 1983

**Desarrollado por David Korn** en Bell Labs
- **Compatible con Bourne Shell**
- **Características de C Shell**
- **Edición de línea de comandos**
- **Funciones avanzadas**

**Innovaciones**
- Edición vi/emacs en línea de comandos
- Aritmética entera built-in
- Arrays asociativos
- Coprocessos

## Bash - Bourne Again Shell

### Historia y Desarrollo

**Desarrollado por Brian Fox** (1989) para el proyecto GNU
- **Sustituto libre** del Bourne Shell
- **Combina características** de sh, csh, y ksh
- **Shell por defecto** en la mayoría de distribuciones Linux
- **Continúa en desarrollo activo**

### Características Principales

**Compatibilidad**
- **Totalmente compatible** con Bourne Shell (sh)
- **Ejecuta scripts** de sh sin modificación
- **Estándar POSIX** compliance
- **Portable** entre sistemas UNIX-like

**Funcionalidades Avanzadas**
- **Autocompletado** inteligente (Tab completion)
- **Historia de comandos** persistente
- **Edición de línea** (vi/emacs modes)
- **Expansión de llaves** `{a,b,c}`
- **Expansión de parámetros** avanzada
- **Arrays** indexados y asociativos

### Configuración de Bash

**Archivos de Configuración**

| Archivo | Scope | Cuándo se ejecuta | Propósito |
|---------|-------|-------------------|-----------|
| `/etc/profile` | Sistema | Login shell | Configuración global |
| `~/.bash_profile` | Usuario | Login shell | Configuración personal de login |
| `~/.bashrc` | Usuario | Interactive shell | Configuración interactiva |
| `~/.bash_logout` | Usuario | Logout | Cleanup al salir |

**Ejemplo de ~/.bashrc**
```bash
# Historial
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTCONTROL=ignoredups:erasedups

# Aliases útiles
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias grep='grep --color=auto'
alias ..='cd ..'
alias ...='cd ../..'

# Variables de entorno
export EDITOR=nano
export PAGER=less
export PATH="$HOME/bin:$PATH"

# Prompt personalizado
PS1='\u@\h:\w\$ '
```

## Shells Modernos

### Zsh (Z Shell)

**Desarrollado por Paul Falstad** (1990)
- **Altamente personalizable**
- **Autocompletado poderoso**
- **Temas y plugins**
- **Compatible con bash**

**Características Destacadas**
- **Corrección automática** de comandos
- **Glob patterns** avanzados
- **Sharing de historial** entre sesiones
- **Framework Oh My Zsh** popular

**Ejemplo de configuración**
```zsh
# ~/.zshrc
# Oh My Zsh
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="agnoster"
plugins=(git docker kubectl)
source $ZSH/oh-my-zsh.sh

# Configuración personalizada
setopt AUTO_CD              # cd automático
setopt CORRECT             # corrección de comandos
setopt HIST_VERIFY         # verificar expansión de historial
```

### Fish (Friendly Interactive Shell)

**Desarrollado por Axel Liljencrantz** (2005)
- **Sintaxis clara** y consistente
- **Autocompletado inteligente**
- **Syntax highlighting** en tiempo real
- **No POSIX compatible** (intencionalmente diferente)

**Filosofía**
- **"Funciona out of the box"**
- **Sin configuración compleja**
- **Experiencia de usuario moderna**
- **Retroalimentación visual**

**Características Únicas**
```fish
# Syntax highlighting en tiempo real
ls -la /home/user/Documents

# Autocompletado basado en historial
git ch[TAB] # sugiere "checkout" si se usó antes

# Funciones simples
function mkcd
    mkdir $argv && cd $argv
end
```

### Otras Shells Especializadas

**tcsh** - Enhanced C Shell
- Versión mejorada de csh
- Edición de línea de comandos
- Programable y personalizable

**dash** - Debian Almquist Shell
- Shell minimalista
- Rápido y ligero
- Usado para scripts del sistema

**xonsh** - Python-powered Shell
- Combina Python con shell
- Sintaxis mixta
- Ideal para programadores Python

## El Prompt - Interfaz de Usuario

### ¿Qué es el Prompt?

El **prompt** es la cadena de texto que el shell muestra para **indicar que está listo para recibir comandos** del usuario.

**Funciones del Prompt**
- **Indicar estado** del shell
- **Mostrar información contextual** (usuario, directorio, hora)
- **Proporcionar feedback visual**
- **Facilitar navegación** y orientación

### Anatomía del Prompt

```
┌── Usuario ── Host ─── Directorio ─── Indicador ──┐
│                                                  │
user@hostname:/current/directory$ comando
│    │        │                  │
│    │        │                  └─ Prompt symbol
│    │        └─ Current working directory
│    └─ Hostname
└─ Username
```

### Variable PS1 en Bash

**PS1** (Prompt String 1) controla el prompt principal

**Códigos de Escape Comunes**

| Código | Descripción | Ejemplo |
|--------|-------------|---------|
| `\u` | Nombre de usuario | `john` |
| `\h` | Hostname (corto) | `laptop` |
| `\H` | Hostname (completo) | `laptop.domain.com` |
| `\w` | Directorio actual (completo) | `/home/john/Documents` |
| `\W` | Directorio actual (basename) | `Documents` |
| `\d` | Fecha | `Mon Jan 15` |
| `\t` | Hora (24h) | `14:30:25` |
| `\T` | Hora (12h) | `02:30:25` |
| `\$` | # si root, $ si usuario normal | `$` |
| `\n` | Nueva línea | |
| `\\` | Backslash literal | `\` |

**Ejemplos de PS1**

```bash
# Prompt simple
PS1='\u@\h:\w\$ '
# Resultado: user@hostname:/current/dir$ 

# Prompt con colores
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
# Resultado: user@hostname:/current/dir$ (con colores)

# Prompt multi-línea
PS1='\[\033[01;33m\]\u@\h\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\]\n\$ '
# Resultado:
# user@hostname /current/dir
# $ 

# Prompt con hora
PS1='[\t] \u@\h:\w\$ '
# Resultado: [14:30:25] user@hostname:/current/dir$ 
```

### Colores en el Prompt

**Códigos de Color ANSI**

| Color | Código | Negrita |
|-------|--------|---------|
| Negro | `\033[30m` | `\033[01;30m` |
| Rojo | `\033[31m` | `\033[01;31m` |
| Verde | `\033[32m` | `\033[01;32m` |
| Amarillo | `\033[33m` | `\033[01;33m` |
| Azul | `\033[34m` | `\033[01;34m` |
| Magenta | `\033[35m` | `\033[01;35m` |
| Cian | `\033[36m` | `\033[01;36m` |
| Blanco | `\033[37m` | `\033[01;37m` |
| Reset | `\033[00m` | |

**Prompt Colorizado Avanzado**
```bash
# Prompt con información de Git
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
```

### Variables de Prompt Adicionales

**PS2** - Prompt de continuación
```bash
PS2='> '  # Aparece cuando el comando continúa en la siguiente línea
```

**PS3** - Prompt para comando `select`
```bash
PS3='Seleccione una opción: '
```

**PS4** - Prompt para modo debug
```bash
PS4='+ '  # Aparece cuando se ejecuta 'set -x'
```

## Funcionalidades Avanzadas del Shell

### Historia de Comandos

**Configuración del Historial**
```bash
# Tamaño del historial en memoria
HISTSIZE=10000

# Tamaño del archivo de historial
HISTFILESIZE=20000

# Control de duplicados
HISTCONTROL=ignoredups:erasedups

# Ignorar comandos específicos
HISTIGNORE="ls:ll:cd:pwd:clear:history"

# Agregar timestamp al historial
HISTTIMEFORMAT='%F %T '
```

**Comandos de Historial**

| Comando | Descripción |
|---------|-------------|
| `history` | Mostrar historial completo |
| `!!` | Ejecutar último comando |
| `!n` | Ejecutar comando número n |
| `!string` | Ejecutar último comando que empieza con string |
| `^old^new` | Reemplazar 'old' por 'new' en último comando |
| `Ctrl+R` | Búsqueda reversa en historial |

### Autocompletado (Tab Completion)

**Tipos de Autocompletado**
- **Comandos**: Nombres de programas en PATH
- **Archivos y directorios**: Basado en filesystem
- **Variables**: Variables de entorno y shell
- **Hostnames**: Para ssh, scp, etc.
- **Usuarios**: Para su, mail, etc.

**Configuración Avanzada**
```bash
# Habilitar autocompletado case-insensitive
bind 'set completion-ignore-case on'

# Mostrar múltiples opciones inmediatamente
bind 'set show-all-if-ambiguous on'

# Completado programable personalizado
complete -W "start stop restart status" service
```

### Aliases y Funciones

**Aliases Útiles**
```bash
# Navegación
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# Listado de archivos
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias lt='ls -ltr'  # Ordenado por tiempo

# Comandos con colores
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# Seguridad
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Utilidades
alias h='history'
alias j='jobs -l'
alias ports='netstat -tulanp'
```

**Funciones Avanzadas**
```bash
# Crear directorio y entrar en él
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extraer archivos comprimidos
extract() {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar e $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)     echo "'$1' no se puede extraer" ;;
        esac
    else
        echo "'$1' no es un archivo válido"
    fi
}

# Buscar y matar procesos
pk() {
    ps aux | grep $1 | grep -v grep | awk '{print $2}' | xargs kill -9
}
```

## Redirección y Pipes

### Redirección de Entrada/Salida

**Redirección Básica**
```bash
# Redirección de salida
comando > archivo          # Sobrescribir
comando >> archivo         # Agregar

# Redirección de entrada
comando < archivo

# Redirección de error estándar
comando 2> error.log       # Solo errores
comando &> archivo         # Salida y errores
comando > archivo 2>&1     # Salida y errores (compatible)
```

**Redirección Avanzada**
```bash
# Here documents
cat << EOF > archivo.txt
Este es el contenido
del archivo
EOF

# Here strings
grep "patrón" <<< "texto a buscar"

# Redirección a múltiples archivos
comando | tee archivo1.txt archivo2.txt
```

### Pipes y Filtros

**Filosofía UNIX**: "Do one thing and do it well"

```bash
# Cadena de pipes básica
ps aux | grep python | wc -l

# Análisis de logs
cat /var/log/apache/access.log | \
    grep "404" | \
    awk '{print $1}' | \
    sort | \
    uniq -c | \
    sort -nr | \
    head -10

# Procesamiento de texto
cat archivo.txt | \
    tr '[:upper:]' '[:lower:]' | \
    sed 's/old/new/g' | \
    sort | \
    uniq > resultado.txt
```

## Control de Trabajos

### Gestión de Procesos

**Comandos de Control**
```bash
# Ejecutar en background
comando &

# Suspender proceso actual
Ctrl+Z

# Listar trabajos
jobs

# Traer trabajo a foreground
fg %1

# Enviar trabajo a background
bg %1

# Terminar trabajo
kill %1
```

**Ejemplo Práctico**
```bash
# Iniciar editor en background
nano archivo.txt &

# Verificar trabajos
jobs
# [1]+  Running    nano archivo.txt &

# Traer a foreground cuando sea necesario
fg %1
```

### Signals y Control de Procesos

**Signals Comunes**

| Signal | Número | Descripción |
|--------|--------|-------------|
| SIGTERM | 15 | Terminación normal |
| SIGKILL | 9 | Terminación forzada |
| SIGSTOP | 19 | Suspender proceso |
| SIGCONT | 18 | Continuar proceso |
| SIGINT | 2 | Interrupción (Ctrl+C) |

```bash
# Terminar proceso por PID
kill 1234
kill -15 1234  # Equivalente

# Forzar terminación
kill -9 1234

# Terminar por nombre
killall firefox
pkill python
```

## Personalización Avanzada

### Frameworks de Shell

**Oh My Zsh** (para Zsh)
```bash
# Instalación
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Configuración ~/.zshrc
ZSH_THEME="agnoster"
plugins=(git docker kubectl auto-suggestions syntax-highlighting)
```

**Oh My Bash** (para Bash)
```bash
# Instalación
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

**Starship** (Cross-shell)
```bash
# Instalación
curl -sS https://starship.rs/install.sh | sh

# Agregar a ~/.bashrc o ~/.zshrc
eval "$(starship init bash)"  # para bash
eval "$(starship init zsh)"   # para zsh
```

### Prompt Inteligente

**Prompt con Información de Git**
```bash
# Función para mostrar branch de Git
git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

# Función para mostrar estado de Git
git_status() {
    if git rev-parse --git-dir > /dev/null 2>&1; then
        if [[ $(git status --porcelain) ]]; then
            echo "*"
        fi
    fi
}

# Prompt con información completa
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(git_branch)\[\033[01;33m\]$(git_status)\[\033[00m\]\$ '
```

**Prompt con Código de Salida**
```bash
# Mostrar código de salida del último comando
PS1='$(if [[ $? == 0 ]]; then echo "\[\033[01;32m\]✓"; else echo "\[\033[01;31m\]✗"; fi)\[\033[00m\] \u@\h:\w\$ '
```

### Variables de Entorno Importantes

**Variables del Sistema**
```bash
# Path de búsqueda de comandos
echo $PATH

# Directorio home del usuario
echo $HOME

# Usuario actual
echo $USER

# Editor por defecto
export EDITOR=nano

# Pager por defecto
export PAGER=less

# Idioma del sistema
export LANG=en_US.UTF-8
```

**Variables del Shell**
```bash
# Shell actual
echo $SHELL

# Opciones del shell
echo $SHELLOPTS

# PID del shell
echo $$

# Último directorio
echo $OLDPWD
```

## Scripting Básico

### Estructura de un Script

```bash
#!/bin/bash
# Shebang - especifica el intérprete

# Comentarios empiezan con #

# Variables
nombre="Juan"
edad=25

# Uso de variables
echo "Hola $nombre, tienes $edad años"
echo "En 10 años tendrás $((edad + 10)) años"

# Lectura de entrada
read -p "¿Cómo te llamas? " nombre_usuario
echo "Hola $nombre_usuario"
```

### Estructuras de Control

```bash
# Condicionales
if [ "$edad" -ge 18 ]; then
    echo "Eres mayor de edad"
elif [ "$edad" -ge 13 ]; then
    echo "Eres adolescente"
else
    echo "Eres niño"
fi

# Bucles
for i in {1..5}; do
    echo "Iteración $i"
done

# While
contador=1
while [ $contador -le 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done

# Case
case $1 in
    start)
        echo "Iniciando servicio..."
        ;;
    stop)
        echo "Deteniendo servicio..."
        ;;
    *)
        echo "Uso: $0 {start|stop}"
        ;;
esac
```

## Mejores Prácticas

### Seguridad

```bash
# Usar comillas para prevenir word splitting
nombre="Juan Pérez"
echo "$nombre"  # Correcto
echo $nombre    # Incorrecto

# Verificar existencia de archivos
if [ -f "$archivo" ]; then
    cat "$archivo"
fi

# Usar -n y -z para verificar strings
if [ -n "$variable" ]; then  # No vacía
    echo "Variable tiene contenido"
fi

if [ -z "$variable" ]; then  # Vacía
    echo "Variable está vacía"
fi
```

### Optimización

```bash
# Usar funciones para código repetitivo
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1"
}

# Usar arrays para múltiples valores
frutas=("manzana" "naranja" "plátano")
for fruta in "${frutas[@]}"; do
    echo "Me gusta la $fruta"
done

# Manejo de errores
set -e  # Salir si algún comando falla
set -u  # Error si variable no definida
set -o pipefail  # Error si falla algún comando en pipe
```

### Documentación

```bash
#!/bin/bash
#
# Nombre: backup.sh
# Descripción: Script para hacer backup de directorios
# Autor: Usuario
# Versión: 1.0
# Fecha: 2024-01-15
#
# Uso: ./backup.sh <directorio_origen> <directorio_destino>
#

# Verificar argumentos
if [ $# -ne 2 ]; then
    echo "Uso: $0 <origen> <destino>"
    exit 1
fi

# Variables
ORIGEN="$1"
DESTINO="$2"
FECHA=$(date +%Y%m%d_%H%M%S)

# Función principal
main() {
    echo "Iniciando backup..."
    tar -czf "${DESTINO}/backup_${FECHA}.tar.gz" "$ORIGEN"
    echo "Backup completado: backup_${FECHA}.tar.gz"
}

# Ejecutar función principal
main
```

## Troubleshooting y Debugging

### Técnicas de Debug

```bash
# Modo verbose
set -x  # Mostrar comandos ejecutados
set +x  # Desactivar modo verbose

# Debug de scripts
bash -x script.sh

# Verificar sintaxis sin ejecutar
bash -n script.sh

# Mostrar expansión de variables
set -v
```

### Problemas Comunes

**Permisos**
```bash
# Hacer script ejecutable
chmod +x script.sh

# Verificar permisos
ls -l script.sh
```

**PATH Issues**
```bash
# Verificar PATH
echo $PATH

# Encontrar ubicación de comando
which comando
type comando
```

**Variable Issues**
```bash
# Verificar si variable está definida
[ -n "$VARIABLE" ] && echo "Definida" || echo "No definida"

# Mostrar todas las variables
env
set
```

 (dólar)
- **Usuario root**: `#` (hashtag/numeral)

#### Variable PS1 para Root

**Detección Automática**
```bash
# PS1 que cambia automáticamente
PS1='\u@\h:\w\$ '
# \$ muestra # si UID=0 (root), $ si UID>0 (usuario normal)

# Versión explícita
if [ "$EUID" -eq 0 ]; then
    PS1='\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]# '
else
    PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
fi
```

### Archivos de Configuración Diferentes

**Ubicaciones por Usuario**

| Usuario | Home Directory | .bashrc | .bash_profile |
|---------|----------------|---------|---------------|
| Normal | `/home/usuario` | `/home/usuario/.bashrc` | `/home/usuario/.bash_profile` |
| Root | `/root` | `/root/.bashrc` | `/root/.bash_profile` |

**Configuración Global vs Personal**
```bash
# Configuración global (afecta a todos)
/etc/profile
/etc/bash.bashrc
/etc/bashrc

# Configuración de root
/root/.bashrc
/root/.bash_profile
/root/.profile
```

### Diferencias en Variables de Entorno

**PATH Diferente**
```bash
# Usuario normal
echo $PATH
# /usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games

# Usuario root
echo $PATH
# /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

**Variables Específicas de Root**
```bash
# Como root
echo $USER     # root
echo $HOME     # /root
echo $SHELL    # /bin/bash (o el shell configurado para root)
echo $LOGNAME  # root
echo $UID      # 0
```

### Seguridad y Advertencias Visuales

**Prompt con Advertencias**
```bash
# Prompt de root con colores de advertencia
PS1='\[\033[01;31m\]ROOT\[\033[00m\]@\[\033[01;33m\]\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]# '
# Resultado: ROOT@hostname:/current/dir# (en rojo)

# Prompt que destaca el peligro
PS1='\[\033[41;37m\] ROOT \[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] # '
# Resultado: [ ROOT ] /current/dir # (fondo rojo)
```

### Formas de Obtener Privilegios de Root

#### 1. Login Directo como Root
```bash
# En login screen
Username: root
Password: [root_password]

# Prompt resultante
root@hostname:~# 
```

#### 2. Comando su (Switch User)
```bash
# Cambiar a root (requiere password de root)
su -
# Password: [root_password]
root@hostname:~# 

# Mantener variables de entorno del usuario original
su
# Password: [root_password]
root@hostname:/home/usuario# 
```

#### 3. Comando sudo (Substitute User Do)
```bash
# Ejecutar comando como root
sudo comando
# [sudo] password for usuario: [user_password]

# Obtener shell de root con sudo
sudo -i
# [sudo] password for usuario: [user_password]
root@hostname:~# 

# Shell de root preservando entorno
sudo -s
root@hostname:/home/usuario# 
```

### Diferencias entre su y sudo

**su (Switch User)**
```bash
su -           # Login shell de root (entorno limpio)
su             # Shell de root (entorno parcial del usuario)
su usuario     # Cambiar a otro usuario
```

**sudo (Substitute User Do)**
```bash
sudo comando           # Ejecutar un comando como root
sudo -i               # Login shell de root
sudo -s               # Shell de root (entorno del usuario)
sudo -u usuario comando # Ejecutar como otro usuario
```

**Ventajas de sudo**
- **No necesita password de root**
- **Auditoría completa** (/var/log/auth.log)
- **Permisos granulares** (/etc/sudoers)
- **Timeout de credenciales** (15 min por defecto)

### Configuración de Seguridad

**Archivo /etc/sudoers**
```bash
# Editar con visudo (nunca directamente)
sudo visudo

# Permitir al usuario ejecutar todo como root
usuario ALL=(ALL:ALL) ALL

# Permitir sin password
usuario ALL=(ALL) NOPASSWD: ALL

# Permitir comandos específicos
usuario ALL=(ALL) /bin/systemctl, /bin/mount
```

**Configuración de Root Shell**
```bash
# Verificar shell de root
grep root /etc/passwd
# root:x:0:0:root:/root:/bin/bash

# Cambiar shell de root
chsh -s /bin/zsh root
```

### Buenas Prácticas de Seguridad

#### 1. Deshabilitar Login Directo de Root
```bash
# Editar /etc/ssh/sshd_config
PermitRootLogin no

# Reiniciar SSH
systemctl restart sshd
```

#### 2. Usar sudo en lugar de su
```bash
# En lugar de
su -
comando

# Usar
sudo comando
# o
sudo -i
```

#### 3. Prompt de Advertencia para Root
```bash
# En /root/.bashrc
PS1='\[\033[01;41;37m\] ⚠ ROOT ⚠ \[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \[\033[01;31m\]#\[\033[00m\] '

# Mensaje de advertencia al hacer su/sudo
echo "⚠️  CUIDADO: Estás ejecutando comandos como ROOT ⚠️"
echo "   - Todos los comandos tienen privilegios máximos"
echo "   - Un error puede dañar el sistema"
echo "   - Sal del modo root tan pronto como termines"
echo ""
```

### Aliases Específicos para Root

```bash
# En /root/.bashrc
# Aliases de seguridad
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
alias chown='chown --preserve-root'
alias chmod='chmod --preserve-root'
alias chgrp='chgrp --preserve-root'

# Prevenir borrado accidental del sistema
alias rm='rm --preserve-root'

# Comandos útiles para administración
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'

# Información del sistema
alias df='df -h'
alias du='du -h'
alias free='free -h'
alias ps='ps auxf'
alias psg='ps aux | grep -v grep | grep -i -e VSZ -e'

# Servicios
alias sctl='systemctl'
alias jctl='journalctl'
```

### Diferencias en Permisos y Capacidades

**Como Usuario Normal**
```bash
# Permisos limitados
ls /root
# ls: cannot open directory '/root': Permission denied

# Necesita sudo para comandos administrativos
systemctl restart apache2
# Failed to restart apache2.service: Access denied
```

**Como Root**
```bash
# Acceso total al sistema
ls /root
# archivo1 archivo2 directorio1

# Control total de servicios
systemctl restart apache2
# Comando ejecutado sin problemas

# Modificación de archivos del sistema
echo "configuración" >> /etc/importante.conf
# Sin restricciones
```

### Indicadores Visuales Avanzados

**Prompt Multi-información**
```bash
# Para root - Prompt muy informativo
PS1='\[\033[01;41;37m\] ROOT \[\033[00m\]\[\033[01;31m\]@\[\033[00m\]\[\033[01;33m\]\h\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \[\033[01;35m\][\t]\[\033[00m\]\n\[\033[01;31m\]# \[\033[00m\]'

# Resultado:
# [ ROOT ]@hostname /current/directory [14:30:25]
# # 
```

**Con información del sistema**
```bash
# Función para mostrar carga del sistema
system_load() {
    uptime | awk '{print $10}' | sed 's/,//'
}

# Prompt con carga del sistema
PS1='\[\033[01;41;37m\] ROOT \[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \[\033[01;33m\][$(system_load)]\[\033[00m\] \[\033[01;31m\]#\[\033[00m\] '
```

## Recursos y Herramientas

### Herramientas de Terminal

**Multiplexores**
- **tmux**: Terminal multiplexer moderno
- **screen**: Multiplexer tradicional
- **byobu**: Wrapper amigable para tmux/screen

**Mejoras de Terminal**
- **fzf**: Fuzzy finder
- **ripgrep**: Búsqueda de texto rápida
- **exa**: Reemplazo moderno de ls
- **bat**: cat con syntax highlighting

### Documentación

**Manuales**
```bash
man bash          # Manual de bash
info bash         # Info de GNU bash
help cd           # Ayuda built-in de bash
type comando      # Información sobre comando
```

**Recursos Online**
- **Advanced Bash-Scripting Guide**: Guía completa
- **ShellCheck**: Linter para shell scripts
- **Bash Reference Manual**: Documentación oficial
- **ExplainShell**: Explicación interactiva de comandos

## Conclusión

El shell y prompt cambian significativamente cuando trabajas como administrador:

**Cambios Visuales**
- Prompt termina en `#` en lugar de `# SHELL Y PROMPT EN LINUX - GUÍA COMPLETA

## ¿Qué es el Shell?

### Definición y Función

El **shell** es un programa que actúa como **interfaz entre el usuario y el kernel** del sistema operativo. Es el intérprete de comandos que:

- **Interpreta y ejecuta comandos** del usuario
- **Proporciona un entorno de trabajo** interactivo
- **Gestiona la entrada y salida** de programas
- **Facilita la automatización** mediante scripts
- **Maneja variables de entorno** y configuraciones

### Arquitectura del Shell

```
┌─────────────────────────────────────────┐
│                USUARIO                  │
└─────────────────┬───────────────────────┘
                  │ Comandos de texto
┌─────────────────▼───────────────────────┐
│                SHELL                    │ ← Intérprete de comandos
│         (bash, zsh, fish, etc.)         │
└─────────────────┬───────────────────────┘
                  │ System calls
┌─────────────────▼───────────────────────┐
│               KERNEL                    │ ← Núcleo del sistema
└─────────────────┬───────────────────────┘
                  │ Hardware access
┌─────────────────▼───────────────────────┐
│              HARDWARE                   │
└─────────────────────────────────────────┘
```

## Historia de los Shells

### Shell Bourne (sh) - 1977

**Desarrollado por Stephen Bourne** en Bell Labs
- **Primer shell estándar** de UNIX
- **Scripting potente** con estructuras de control
- **Variables y funciones** básicas
- **Base de shells modernos**

**Características**
- Control de flujo: if, while, for
- Variables de entorno
- Redirección de entrada/salida
- Pipes para conectar comandos

### C Shell (csh) - 1978

**Desarrollado por Bill Joy** en Berkeley
- **Sintaxis similar a C**
- **Historia de comandos**
- **Alias de comandos**
- **Control de trabajos**

**Mejoras**
- Historial con `!!` y `!n`
- Autocompletado básico
- Expresiones matemáticas
- Arrays y variables indexadas

### Korn Shell (ksh) - 1983

**Desarrollado por David Korn** en Bell Labs
- **Compatible con Bourne Shell**
- **Características de C Shell**
- **Edición de línea de comandos**
- **Funciones avanzadas**

**Innovaciones**
- Edición vi/emacs en línea de comandos
- Aritmética entera built-in
- Arrays asociativos
- Coprocessos

## Bash - Bourne Again Shell

### Historia y Desarrollo

**Desarrollado por Brian Fox** (1989) para el proyecto GNU
- **Sustituto libre** del Bourne Shell
- **Combina características** de sh, csh, y ksh
- **Shell por defecto** en la mayoría de distribuciones Linux
- **Continúa en desarrollo activo**

### Características Principales

**Compatibilidad**
- **Totalmente compatible** con Bourne Shell (sh)
- **Ejecuta scripts** de sh sin modificación
- **Estándar POSIX** compliance
- **Portable** entre sistemas UNIX-like

**Funcionalidades Avanzadas**
- **Autocompletado** inteligente (Tab completion)
- **Historia de comandos** persistente
- **Edición de línea** (vi/emacs modes)
- **Expansión de llaves** `{a,b,c}`
- **Expansión de parámetros** avanzada
- **Arrays** indexados y asociativos

### Configuración de Bash

**Archivos de Configuración**

| Archivo | Scope | Cuándo se ejecuta | Propósito |
|---------|-------|-------------------|-----------|
| `/etc/profile` | Sistema | Login shell | Configuración global |
| `~/.bash_profile` | Usuario | Login shell | Configuración personal de login |
| `~/.bashrc` | Usuario | Interactive shell | Configuración interactiva |
| `~/.bash_logout` | Usuario | Logout | Cleanup al salir |

**Ejemplo de ~/.bashrc**
```bash
# Historial
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTCONTROL=ignoredups:erasedups

# Aliases útiles
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias grep='grep --color=auto'
alias ..='cd ..'
alias ...='cd ../..'

# Variables de entorno
export EDITOR=nano
export PAGER=less
export PATH="$HOME/bin:$PATH"

# Prompt personalizado
PS1='\u@\h:\w\$ '
```

## Shells Modernos

### Zsh (Z Shell)

**Desarrollado por Paul Falstad** (1990)
- **Altamente personalizable**
- **Autocompletado poderoso**
- **Temas y plugins**
- **Compatible con bash**

**Características Destacadas**
- **Corrección automática** de comandos
- **Glob patterns** avanzados
- **Sharing de historial** entre sesiones
- **Framework Oh My Zsh** popular

**Ejemplo de configuración**
```zsh
# ~/.zshrc
# Oh My Zsh
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="agnoster"
plugins=(git docker kubectl)
source $ZSH/oh-my-zsh.sh

# Configuración personalizada
setopt AUTO_CD              # cd automático
setopt CORRECT             # corrección de comandos
setopt HIST_VERIFY         # verificar expansión de historial
```

### Fish (Friendly Interactive Shell)

**Desarrollado por Axel Liljencrantz** (2005)
- **Sintaxis clara** y consistente
- **Autocompletado inteligente**
- **Syntax highlighting** en tiempo real
- **No POSIX compatible** (intencionalmente diferente)

**Filosofía**
- **"Funciona out of the box"**
- **Sin configuración compleja**
- **Experiencia de usuario moderna**
- **Retroalimentación visual**

**Características Únicas**
```fish
# Syntax highlighting en tiempo real
ls -la /home/user/Documents

# Autocompletado basado en historial
git ch[TAB] # sugiere "checkout" si se usó antes

# Funciones simples
function mkcd
    mkdir $argv && cd $argv
end
```

### Otras Shells Especializadas

**tcsh** - Enhanced C Shell
- Versión mejorada de csh
- Edición de línea de comandos
- Programable y personalizable

**dash** - Debian Almquist Shell
- Shell minimalista
- Rápido y ligero
- Usado para scripts del sistema

**xonsh** - Python-powered Shell
- Combina Python con shell
- Sintaxis mixta
- Ideal para programadores Python

## El Prompt - Interfaz de Usuario

### ¿Qué es el Prompt?

El **prompt** es la cadena de texto que el shell muestra para **indicar que está listo para recibir comandos** del usuario.

**Funciones del Prompt**
- **Indicar estado** del shell
- **Mostrar información contextual** (usuario, directorio, hora)
- **Proporcionar feedback visual**
- **Facilitar navegación** y orientación

### Anatomía del Prompt

```
┌── Usuario ── Host ─── Directorio ─── Indicador ──┐
│                                                  │
user@hostname:/current/directory$ comando
│    │        │                  │
│    │        │                  └─ Prompt symbol
│    │        └─ Current working directory
│    └─ Hostname
└─ Username
```

### Variable PS1 en Bash

**PS1** (Prompt String 1) controla el prompt principal

**Códigos de Escape Comunes**

| Código | Descripción | Ejemplo |
|--------|-------------|---------|
| `\u` | Nombre de usuario | `john` |
| `\h` | Hostname (corto) | `laptop` |
| `\H` | Hostname (completo) | `laptop.domain.com` |
| `\w` | Directorio actual (completo) | `/home/john/Documents` |
| `\W` | Directorio actual (basename) | `Documents` |
| `\d` | Fecha | `Mon Jan 15` |
| `\t` | Hora (24h) | `14:30:25` |
| `\T` | Hora (12h) | `02:30:25` |
| `\$` | # si root, $ si usuario normal | `$` |
| `\n` | Nueva línea | |
| `\\` | Backslash literal | `\` |

**Ejemplos de PS1**

```bash
# Prompt simple
PS1='\u@\h:\w\$ '
# Resultado: user@hostname:/current/dir$ 

# Prompt con colores
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
# Resultado: user@hostname:/current/dir$ (con colores)

# Prompt multi-línea
PS1='\[\033[01;33m\]\u@\h\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\]\n\$ '
# Resultado:
# user@hostname /current/dir
# $ 

# Prompt con hora
PS1='[\t] \u@\h:\w\$ '
# Resultado: [14:30:25] user@hostname:/current/dir$ 
```

### Colores en el Prompt

**Códigos de Color ANSI**

| Color | Código | Negrita |
|-------|--------|---------|
| Negro | `\033[30m` | `\033[01;30m` |
| Rojo | `\033[31m` | `\033[01;31m` |
| Verde | `\033[32m` | `\033[01;32m` |
| Amarillo | `\033[33m` | `\033[01;33m` |
| Azul | `\033[34m` | `\033[01;34m` |
| Magenta | `\033[35m` | `\033[01;35m` |
| Cian | `\033[36m` | `\033[01;36m` |
| Blanco | `\033[37m` | `\033[01;37m` |
| Reset | `\033[00m` | |

**Prompt Colorizado Avanzado**
```bash
# Prompt con información de Git
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
```

### Variables de Prompt Adicionales

**PS2** - Prompt de continuación
```bash
PS2='> '  # Aparece cuando el comando continúa en la siguiente línea
```

**PS3** - Prompt para comando `select`
```bash
PS3='Seleccione una opción: '
```

**PS4** - Prompt para modo debug
```bash
PS4='+ '  # Aparece cuando se ejecuta 'set -x'
```

## Funcionalidades Avanzadas del Shell

### Historia de Comandos

**Configuración del Historial**
```bash
# Tamaño del historial en memoria
HISTSIZE=10000

# Tamaño del archivo de historial
HISTFILESIZE=20000

# Control de duplicados
HISTCONTROL=ignoredups:erasedups

# Ignorar comandos específicos
HISTIGNORE="ls:ll:cd:pwd:clear:history"

# Agregar timestamp al historial
HISTTIMEFORMAT='%F %T '
```

**Comandos de Historial**

| Comando | Descripción |
|---------|-------------|
| `history` | Mostrar historial completo |
| `!!` | Ejecutar último comando |
| `!n` | Ejecutar comando número n |
| `!string` | Ejecutar último comando que empieza con string |
| `^old^new` | Reemplazar 'old' por 'new' en último comando |
| `Ctrl+R` | Búsqueda reversa en historial |

### Autocompletado (Tab Completion)

**Tipos de Autocompletado**
- **Comandos**: Nombres de programas en PATH
- **Archivos y directorios**: Basado en filesystem
- **Variables**: Variables de entorno y shell
- **Hostnames**: Para ssh, scp, etc.
- **Usuarios**: Para su, mail, etc.

**Configuración Avanzada**
```bash
# Habilitar autocompletado case-insensitive
bind 'set completion-ignore-case on'

# Mostrar múltiples opciones inmediatamente
bind 'set show-all-if-ambiguous on'

# Completado programable personalizado
complete -W "start stop restart status" service
```

### Aliases y Funciones

**Aliases Útiles**
```bash
# Navegación
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# Listado de archivos
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias lt='ls -ltr'  # Ordenado por tiempo

# Comandos con colores
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# Seguridad
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Utilidades
alias h='history'
alias j='jobs -l'
alias ports='netstat -tulanp'
```

**Funciones Avanzadas**
```bash
# Crear directorio y entrar en él
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extraer archivos comprimidos
extract() {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar e $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)     echo "'$1' no se puede extraer" ;;
        esac
    else
        echo "'$1' no es un archivo válido"
    fi
}

# Buscar y matar procesos
pk() {
    ps aux | grep $1 | grep -v grep | awk '{print $2}' | xargs kill -9
}
```

## Redirección y Pipes

### Redirección de Entrada/Salida

**Redirección Básica**
```bash
# Redirección de salida
comando > archivo          # Sobrescribir
comando >> archivo         # Agregar

# Redirección de entrada
comando < archivo

# Redirección de error estándar
comando 2> error.log       # Solo errores
comando &> archivo         # Salida y errores
comando > archivo 2>&1     # Salida y errores (compatible)
```

**Redirección Avanzada**
```bash
# Here documents
cat << EOF > archivo.txt
Este es el contenido
del archivo
EOF

# Here strings
grep "patrón" <<< "texto a buscar"

# Redirección a múltiples archivos
comando | tee archivo1.txt archivo2.txt
```

### Pipes y Filtros

**Filosofía UNIX**: "Do one thing and do it well"

```bash
# Cadena de pipes básica
ps aux | grep python | wc -l

# Análisis de logs
cat /var/log/apache/access.log | \
    grep "404" | \
    awk '{print $1}' | \
    sort | \
    uniq -c | \
    sort -nr | \
    head -10

# Procesamiento de texto
cat archivo.txt | \
    tr '[:upper:]' '[:lower:]' | \
    sed 's/old/new/g' | \
    sort | \
    uniq > resultado.txt
```

## Control de Trabajos

### Gestión de Procesos

**Comandos de Control**
```bash
# Ejecutar en background
comando &

# Suspender proceso actual
Ctrl+Z

# Listar trabajos
jobs

# Traer trabajo a foreground
fg %1

# Enviar trabajo a background
bg %1

# Terminar trabajo
kill %1
```

**Ejemplo Práctico**
```bash
# Iniciar editor en background
nano archivo.txt &

# Verificar trabajos
jobs
# [1]+  Running    nano archivo.txt &

# Traer a foreground cuando sea necesario
fg %1
```

### Signals y Control de Procesos

**Signals Comunes**

| Signal | Número | Descripción |
|--------|--------|-------------|
| SIGTERM | 15 | Terminación normal |
| SIGKILL | 9 | Terminación forzada |
| SIGSTOP | 19 | Suspender proceso |
| SIGCONT | 18 | Continuar proceso |
| SIGINT | 2 | Interrupción (Ctrl+C) |

```bash
# Terminar proceso por PID
kill 1234
kill -15 1234  # Equivalente

# Forzar terminación
kill -9 1234

# Terminar por nombre
killall firefox
pkill python
```

## Personalización Avanzada

### Frameworks de Shell

**Oh My Zsh** (para Zsh)
```bash
# Instalación
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Configuración ~/.zshrc
ZSH_THEME="agnoster"
plugins=(git docker kubectl auto-suggestions syntax-highlighting)
```

**Oh My Bash** (para Bash)
```bash
# Instalación
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

**Starship** (Cross-shell)
```bash
# Instalación
curl -sS https://starship.rs/install.sh | sh

# Agregar a ~/.bashrc o ~/.zshrc
eval "$(starship init bash)"  # para bash
eval "$(starship init zsh)"   # para zsh
```

### Prompt Inteligente

**Prompt con Información de Git**
```bash
# Función para mostrar branch de Git
git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

# Función para mostrar estado de Git
git_status() {
    if git rev-parse --git-dir > /dev/null 2>&1; then
        if [[ $(git status --porcelain) ]]; then
            echo "*"
        fi
    fi
}

# Prompt con información completa
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(git_branch)\[\033[01;33m\]$(git_status)\[\033[00m\]\$ '
```

**Prompt con Código de Salida**
```bash
# Mostrar código de salida del último comando
PS1='$(if [[ $? == 0 ]]; then echo "\[\033[01;32m\]✓"; else echo "\[\033[01;31m\]✗"; fi)\[\033[00m\] \u@\h:\w\$ '
```

### Variables de Entorno Importantes

**Variables del Sistema**
```bash
# Path de búsqueda de comandos
echo $PATH

# Directorio home del usuario
echo $HOME

# Usuario actual
echo $USER

# Editor por defecto
export EDITOR=nano

# Pager por defecto
export PAGER=less

# Idioma del sistema
export LANG=en_US.UTF-8
```

**Variables del Shell**
```bash
# Shell actual
echo $SHELL

# Opciones del shell
echo $SHELLOPTS

# PID del shell
echo $$

# Último directorio
echo $OLDPWD
```

## Scripting Básico

### Estructura de un Script

```bash
#!/bin/bash
# Shebang - especifica el intérprete

# Comentarios empiezan con #

# Variables
nombre="Juan"
edad=25

# Uso de variables
echo "Hola $nombre, tienes $edad años"
echo "En 10 años tendrás $((edad + 10)) años"

# Lectura de entrada
read -p "¿Cómo te llamas? " nombre_usuario
echo "Hola $nombre_usuario"
```

### Estructuras de Control

```bash
# Condicionales
if [ "$edad" -ge 18 ]; then
    echo "Eres mayor de edad"
elif [ "$edad" -ge 13 ]; then
    echo "Eres adolescente"
else
    echo "Eres niño"
fi

# Bucles
for i in {1..5}; do
    echo "Iteración $i"
done

# While
contador=1
while [ $contador -le 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done

# Case
case $1 in
    start)
        echo "Iniciando servicio..."
        ;;
    stop)
        echo "Deteniendo servicio..."
        ;;
    *)
        echo "Uso: $0 {start|stop}"
        ;;
esac
```

## Mejores Prácticas

### Seguridad

```bash
# Usar comillas para prevenir word splitting
nombre="Juan Pérez"
echo "$nombre"  # Correcto
echo $nombre    # Incorrecto

# Verificar existencia de archivos
if [ -f "$archivo" ]; then
    cat "$archivo"
fi

# Usar -n y -z para verificar strings
if [ -n "$variable" ]; then  # No vacía
    echo "Variable tiene contenido"
fi

if [ -z "$variable" ]; then  # Vacía
    echo "Variable está vacía"
fi
```

### Optimización

```bash
# Usar funciones para código repetitivo
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1"
}

# Usar arrays para múltiples valores
frutas=("manzana" "naranja" "plátano")
for fruta in "${frutas[@]}"; do
    echo "Me gusta la $fruta"
done

# Manejo de errores
set -e  # Salir si algún comando falla
set -u  # Error si variable no definida
set -o pipefail  # Error si falla algún comando en pipe
```

### Documentación

```bash
#!/bin/bash
#
# Nombre: backup.sh
# Descripción: Script para hacer backup de directorios
# Autor: Usuario
# Versión: 1.0
# Fecha: 2024-01-15
#
# Uso: ./backup.sh <directorio_origen> <directorio_destino>
#

# Verificar argumentos
if [ $# -ne 2 ]; then
    echo "Uso: $0 <origen> <destino>"
    exit 1
fi

# Variables
ORIGEN="$1"
DESTINO="$2"
FECHA=$(date +%Y%m%d_%H%M%S)

# Función principal
main() {
    echo "Iniciando backup..."
    tar -czf "${DESTINO}/backup_${FECHA}.tar.gz" "$ORIGEN"
    echo "Backup completado: backup_${FECHA}.tar.gz"
}

# Ejecutar función principal
main
```

## Troubleshooting y Debugging

### Técnicas de Debug

```bash
# Modo verbose
set -x  # Mostrar comandos ejecutados
set +x  # Desactivar modo verbose

# Debug de scripts
bash -x script.sh

# Verificar sintaxis sin ejecutar
bash -n script.sh

# Mostrar expansión de variables
set -v
```

### Problemas Comunes

**Permisos**
```bash
# Hacer script ejecutable
chmod +x script.sh

# Verificar permisos
ls -l script.sh
```

**PATH Issues**
```bash
# Verificar PATH
echo $PATH

# Encontrar ubicación de comando
which comando
type comando
```

**Variable Issues**
```bash
# Verificar si variable está definida
[ -n "$VARIABLE" ] && echo "Definida" || echo "No definida"

# Mostrar todas las variables
env
set
```


- Colores de advertencia (rojo) comúnmente usados
- Información adicional (warnings, carga del sistema)

**Cambios Funcionales**
- Diferentes archivos de configuración (`/root/*`)
- PATH extendido con directorios `sbin`
- Variables de entorno específicas de root
- Acceso total al sistema sin restricciones

**Implicaciones de Seguridad**
- Poder absoluto requiere responsabilidad extrema
- Un error puede comprometer todo el sistema
- Auditoría y logging más importantes
- Mejores prácticas de seguridad esenciales

El dominio del shell y el prompt, tanto para usuarios normales como para administradores, es fundamental para la productividad y seguridad en Linux. La personalización adecuada puede transformar la experiencia de línea de comandos de intimidante a poderosa y eficiente, mientras mantiene la conciencia de los privilegios y responsabilidades en cada contexto.