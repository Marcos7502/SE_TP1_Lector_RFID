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
  
## Descripción
En este trabajo práctico se incorporará un teclado matricial para acceder a la puerta en caso de pérdida de la tarjeta RFID. Para ello, se necesitará:
- Implementar el teclado matricial 
- Implementar un timer para medir el debounce de las teclas
El teclado matricial es del estilo que se muestra debajo:
- https://www.mercadolibre.com.ar/teclado-membrana-matricial-4x4-autoadhesivo-arduino/p/MLA32492378?item_id=MLA1666016868&from=gshop&matt_tool=56318942&matt_word=&matt_source=google&matt_campaign_id=14545592786&matt_ad_group_id=161054711007&matt_match_type=&matt_network=g&matt_device=c&matt_creative=686452904785&matt_keyword=&matt_ad_position=&matt_ad_type=pla&matt_merchant_id=735113679&matt_product_id=MLA32492378-product&matt_product_partition_id=2266488685416&matt_target_id=aud-1928690346655:pla-2266488685416&cq_src=google_ads&cq_cmp=14545592786&cq_net=g&cq_plt=gp&cq_med=pla&gad_source=1&gclid=Cj0KCQjwurS3BhCGARIsADdUH51zF87hFhsJY3J3Xz3nVAZ83l_DVT49zmMAnxrvuYJDPuvP_MFUeoYaAjGUEALw_wcB

Se incluirán funciones de titileo de LEDS para indicar cuando una tarjeta introducida es incorrecta y tambien para indicar cuando una tarjeta fue guardada correctamente. 
Adicionalmente, en este trabajo práctico se propone revisar y rediseñar la interfaz SPI desarrollada en SE_TP1. Enfatizando la modularización en archivos, el buen uso de variables y funciones, la maximización de la cohesion y la minimización del acoplamiento.

Por último, se incorporará un sensor magnético para detectar cuando la puerta esta en el lugar correcto para cerrarla y cuando fue olvidada abierta. Si fue olvidada abierta, en el proximo trabajo práctico se notificará al usario por celular o se hará sonar una alarma.


## Desarrollo
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


     

