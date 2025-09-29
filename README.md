[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=20745302&assignment_repo_type=AssignmentRepo)
# Lab04: Visualización de Datos en Raspberry Pi con Node-RED 

## Integrantes
Maria Paula Fierro Barrios 

Camilo Suarez Camacho 

Astrid Catalina Ortíz López

## Documentación

En este laboratorio se trata de como implenetar y realizar la conexion de la raspberry pi a Node RED.
Para comenzar, nos conectamos a la Raspberry Pi utilizando una conexión SSH desde la terminal de nuestro computador. Para ello escribimos el comando ssh usuario_raspberry@ip, donde el primer dato corresponde al usuario configurado en la Raspberry y el segundo a la dirección IP asignada en la red local. vez que establecíamos la conexión, el sistema mostró un mensaje de advertencia indicando que no podía verificar la autenticidad del dispositivo. En ese momento escribimos yes para aceptar la clave y, posteriormente, ingresamos la contraseña del usuario. Una vez hecho esto, la terminal cambió al nombre de la Raspberry Pi, confirmando que ya estábamos trabajando directamente en ella.
Después de lograr la conexión, procedimos a instalar Node-RED junto con Node.js y npm. Para esto ejecutamos el comando:

bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)

el cual descarga y corre automáticamente el script oficial de instalación. Durante el proceso, el sistema pidió confirmar dos preguntas: la primera fue si realmente queríamos realizar la instalación, a lo que respondimos con y; y la segunda fue si deseábamos instalar los nodos específicos para la Raspberry Pi, a lo cual también respondimos afirmativamente con y.
Con estas confirmaciones la instalación continuó de forma automática y, tras unos minutos, quedó completada correctamente. Al finalizar, nuestra Raspberry Pi ya tenía disponibles Node.js, npm y Node-RED, listos para ser utilizados en los siguientes pasos del laboratorio.
Para realizar la instalación de Node-RED en la Raspberry Pi, seguimos la recomendación oficial y utilizamos el script que instala automáticamente Node.js, npm y Node-RED. Para ello, ejecutamos en la terminal el comando:

bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)

Al iniciar el proceso, el script hizo varias verificaciones y nos solicitó confirmar algunas acciones. La primera pregunta fue si realmente deseábamos continuar con la instalación, a lo cual respondimos escribiendo y y presionando Enter. Luego, nos preguntó si queríamos instalar los nodos específicos para la Raspberry Pi, y también respondimos afirmativamente.
Después de estas confirmaciones, la instalación comenzó a ejecutarse de manera automática, mostrando en pantalla el progreso de cada paso hasta completar la configuración de Node-RED en la Raspberry Pi.

Durante la instalación, el script actualizó Node.js, instaló Node-RED y configuró los nodos específicos para la Raspberry Pi. El proceso tardó varios minutos y fue necesario esperar sin interrumpir la terminal. Al finalizar, apareció el mensaje “All done.”, seguido de unas preguntas de configuración inicial, donde en la mayoría de los casos bastó con presionar Enter para aceptar las opciones por defecto.

 
Una vez completada la instalación, procedimos a ejecutar Node-RED localmente en la Raspberry Pi utilizando el comando:
node-red-pi --max-old-space-size=256
Este comando permitió iniciar Node-RED optimizado para la Raspberry Pi, limitando el uso de memoria a 256 MB, lo cual resulta útil para evitar un consumo excesivo de recursos. Al finalizar la carga, accedimos a la interfaz gráfica desde un navegador web en el computador, ingresando la dirección http://ip:1880, donde ip corresponde a la dirección de nuestra Raspberry Pi. Allí se mostró la interfaz de Node-RED, confirmando que todo funcionaba correctamente.

