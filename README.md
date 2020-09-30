# Trabajo Práctico 0 - Taller de Programación I - (75.42/95.08)
# Informe

**Padrón:**  97877

**Nombre:**  Escobar Benitez Maria Soledad

**Repositorio:** [Link GitHub!](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion)

**Fecha de entrega:** 06/10/2020

## Paso 0: Entorno de trabajo

1. **Capturas de pantalla de la ejecución del aplicativo.**
![Paso0](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso0/paso0.png)

2. **¿Para qué sirve ​ Valgrind​? ¿Cuáles son sus opciones más comunes?**

Valgrind es una herramienta que se utiliza para detectar y reportar errores en 
nuestros programas, relacionados al uso de memoria, como puede ser la pérdida 
de memoria, el uso de memoria que no corresponde a nuestro programa, memoria 
que no ha sido inicializada, memoria mal liberada, etc. 
Valgrind utiliza por defecto la herramienta llamada *memcheck*, esta 
herramienta reporta un tipo de error específico de acuerdo a los problemas que 
vaya detectando durante la ejecución del programa. Además se le puede indicar 
ciertas opciones específicas de acuerdo a lo que nos interesa detectar, como 
por ejemplo:
	- *--leak-check:* buscará y reportará escapes de memoria. Si le asignamos la 
		opción --leak-check=summary informará sobre la cantidad de escapes
		detectados, se le pueden asignar otras opciones como yes/no, para 
		habilitar y deshabilitar, y full, para un reporte más detallado.
	- *--undef-value-errors:* reportará los errores asociados a valores no 
		definidos. Se puede asignar --undef-value-errors=yes o 
		--undef-value-errors=no para habilitar o deshabilitar esta opción.
    - *--show-reachable: se utiliza para reportar fugas de memoria, incluso las
        que al terminar la ejecucion el sistema operativo se encarga 
        de arreglar.
    - *--track-origins: esta opción nos sirve para recibir un reporte acerca de
        donde se están originando los valores no inicializados, de haberlos.
	
3. **¿Qué representa ​ sizeof()​?¿Cuál sería el valor de salida de sizeof(char)​ 
y ​sizeof(int)​?**

El operador sizeof()​ devuelve el tamaño, en bytes, que un tipo de dato, el cual 
le pasamos por parámetro, ocupa en memoria.
El tamaño de un char es de 1 byte, por lo que la salida de ​sizeof(char) debe 
ser igual a 1, por otro lado el tamaño de un int depende de la arquitectura 
específica de la máquina que estemos utilizando, por lo que si estamos en una 
arquitectura de 32 bits sizeof(int) es 4, pero si estamos en 64 bits el valor de
sizeof(int) puede ser de 4 u 8 bytes, lo que sí es seguro es que siempre serán 
multiplos de 4.


4. **¿El ​sizeof()​ de una struct de C es igual a la suma del sizeof()​ de cada 
uno sus elementos? Justifique mediante un ejemplo.**

En el caso de una struct hemos visto en clase que podemos encontrarnos con 
espacio desperdiciado dentro de ella, ya que los datos se alinean en posiciones
múltiplos de 4 para lograr acceder a los elementos de manera más eficiente, 
al ocurrir esto nos podemos encontrar con que la suma del sizeof() de cada uno 
de los elementos no necesariamente coincide con el sizeof() del struct, 
veamos el siguiente ejemplo:
```C
	struct Ej {
		int a;
		char b;
		int c;
	};
	
	//Si defino los valores de mi struct
	struct Ej ejemplo = {1,2,3};
```
Supongamos que estamos en una arquitectura donde el tamaño de un int es de 
4 bytes, la estructura queda almacenada como:
- |0|0|0|1|
- |2|-|-|-| => se puede observar que quedan bytes desperdiciados, por lo que el 
- |0|0|0|3|   sizeof() de mi estructura devolvería 12, si sumamos los tamaños 
sizeof(int) + sizeof(char) + sizeof(int) = 4+1+4 = 9 vemos que no coinciden.


5. **Investigar la existencia de los archivos estándar: STDIN, STDOUT, STDERR.
Explicar brevemente su uso y cómo redirigirlos en caso de ser necesario 
(caracteres > y ​ <) y como conectar la salida estándar de un proceso a la 
entrada estándar de otro con un pipe​ (carácter |​).**

