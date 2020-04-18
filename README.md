### muralla

Es un proyecto desarrollado con el lenguaje de programación python que pretende 
facilitar la gestión de un firewall construido por _Iptables_ como sistema base.

El programa está totalmente abierto, se puede leer el código fuente sin problemas.

<a href="https://wiki.nuxpy.com/index.php/Muralla">Sitio oficial del proyecto.</a>

### Instalación y dependencia

En primera instancia tener instalado el programa: **man-db**

El contenido debería tener un árbol de archivos parecido al siguiente:

    muralla
       ├── etc
       │   ├── muralla
       │   │   └── muralla.conf
       │   ├── network
       │   │   └── if-up.d
       │   │       └── muralla-up
       │   └── sysconfig
       │       └── network-scripts
       │           └── muralla-up
       ├── install
       ├── README.txt
       └── usr
           ├── sbin
           │   └── muralla
           └── share
               └── man
                   ├── es
                   │   ├── man5
                   │   │   └── muralla.conf.5.gz
                   │   └── man8
                   │       └── muralla.8.gz
                   ├── man5
                   │   └── muralla.conf.5.gz
                   └── man8
                       └── muralla.8.gz

Se instala como usuario **root** de la siguiente manera:

    ./install

### Fichero muralla.conf

La ruta absoluta del archivo de configuración es: **/etc/muralla/muralla.conf**

El contenido del archivo muralla.conf es parecido al formato de archivos _Json_, 
internamente la estructura aceptará comandos y parámetros relacionados con los 
comandos y parámetros de _Iptables_.

### Ejemplos

Declarando una política permisiva con negación de respuesta de ping:

    {
       "policy": {
           "input": "accept",
           "forward": "accept",
           "output": "accept"
       },
       "input_accept": [
           {"ip_src": "127.0.0.1", "ip_dst": "127.0.0.1"}
       ],
       "input_drop": [
           {"proto": "icmp --icmp-type echo-request"}
       ]

    }

Ejemplo base del archivo de configuración:

    {
        "policy": {
            "input": "DROP",
            "forward": "drop",
            "output": "accept"
        },
        "input_accept": [
            { "ip_src": "127.0.0.1", "ip_dst": "127.0.0.1" },
            { "port_dst": 22, 'proto': "tcp" },
            { "port_dst": 80, 'proto': 'tcp' },
            { "port_dst": 443, 'proto': 'tcp' },
            { "state": "new, established, related" }
        ],
        "input_drop": [
            { "port_dst": 25, 'proto': 'tcp' },
            { "port_dst": 21, 'proto': 'tcp' },
            { "port_dst": 23, 'proto': 'tcp' },
            { "port_dst": 25, 'proto': 'udp' }
        ]
    }

Ejemplo rechazando conexiones de HTTP:

    {
        "policy": {
            "input": "drop",
            "forward": "drop",
            "output": "accept"
        },
        "input_drop": [
            {"port_dst": "http", "proto": "tcp", "ip_src": "192.168.1.0/24"}
        ],
        "input_accept": [
            {"ip_src": "127.0.0.1", "ip_dst": "127.0.0.1"},
            {"state": "new, established, related"}
        ]

    }

### Fichero muralla

La ruta absoluta del archivo es: **/usr/local/sbin/muralla**

Este archivo es el script principal desde donde se lee el archivo de configuración, 
se listan las reglas implementadas, se cargan y eliminan reglas y se ve la ayuda 
del mismo, también se desinstala el programa. 

    muralla -l      # Listar las reglas
    muralla -c      # Cargar las reglas
    muralla -d      # Eliminar las reglas
    muralla -h      # Muestra esta ayuda
    muralla -u      # Elimina el programa del sistema

### Fichero muralla-up

La ruta absoluta de este archivo depende de la distribución Linux.

Para familia _Debian_: **/etc/network/if-up.d/muralla-up**

Para familia _Red Hat_: **/etc/sysconfig/network-scripts/muralla-up**

La intención de este archivo es cargar las reglas que están definidas en el 
archivo _muralla.conf_ durante el arranque del sistema operativo.

### Deinstalación

La desinstalación se realizan como usuario **root** y con el mismo comando base:

    muralla -u

### Autor
Félix Urbina
