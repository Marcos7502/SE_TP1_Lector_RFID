# SE_TP2_Teclado_Matricial
Trabajo practico número 2 de la materia Sistemas Embebidos de la FIUBA

Título: Smartlock

Alumno: Marcos Gómez Villafañe

Padrón: 105055

Objetivo Final: Desarrollar una cerradura inteligente que permita acceder con tarjeta y, en caso de visita sin tarjeta, permita hablar por telefono con la visita.

Los temas a incorporar para este trabajo práctico son:
- Máquina de estado finito
- Reloj de tiempo real 
- Modularización en archivos
- Buen uso de variables y funciones públicas y privadas 
- Diseño con bajo acoplamiento y alta cohesión 
- Displays alfanuméricos y gráficos
- Interfaces I2C y SPI
- Capas de abstracción de hardware y software
  
## Descripcion
En este trabajo práctico se incorporará el uso de un teclado matricial para acceder a la puerta en caso de pérdida del lector RFID.

## Desarrollo:
A continuación, se describe el contenido de este Trabajo Práctico:
1) Se realiza el esquemático con las conexiones en TP1_SE_esquematico. Éste se define a partir de las especificaciones y de la hoja de datos en https://os.mbed.com/platforms/ST-Nucleo-F429ZI/
2) Con el esquemático, se definen los pines a utilizar para el código en global_definitions
3) Se hace uso de:
   - Una comunicación UART con la computadora
   - Una comuniación SPI con el lector RFID
   - Un timer para contar el tiempo en que la puerta permanece abierta

4) La lógica del codigo es la siguiente:
   - Si se acerca una tarjeta nueva preguntar si se desea guardarla
   - Si se desea guardar, se escribe en la memoria de la NUCLEO el ID leido de la tarjeta
   - Si no se desea guardar, no se escribe nada en la memoria
   - Si el ID de la tarjeta leida es igual al ID guardado, se abre la puerta y se inicializa un timer
   - Si el tiempo del timer es mayor a 10 segundos,se cierra la puerta
   - En todo el proceso, si se presiona el botón para cerrar la puerta se cierra la puerta

![Estados TP1](https://github.com/user-attachments/assets/62f4d531-08d9-4f3d-b6ac-242f25beefea)

## Bugs
1) Algunas de las condiciones de if del puntero rfid_content no funcionan correctamente y por eso no se escriben los mensajes en la computadora.

## Resultado
El siguiente video muestra que el ID de la tarjeta fue leído y guardado por el sistema. Al acercar la tarjeta nuevamente, se prende el led verde indicando que abrió la puerta.

https://github.com/user-attachments/assets/06ab2fae-fa66-4fb5-a746-cb7c03a149e0


     