Después de interactuar con la interfaz de bienvenida, notamos que al ejecutar Node-RED localmente este ocupa la terminal en primer plano, lo que impide usarla para otros comandos. Además, si la terminal se cierra, el servicio se detiene y ya no es posible acceder a la interfaz web.
Para evitar esto, configuramos Node-RED para que se ejecute automáticamente al iniciar la Raspberry Pi. Como el script de instalación ya había creado el servicio en systemd, solo fue necesario habilitarlo con:
sudo systemctl enable nodered.service
Luego reiniciamos la Raspberry Pi con:
sudo reboot
De esta manera, comprobamos que Node-RED se inicia en cada arranque sin necesidad de ejecutarlo manualmente, pudiendo acceder siempre desde la URL http://ip:1880 mientras la Raspberry Pi esté encendida.

Crear un flujo para un selector de colores
Lo primero que hicimos fue instalar el dashboard de Node-RED desde la interfaz, entrando a Menu > Manage palette > Install, donde busqué dashboard e instalé el paquete. Con eso ya tenía disponibles los nodos necesarios para armar la interfaz gráfica.
Después entramos en la pestaña Dashboard, donde creé una nueva Tab llamada tab1. A esta tab le puse el nombre color y también añadí un Group con el mismo nombre, que fue donde organicé los elementos del flujo.
En el panel de nodos arrastré los siguientes:
color picker
text input
debug
function
file
Luego lo conectamos de tal manera que el color picker me permitiera elegir un color, cuyos valores RGB se mostraban en el text input, se verificaban en el debug, se procesaban en el nodo function y finalmente se guardaban en un archivo a través del nodo file.
Para visualizar el resultado, copié la dirección IP de la Raspberry Pi y le agregué /ui (ejemplo: http://10.221.240.165/ui). Al abrir esta ruta, aparecía la tab1 con el selector de colores, y al probar distintos colores se actualizaban los valores y quedaban almacenados en el archivo.
Además de esto también agregamos a otra dashboard llamada button, con el fin de tener un control adicional desde la misma interfaz. En este botón podía asignar acciones y asociarlas con el flujo.
En el nodo function configuré el mensaje para que se asignara al text input y al nodo file, de modo que los valores capturados se escribieran en un archivo de texto dentro de la Raspberry Pi. La ruta configurada fue:
/home/mac/documents/test.txt
Finalmente, conectamos  desde Windows PowerShell a la Raspberry Pi usando mi usuario y contraseña. Una vez dentro, entré a la carpeta de documentos y con pwd confirmé la ruta. Después utilicé ls para verificar los archivos creados y encontré el archivo test.txt. También observé que dentro de esa carpeta se generó otra carpeta llamada src, en la cual apareció otro archivo text.txt. Con esto comprobé que el flujo funcionaba correctamente, ya que los valores enviados desde la tab1 del dashboard quedaban registrados en la Raspberry.

Dificultades

Una de las principales dificultades que se nos presento es gestionar Node-RED como servicio en segundo plano en la Raspberry Pi.
Al inicio, ejecutar node-red-pi --max-old-space-size=256 funciona, pero mantiene la terminal ocupada y se detiene si cierras sesión SSH. Esto obliga a aprender sobre systemd y cómo habilitar servicios con:

sudo systemctl enable nodered.service
sudo systemctl start nodered.service

Términos técnicos / de código nuevos

- SSH (Secure Shell)
    Protocolo para conectarse remotamente a la Raspberry desde otra máquina. El comando:

    ssh usuario@ip

-   Script de instalación con curl y bash
    Ejemplo:

    bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)

    se aprendio cómo descargar y ejecutar un script remoto en una sola línea.

- systemctl y servicios systemd
    Comandos como:

    sudo systemctl enable nodered.service
    sudo systemctl status nodered.service

    permiten manejar Node-RED como servicio, lo que implica conceptos de arranque automático y demonios en Linux.

- Uso de parámetros en ejecución (--max-old-space-size)
    En: 

    node-red-pi --max-old-space-size=256

    se controla el uso máximo de memoria para Node.js. Esto es un parámetro de optimización que normalmente no se conoce si no trabajas con entornos de recursos limitados (como la Raspberry).
