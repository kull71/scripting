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
Fichero /root/.nanorc en Parrot esta en /etc/nanorc

Ponemos :
  ```
  set tabsize 4 
  set autoindent
  set smooth
  set linenumbers
  ```
# Path Hijchaking

     #include <stdio.h>
         void main() {
         setuid(0);
         printf ("\n\n Listando procesos (/usr/bin/ps)\n\n");
         system("/usr/bin/ps");
         printf("\n\n Listando proceso (ps)\n\n")    ;
        system("ps");
    }

# Chequeadno procesos

    #/bin/bash
        old_proces=$(ps -eo command)
        while true
         do
             new_proces=$(ps -eo command)
             diff <(echo "$old_proces") <(echo "$new_proces") | grep -v "kworker" | g>
             old_proces=$new_proces
          done


### Grepeado del nmap {ip} -p- --open -n -T5 -v -oG allPorts - Tambien se puede poner en el .Bashrc com una funcion.                                    
    
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

# Escaneo de puertos con un script en bash.
    #!/bin/bash
    MAX_PROCESOS=135
    if [ -z "$1" ]; then
    echo "Uso: $0 <IP o dominio>"
        exit 1
    fi
    for i in $(seq 1 65535); do
        Verifica si se alcanzó el número máximo de procesos
        while [ "$(jobs -r | wc -l)" -ge "$MAX_PROCESOS" ]; do
            wait -n
        done
        timeout 1 bash -c "echo > /dev/tcp/$1/$i" 2>/dev/null && echo "[*] Puerto $i: Abierto." &
    done
    
# Descubrir máquinas en tu segmento de red
    #!/bin/bash
        fin="\033[0m\e[0m"
        rojo="\e[0;31m\033[1m"
        for i in $(seq 2 254); do
            # Realiza un ping a cada IP en segundo plano
            timeout 1 bash -c "ping -c 1 192.168.1.$i &>/dev/null" && echo -e "${rojo}[*] Host 192.168.1.$i: Activo ${fin}" &
        done; wait

      

 

