[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=20745302&assignment_repo_type=AssignmentRepo)
# Lab04: Visualización de Datos en Raspberry Pi con Node-RED 

## Integrantes
Maria Paula Fierro Barrios 
Camilo Suarez Camacho 
Astrid Catalina Ortíz López

## Documentación

En este laboratorio se tratade de como implenetar y realizar la conexion de la raspberry pi a Node RED.
Para comenzar, nos conectamos a la Raspberry Pi utilizando una conexión SSH desde la terminal de nuestro computador. Para ello escribimos el comando ssh usuario_raspberry@ip, donde el primer dato corresponde al usuario configurado en la Raspberry y el segundo a la dirección IP asignada en la red local. vez que establecíamos la conexión, el sistema mostró un mensaje de advertencia indicando que no podía verificar la autenticidad del dispositivo. En ese momento escribimos yes para aceptar la clave y, posteriormente, ingresamos la contraseña del usuario. Una vez hecho esto, la terminal cambió al nombre de la Raspberry Pi, confirmando que ya estábamos trabajando directamente en ella.
Después de lograr la conexión, procedimos a instalar Node-RED junto con Node.js y npm. Para esto ejecutamos el comando:

bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)

el cual descarga y corre automáticamente el script oficial de instalación. Durante el proceso, el sistema pidió confirmar dos preguntas: la primera fue si realmente queríamos realizar la instalación, a lo que respondimos con y; y la segunda fue si deseábamos instalar los nodos específicos para la Raspberry Pi, a lo cual también respondimos afirmativamente con y.
Con estas confirmaciones la instalación continuó de forma automática y, tras unos minutos, quedó completada correctamente. Al finalizar, nuestra Raspberry Pi ya tenía disponibles Node.js, npm y Node-RED, listos para ser utilizados en los siguientes pasos del laboratorio.
Para realizar la instalación de Node-RED en la Raspberry Pi, seguimos la recomendación oficial y utilizamos el script que instala automáticamente Node.js, npm y Node-RED. Para ello, ejecutamos en la terminal el comando:

bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)

Al iniciar el proceso, el script hizo varias verificaciones y nos solicitó confirmar algunas acciones. La primera pregunta fue si realmente deseábamos continuar con la instalación, a lo cual respondimos escribiendo y y presionando Enter. Luego, nos preguntó si queríamos instalar los nodos específicos para la Raspberry Pi, y también respondimos afirmativamente.
Después de estas confirmaciones, la instalación comenzó a ejecutarse de manera automática, mostrando en pantalla el progreso de cada paso hasta completar la configuración de Node-RED en la Raspberry Pi.


<!-- Incluir diagramas y adjuntar al repositorio, en una carpeta src, el flujo que crearon -->


## Conclusiones
