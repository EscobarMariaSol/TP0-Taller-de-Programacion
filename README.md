# Trabajo Práctico 0 - Taller de Programación  - (75.42/95.08)
# Informe

**Padrón:**  97877

**Nombre:**  Escobar Benitez Maria Soledad

**Repositorio:** [Link GitHub!](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion)

**Fecha de entrega:** 06/10/2020

## Paso 0: Entorno de trabajo

1. Capturas de pantalla de la ejecución del aplicativo.
![Paso0](https://github.com/EscobarMariaSol/TP0-Taller-de-Programacion/blob/master/img/paso0/paso0.png)

2. ¿Para qué sirve ​ Valgrind​? ¿Cuáles son sus opciones más comunes?

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
	
3. ¿Qué representa ​ sizeof()​?¿Cuál sería el valor de salida de sizeof(char)​ 
y ​sizeof(int)​?

El operador sizeof()​ devuelve el tamaño, en bytes, que un tipo de dato, el cual 
le pasamos por parámetro, ocupa en memoria.
El tamaño de un char es de 1 byte, por lo que la salida de ​sizeof(char) debe 
ser igual a 1, por otro lado el tamaño de un int depende de la arquitectura 
específica de la máquina que estemos utilizando, por lo que si estamos en una 
arquitectura de 32 bits sizeof(int) es 4, pero si estamos en 64 bits el valor de
sizeof(int) puede ser de 4 u 8 bytes, lo que sí es seguro es que siempre serán 
multiplos de 4.


4. ¿El ​sizeof()​ de una struct de C es igual a la suma del sizeof()​ de cada 
uno sus elementos? Justifique mediante un ejemplo.

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
|0|0|0|1|
|2|-|-|-| => se puede observar que quedan bytes desperdiciados, por lo que el 
|0|0|0|3|   sizeof() de mi estructura devolvería 12, si sumamos los tamaños 
sizeof(int) + sizeof(char) + sizeof(int) = 4+1+4 = 9 vemos que no coinciden.


5. Investigar la existencia de los archivos estándar: STDIN, STDOUT, STDERR. 
Explicar brevemente su uso y cómo redirigirlos en caso de ser necesario 
(caracteres > y ​ <) y como conectar la salida estándar de un proceso a la 
entrada estándar de otro con un pipe​ (carácter |​).

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
