# Trabajo Práctico 0 - Taller de Programación I - (75.42/95.08)
# Informe


**Nombre:**  Escobar Benitez Maria Soledad

**Padrón:**  97877

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
- *--show-reachable:* se utiliza para reportar fugas de memoria, incluso las
        que al terminar la ejecucion el sistema operativo se encarga 
        de arreglar.
- *--track-origins:* esta opción nos sirve para recibir un reporte acerca de
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
- |2|x|x|x| => se puede observar que quedan bytes desperdiciados, por lo que el 
- |0|0|0|3| sizeof() de mi estructura devolvería 12, si sumamos los tamaños 
            sizeof(int) + sizeof(char) + sizeof(int) = 4+1+4 = 9 
            vemos que no coinciden.


5. **Investigar la existencia de los archivos estándar: STDIN, STDOUT, STDERR.
Explicar brevemente su uso y cómo redirigirlos en caso de ser necesario 
(caracteres > y ​ <) y como conectar la salida estándar de un proceso a la 
entrada estándar de otro con un pipe​ (carácter |​).**

Los archivos estándar **STDIN, STDOUT, STDERR** son descriptores o canales 
que uiliza el sistema operativo para conectar la entrada, salida e informe de
errores de un programa con la terminal cuando se está ejecutando.
- *STDIN:* refiere a la entrada estándar, es decir, a los datos que se envian al
programa, por ejemplo los parámetros que se ingresan al realizar una llamada al
programa o al enviarle un archivo de entrada.
- *STDOUT:* refiere a la salida estándar, es decir, a los datos que devuelve el 
programa durante el período de ejecición.
- *STDERR:* refiere a la salida de errores, es decir, a los errores que han ido 
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
ejecutable localmente sí se reportan warnings, esos warnigs
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
		por último se elimina un espacio innecesario entre la variable
        next_state y el *;*.
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

1. **Describa en breves palabras las correcciones realizadas respecto de la 
versión anterior.**
- **paso3_wordscounter.c:** en este archivo se incluye la biblioteca 
		<stdlib.h>, la cual no estaba incluida en las versiones anteriores.
- **paso3_wordscounter.h:** aquí se incluyen 2 bibliotecas, <string.h> y
		<stdio.h>, las cuales no estaban incluidas en las versiones anteriores 
		de este archivo.
- **paso3_main.c:** no presenta nuevos cambios con respecto a las versiones
		anteriores.
		
2. **Captura de pantalla indicando los errores de generación del ejecutable.** 
**Explicar cada uno e indicar si se trata de errores del compilador o del linker.**

![Paso3](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso3/paso3.png)

Podemos observar de la existencia de un único error correspondiente al
archivo *paso3_main.c*, en la línea número 27, *undefined reference to 
'wordscounter_destroy'*, este error nos indica que tenemos una referencia no
definida, esto tiene que ver con el hecho de que si bien la función 
*wordscounter_destroy*, está declarada en el archivo *paso3_wordscounter.h*,
el cual estamos incluyendo, la función no se encuentra definida ni en 
*paso3_wordscounter.h* o *paso3_wordscounter.c*, por lo que se genera un error
del linker, ya que al buscar el código de esta función para enlazarlo y generar
el ejecutable el linker no logra encontrarlo.

## Paso 4: SERCOM - ​ Memory Leaks y ​ Buffer Overflows

1. **Describa en breves palabras las correcciones realizadas respecto de la 
versión anterior.**

La única correción detectada es la que se realizó en el archivo 
*paso3_wordscounter.c*, donde se define la función *wordscounter_destroy*, esto
hace que el linker no arroje ningun error, aunque no se le proporciona ninguna
funcionalidad a la función.

2. **Captura de pantalla del resultado de ejecución con Valgrind​ de la prueba 
‘TDA’. Describir los errores reportados por Valgrind.**

![Paso4_1](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso4/paso_4_0.png)

![Paso4_2](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso4/paso_4_1.png)

![Paso4_3](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso4/paso_4_2.png)

- **paso4_main.c:** En la línea 14 indica que hay 472 bytes sin liberar, a
		los cuales no se le pierde referencia durante la ejecución, esto sucede
		porque en esa línea se llama a la función *fopen* pero luego nunca se 
		cierra el archivo llamando a *fclose*.
- **paso4_main.c:** En la línea 24 indica que se perdieron 1,505 bytes en 
		215 bloques, esto pasa porque al llamar función *wordscounter_process*,
		que se encuentra en *paso4_wordscounter.c*, la cual a su vez llama a 
		*wordscounter_next_state*, la cual pide memoria a través de *malloc* 
		pero luego esa memoria no es liberada y al salir de la función de pierde
		su referencia, como durante la ejecución de *wordscounter_process* se 
		hacen varios llamados a esta función esto sucede en 215 veces.
		