Los archivos estándar **STDIN, STDOUT, STDERR** son descriptores o canales 
que uiliza el sistema operativo para conectar la entrada, salida e informe de
errores de un programa con la terminal cuando se está ejecutando.
*STDIN:* refiere a la entrada estándar, es decir, a los datos que se envian al
programa, por ejemplo los parámetros que se ingresan al realizar una llamada al
programa o al enviarle un archivo de entrada.
*STDOUT:* refiere a la salida estándar, es decir, a los datos que devuelve el 
programa durante el período de ejecición.
*STDERR:* refiere a la salida de errores, es decir, a los errores que han ido 
registrando a lo largo de la ejecución de un programa.
La información recolectada por de STDOUT y STDERR se pueden redirigir a un 
archivo específico utilizando el caracter **>**, por ejemplo, 
*./tp > mi_archivo.txt* para la salida estándar, y *./tp 2> mis_errores.txt* 
para la salida de errores.
También se puede redirigir la entrada estándar de un programa utilizando el
 caracter **<**, por ejemplo, *./tp < archivo_entrada.txt*. 
A su vez se puede combinar el uso de estos caracteres, se puede hacer de la 
siguiente manera, *./tp < archivo_entrada.txt > mi_archivo.txt*,redirigiendo 
de esta manera la entrada y salida a la vez o incluso 
*./tp < archivo_entrada.txt 2> mi_archivo.txt* para redirigir la entrada y la 
salida de errores.
La salida estándar de un proceso se puede conectar a la entrada estándar de otro
proceso mediante el caracter *|*, esto permite que los valores devueltos por un 
programa se puedan utilizar como entrada para otro programa. Un ejemplo de como 
hacer esto sería ejecutando el siguiente comando *prog_entrada | prog_salida*, 
donde prog_salida utiliza como entrada los datos devuletos por prog_entrada.

## Paso 1: SERCOM - Errores de generación y normas de programación


1. **Capturas de pantalla mostrando los problemas de estilo detectados. 
Explicar cada uno.**
![Paso1_1](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso1/paso_1_1.png)
- **Archivo paso1_wordscounter.c**
	- Línea 27: indica que falta un espacio para separar la clausula de flujo 
		*while* de la condición encerrada entre paréntesis.
	- Línea 41: indica que hay un espacio innecesario dentro del parentesis de 
		la condición del *if*.
	- Línea 47: indica que un *else if* debe aparecer en la misma linea de la 
		llave que lo precede, es decir, en la linea 46, y que además si un 
		*else* tiene una llave a un lado debe tenerlo de ambos lados.
	- Línea 48: indica que debe haber un espacio entre la sentencia *if* y el 
		paréntesis que encierra la condición.
	- Línea 53: indica que hay un espacio innecesario entre la variable 
		*next_state* y el *;*.
	- Línea 14: si bien el Sercom no indica la existencia de un error, en esta 
		linea no se cumple con las normas básicas de codificación al abrir una 
		llave en una nueva línea, la misma debería estar en la línea 13.
- **Archivo paso1_main.c**
	- Línea 12: indica que siempre es preferible usar la función *snprintf* en 
		lugar de *strcpy*, ya que a la misma le especifico la cantidad de bytes 
		que voy a escribir y no va a permitir que escriba más que esa cantidad, 
		sin embargo con *strcpy* puedo escribir y superar el tamaño que se 
		espera y pisar otros datos.
	- Línea 15: aca nos indica nuevamente que un *else* debe aparecer en la 
		misma línea que la llave que lo precede y que además el mismo debe tener
		llaves de ambos lados.
- **Archivo paso1_wordscounter.h**
	- Línea 5: indica que las líneas no deben tener más de 80 caracteres ya que 
	en esta linea tenemos un comentario con 82 caracteres.
Si bien Sercom no emitió errores sobre los nombres de funciones, en las reglas 
básicas de codificación se señala que las funciones y métodos deben nombrarse
utilizando camelCase como separador de palabras, como también PascalCase para
las clases y tipos, lo cual no se cumple en ninguno de estos archivos.

2. **Captura de pantalla indicando los errores de generación del ejecutable. 
Explicar cada uno e indicar si se trata de errores del compilador o del linker.**
![Paso1_2](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso1/paso_1_0.png)
	
- **Archivo paso1_main.c**
	- Línea 22: el error indica que no se conoce el tipo *wordscounter_t* ya
		que el mismo no está declarado dentro del archivo paso1_main.c, este 
		error corresponde a un error de compilación.
	- Líneas 23, 24,25 y 27: todas corresponden a un error de compilación, ya 
		que no se han declarado las funciones  *wordscounter_create, 
		wordscounter_process, wordscounter_get_words y wordscounter_destroy*, y
		el compilador no sabe como resolver esas referencias.

3. **¿El sistema reportó algún WARNING? ¿Por qué?**

