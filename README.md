# Scripting
## Articulos de script - Objectivo recordatorio.

### Colores en Bash
```
#Colours
    verdeColor="\e[0;32m\033[1m"
    finColor="\033[0m\e[0m"
    rojoolor="\e[0;31m\033[1m"
    azulColor="\e[0;34m\033[1m"
    amarilloColor="\e[0;33m\033[1m"
    purpuraColor="\e[0;35m\033[1m"
    turquoesaColor="\e[0;36m\033[1m"
    grisColor="\e[0;37m\033[1m"
```
Para ponerlo en práctica : 
```
Ejemplo:
echo -e "\n${rojoColor}[*]${findColor}${grisColor}Esto está en gris ${finColor}"

```
### Configuración en nano
Fichero /root/.nanorc

Ponemos :
  ```
  set tabsize 4 
  set autouindent
  set smooth
  set linenumbers
  ```

Grepeado del nmap {ip} -p- --open -n -T5 -v -oG allPorts - Tambien se puede poner en el .Bashrc com una funcion.

  GNU nano 7.2                                                            allPorts.sh                                                                         
#!/bin/bash

    verde="\e[0;32m\033[1m"
    fin="\033[0m\e[0m"
    rojo="\e[0;31m\033[1m"
    azul="\e[0;34m\033[1m"
    amarillo="\e[0;33m\033[1m"
    purpura="\e[0;35m\033[1m"
    turquoesa="\e[0;36m\033[1m"
    gris="\e[0;37m\033[1m"

    ip=$(cat puertos_router  | grep  -oP ' \d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}' | sort -u)
    open_ports=$(cat $1 | grep -oP '\d{1,5}/open' | awk '{print $1}' FS='/' | xargs | tr ' ' ',')

    echo -e "\n${rojo}[*]${fin} ${gris} Equipo escaneado con nmap : ${fin}"
    echo -e "\t${azul}[*] IP del equipo: ${fin}${gris}$ip${fin}"
    echo -e "\t${azul}[*] Puertos abiertos : ${fin}${gris}$open_ports${fin}\n"
    echo -e "\t${rojo}[*] Copias los puertos en el portapapeles.${fin}\n"
    echo $open_ports | tr -d '\n' | xclip -sel clip