3. **Captura de pantalla del resultado de ejecución con Valgrind​ de la prueba
‘Long Filename’. Describir los errores reportados por Valgrind.**

![Paso4_4](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso4/paso_4_3.png)

![Paso4_5](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso4/paso_4_4.png)

Este error indica que se produce un buffer overflow, esto sucede en el archivo 
*paso4_main.c*, línea 13, donde se realiza un llamado a la función *memcpy* a 
la cual se le pasa un buffer, luego se le pasa un texto el cual, será copiado 
dentro del buffer, y el tamaño del texto, lo que sucede aquí es que esta 
función no controla el tamaño de bytes que tiene el texto, por lo que al pasar
un texto de tamaño mayor al tamaño del buffer, el buffer se desborda y se 
empieza a copiar en la memoria vecina al buffer.

4. **¿Podría solucionarse este error utilizando la función strncpy​?
¿Qué hubiera ocurrido con la ejecución de la prueba?**

Si utilizaramos la función  *strncpy* el problema no será solucionado ya que 
se copiaran los n bytes que le indiquemos, así sea mayor al tamaño del buffer,
a no ser que se encuentre con un '\0' dentro de los bytes a copiar, lo cual es 
la unica diferencia que tiene con *memcpy*, ya que esta copia la cantidad de
 bytes que nosotros le hayamos especificado, sin detectar si hay caracteres
 nulos o fin de string dentro de los mismos. 


5. **Explicar de qué se trata un ​ segmentation fault​ y un ​ buffer overflow​.**

**Segmentation Fault** es un error que se da cuanto se intenta acceder a lugares
de memoria a los cuales no tenemos permitido. Por ejemplo, cuando se intenta
escribir o modificar valores dentro del code segment.

**Buffer overflow** es un error que se da cuando reservamos cierta cantidad de 
memoria en un buffer y luego a la hora de utilizarlo superamos el tamaño de la
memoria reservada y comenzamos a escribir en memoria que no teníamos asignada 
para ese proposito.

## Paso 5: SERCOM - Código de retorno y salida estándar

1. **Describa en breves palabras las correcciones realizadas respecto de la 
versión anterior.**
	
- **paso5_main.c:** se elimina el buffer y la función memcpy que generaba un
	error en el paso anterior, ya que se copiaba la ruta del archivo en el 
	buffer y este se desbordaba, ahora directamente se pasa la ruta del archivo
	a la función *fopen*, sin necesidad de pasos intermedios, además se coloca 
	una condición para verificar el fin  del archivo y así llamar a *fclose* 
	para cerrarlo.
- **paso5_wordscounter.c:** se elimina el llamado a la función *malloc* que se 
	usaba para pedir memoria en la cual almacenar los caracteres delimitadores,
	esto soluciona el problema de pérdida de memoria causada por no liberar la
	memoria reservada con la función *malloc*, en cambio se utiliza una
	constante que representa un arreglo de los caracteres delimitadores.

2. **Describa el motivo por el que fallan las prueba ‘Invalid File’ y ‘Single
Word’. ¿Qué información entrega SERCOM para identificar el error? Realice una
captura de pantalla.**

![Paso5_1](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso5/paso5.png)

- **Invalid File(archivo_invalido):** esta prueba falla porque el sistema espera que se retorne un
	1 cuando ocurra un error durante la ejecución del programa, en este caso el
	error es que el archivo no es válido y el valor de retorno especificado en 
	*paso5_main.c* es ERROR que vale -1. Por este motivo el Sercom indica que 
    se esperaba terminar con un código de retorno 1 pero se obtuvo 255, que 
    corresponde al valor -1.
- **Single Word(una_palabra):** esta prueba falla porque la salida estándar no coincide con 
	lo esperado, esto es lo que indica el Sercom. Esto se debe a que el archivo
	finaliza luego del último caracter de la palabra *word*, entonces como antes
	de que el programa chequee si se acabó la palabra se chequea el fin del 
	archivo, la funció finaliza sin actualizar el contador, es por eso que se
	devuelve un 0, en lugar de un 1, haciendo que los resultados no coincidan.

3. **Captura de pantalla de la ejecución del comando hexdump​. 
¿Cuál es el último carácter del archivo input_single_word.txt?**

![Paso5_2](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso5/paso_5_0.png)

El último caracter del archivo es el valor hexadecimal *64*, que corresponde a 
la letra *d*.

4. **Captura de pantalla con el resultado de la ejecución con gdb​.
Explique brevemente los comandos utilizados en gdb​. ¿Por qué motivo el debugger
no se detuvo en el breakpoint de la línea 45: self->words++;?**