El Sercom no reporta ningún warning, sin embargo al intentar compilar y crear el 
ejecutable desde la terminal sí se reportan warnings, esos warnigs
en el Sercom se han reportado como errores, esto sucede por los flags utilizados
a la hora de compilar ya que el Sercom utiliza flags para el tratamiento de 
warnigs, en particular los flags *-pedantic-errors* y *-Werror* hacen que los
warnings se reporten como errores. 
Los warnigs detectados son los siguientes:
![Paso1_3](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso1/paso_1_2.png)
Se puede observar que algunos corresponden a los mencionados en items 
anteriores, pero hay también ciertos errores que no aparecían anteriormente.
	- **paso1_wordscounter.c:31:** en esta linea nos indica una declaración 
		implicita de la función *malloc* y además nos sugiere incluir la
		biblioteca <stdlib.h> o proveer una declaración de la función dentro
		de nuestro archivo. Esto sucede porque a la hora de compilar el archivo
		el compilador no encuentra la función dentro del mismo o una declaración
		que le asegure que esa función está definida en algún otro archivo.
	- **paso1_wordscounter.h:7, 20, 25:** nos reporta un error de tipos 
		desconocidos, ya que no se conocen los tipos *size_t y FILE*.

## Paso 2: SERCOM - Errores de generación 2


1. **Describa en breves palabras​ las correcciones realizadas respecto de la versión
anterior. Luego de Verificar los cambios realizados respecto de la entrega 
anterior utilizando el comando diff:**

*diff paso1_main.c paso2_main.c || diff paso1_wordscounter.c paso2_wordscounter.c*
*|| diff paso1_wordscounter.h paso2_wordscounter.h*

Las correcciones realizadas en los archivos están relacionadas a los errores 
asociados a las normas básicas de codificación.
	- **diff paso1_main.c paso2_main.c:** Se incluye el archivo
		*paso2_wordscounter.h*, se reemplaza la función *strcpy* por la función
		*memcpy*, y por último se coloca la sentencia *else* en la misma línea 
		que la llave que lo precede.
	- **diff paso1_wordscounter.c paso2_wordscounter.c:** Se incluye el archivo
		*paso2_wordscounter.h*, se agrega un espacio entre la sentencia *while*
		y el paréntesis que encierra la condición, se elimina un espacio 
		innecesario dentro del paréntesis que encierra la condición de un *if*,
		se coloca un *else if* en la misma línea que la llave que lo precede y 
		por último se elimina un espacio innecesario entre una variable y el *;*.
	- **diff paso1_wordscounter.h paso2_wordscounter.h:** se reduce la longitud
		del comentario que superaba los 80 caracteres.
		
2. **Captura de pantalla indicando la correcta ejecución de verificación de normas
de programación.**
![Paso2_1](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso2/paso_2_2.png)

3. **Captura de pantalla indicando los errores de generación del ejecutable. 
Explicar cada uno e indicar si se trata de errores del compilador o del linker.**
![Paso2_2](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso2/paso_2_0.png)
![paso2_3](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso2/paso_2_1.png)
	- **paso2_wordscounter.h:7 y 20:** error de tipo desconocido, esto es porque
		el tipo *size_t* no fue declarado dentro del archivo, vemos además que 
        el compilador nos sugiere incluir la librería <stddef.h>, ya que en 
        ella se provee una declaración del tipo de dato *size_t*, indicandonos
        cómo y dónde hacerlo, este error corresponde a un error de compilación.
	- **paso2_wordscounter.h:25:** nuevamente se trata de un error de tipo
		desconocido, ya que el tipo *FILE* no fue declarado dentro del archivo,
		y corresponde a un error de compilación.
	- **paso2_wordscounter.c:17:** aquí se produce un error debido al error del
		tipo *size_t*, ya que *wordscounter_get_words* devuelve un valor de tipo
		*size_t*, como el compilador no conoce este tipo se produce el error.
	- **paso2_wordscounter.h:20:** es un mensaje de error indicando donde fue 
		declarada la función *wordscounter_get_words*, el cual se debe al error
		mencionado anteriormente y corresponde a un error de compilación.
	- **paso2_wordscounter.c:30:** este error indica una declaración 
		implicita de la función *malloc*, que devuelve punteros, 
        ya que la misma no está declarada de esa manera pues existe una
        una declaración default (built-in) que devuelve int, por lo que al 
        intentar usar la que devuelve punteros se entra en conflicto. Como GCC
		conoce de la existencia de este problema nos sugiere incluir la 
        biblioteca <stdlib.h> la cual provee una declaración de la función
        malloc que realmente se quiere usar. Este error también corresponde a 
        un error de compilación.

## Paso 3: SERCOM - Errores de generación 3
		