---
layout: post
title: "Shell scripts arguments"
date: 2017-09-26
description: Una forma sencilla y efectiva para leer los parámetros de entrada de tus scripts de shell.
tags:
- scripting
- bash
- shell
categories: 
- Scripting
- Tips
- Snippets
twitter_text: How to read arguments in shell scripts
---

Cuando escribimos **scripts de bash/shell**, la mayoría de las veces necesitamos que reciban parámetros de entrada, y los solemos leer haciendo algo así:

```shell
#!/bin/bash

s=$1
p=$2

echo "s = ${s}" 
echo "p = ${p}"
```
Este script lo ejecutaríamos así: `./test.sh foo bar`. Esta forma de leer parámetros es la más sencilla, pero tiene inconvenientes cuando nuestro script es complejo y la lista de argumentos es larga, pueden ser o no opcionales, y pueden introducirse en cualquier orden. Para estos casos, podemos usar la utilidad del sistema `getopts`, échale un ojo a este script!:

```shell
#!/bin/bash

usage() { 
    echo "Usage: $0 [-s <string>] [-p <string>] <string>" 1>&2; exit 1; 
}

# Loop over all the options with "getopts"
while getopts ":s:p:" option; do
    case "${option}" in
        s)
            s=${OPTARG}
            ;;
        p)
            p=${OPTARG}
            ;;
        *)
            usage
            ;;
    esac
done

# skip all the "opts" arguments and read the rest of the arguments. In this case
# we only read one string argument
shift $((OPTIND-1))
arg=$1

# Validate mandatory options and arguments
if [ -z "${s}" ] || [ -z "${p}" ] || [ -z "${arg}" ]; then
    usage
fi

echo "s = ${s}"
echo "p = ${p}"
echo "arg = ${arg}"
```

Ejecutamos el script con `./test.sh -p foo -s bar bazz` y el resultado es:

```shell
s = bar
p = foo
arg = bazz
```

Espero que este consejillo os haga más fácil la escritura de scripts, **enjoy!!**.