![Paso5_3](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso5/paso_5_1.png)

![Paso5_4](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso5/paso_5_2.png)

![Paso5_5](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso5/paso_5_3.png)

![Paso5_6](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso5/paso_5_4.png)

- **info functions:** lista las funciones propias que se utilizan dentro del 
	programa indicando los tipos de los parámetros que reciben.
- **list wordscounter_next_state:** nos muestra las lineas que rodean a la
	función que le indicamos, por default se muestran 10 lineas, en este caso se
	muestran las 5 lineas por encima y por debajo de la definición de la misma:
```C
	    int c = getc(text_file);
        state = wordscounter_next_state(self, state, c);
    } while (state != STATE_FINISHED);
}

static char wordscounter_next_state(wordscounter_t *self, char state, char c) {
    const char* delim_words = " ,.;:\n";

    char next_state = state;
    if (c == EOF) {
```
- **list:** nos muestra las 10 líneas que están a continuación de las últimas 
	líneas impresas:
```C
        next_state = STATE_FINISHED;
    } else if (state == STATE_WAITING_WORD) {
        if (strchr(delim_words, c) == NULL)
            next_state = STATE_IN_WORD;
    } else if (state == STATE_IN_WORD) {
        if (strchr(delim_words, c) != NULL) {
            self->words++;
            next_state = STATE_WAITING_WORD;
        }
    }
```
- **break 45:** este comando indica que cuando el programa esté en ejecución el
	mismo se detenga en esa línea, la 45.
- **run:** este comando se utiliza para iniciar la ejecución del programa.
- **¿Por qué motivo el debugger no se detuvo en el breakpoint de la línea 45: 
self->words++;?**


Durante la ejecución del programa, el debugger no se detuvo en el breakpoint de 
la línea 45: self->words++; porque nunca llega a ejecutar esas líneas, lo que 
sucede es que al chequear en *end of file* en la línea 38, se da como finalizado
el conteo y directamente se salta a la línea 49. Esto se puede observar en el 
código citado a continuación.

```C
34	static char wordscounter_next_state(wordscounter_t *self, char state, char c) {
35	    const char* delim_words = " ,.;:\n";
36
37	    char next_state = state;
38	    if (c == EOF) {
39	        next_state = STATE_FINISHED;
40	    } else if (state == STATE_WAITING_WORD) {
41	        if (strchr(delim_words, c) == NULL)
42	            next_state = STATE_IN_WORD;
43	    } else if (state == STATE_IN_WORD) {
44	        if (strchr(delim_words, c) != NULL) {
45	            self->words++;
46	            next_state = STATE_WAITING_WORD;
47	        }
48	    }
49		 return next_state;
50	}
```

## Paso 6: SERCOM - Entrega exitosa


1. **Describa en breves palabras las correcciones realizadas respecto de la
versión anterior.**

- **paso6_main.c:** en esta fución se cambia la definición de la constante ERROR
	de un -1 a un 1, esto soluciona el error de la prueba *Invalid File*.
- **paso6_wordscounter.c:** aquí se cambia la definición de delim_words que pasa
	de ser una constante local de la función *wordscounter_next_state*, y se 
	define como una constante simbolica. Además se realiza un cambio a la hora 
	de chequear el estado del counter, es decir se chequea primero si este 
	debe ser incrementado y luego se chequea si se llegó al final del archivo,
	este cambio soluciona el problema de la prueba *Single Word*, ya que el
	contador se actualizará a 1 antes de finalizar la ejecución del programa.
	
2. **Captura de pantalla mostrando todas las entregas realizadas​ , tanto exitosas
como fallidas.**

![Paso6_1](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso6/paso_6_0.png)

![Paso6_2](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso6/paso_6_2.png)

3. **Captura de pantalla mostrando la ejecución de la prueba ‘Single Word’
de forma local​ con las distintas variantes indicadas.**

![Paso6_3](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso6/paso_6_1.png)

## Paso 7: SERCOM - Revisión de la entrega

1. **Revisar el estado de todas las pruebas ejecutadas en SERCOM con el código del
paso 6.**

Se corroboró que todas las pruebas ejecutadas por el Sercom cumplen con la
salida esperada.

2. **Abrir cada una de las salidas de Valgrind​ y controlar que no hay errores 
reportados que no fueran detectados como un fallo en la ejecución. Revisar con
atención el listado de archivos abiertos al finalizar el programa.**

No se han reportado errores con valgrind que el Sercom no haya detectado.

3. **Controlar el código final entregado. Verificar el uso de buenas prácticas de
programación y el cumplimiento del enunciado del trabajo.**


