# Tarea de autoconfiguración de servidor iscsi y dos clientes.

Aparte de instalar el requerements.txt en nuestro entorno virtual, vagrant necesita unas gemas para winrm:

`sudo gem install -r winrm`

`sudo gem install winrm-elevated`

También usaremos en ansible algunos módulos de la comunidad por lo que instalamos en nuestro entorno virtual de ansible lo siguiente:

`ansible-galaxy collection install community.general`

Una vez se realiza `vagrant up` este creará lo siguiente:

1. Una Máquina Linux (nodo1), que hará de servidor iscsi con dos target a los que conectarse desde los clientes

2. Una Máquina Linux (nodo2), que hára de cliente linux el cual se conectará al target 2, creará los puntos de montaje con systemd y le dara formato a uno de los dispositivos de bloques agregados con iscsi.

4. Una Maquina Windows (nodo3), que hará de cliente windows el cual se conectará al target 1, y agregará esta conexión de forma permanente, por lo cual tendremos un dispositivo de bloque en esta máquina.
