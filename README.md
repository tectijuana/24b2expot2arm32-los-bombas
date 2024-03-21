
<!---
   Para comentarios usar este bloque para documentar pendientes, secuencias, etc.
--->


![](https://s3.amazonaws.com/videos.pentesteracademy.com/videos/badges/low/arm-assembly.png)

Borrar y modificar README

# Utilizar los dos directorios

- code  - ahi depositar sus programas los ***archivos extensión *.s****  (Source File) algunos autores en x86 de ponen .asm y en otras plataformas ARM compatibles la extension *.s
- Todo programa lleva su comentario en la parte de arriba, objetivo y nombre del programador minimo, como templete
- images  - de haber algo de pantallas ahi se presentaran, su busca documentarlas en MARKDOWN el código es:

``` ![](images/---archivo.jpg---) recordar que no lleva espacios```

<!---
  Los nombres de las imagenes no deben cambiar de preferenci el nombre del programa como:  KIOSKO.cpp (su pantallas serian KISOCO.jpg, KIOSCO-1.jpg, KIOSCO-2.jpg ... )
  Y asi procurar estar agrupados.
--->



- Programa en MarkDown es inicia con tres tildes * (`) sin espacio, seguido de el lenguaje de programacion, al final del codigo se poner otra vez los mismos tilder..

No se usan espacios en nombres de archivos, usar los nombres estilo camelCase (primera palabra minusculas, mayuscula solo la 1ra letra de cada palabra subsecuente):  ejemplo: sensorHumo, etc.

Suerte.



------

<pre>

	<p align=center>

Tecnológico Nacional de México
Instituto Tecnológico de Tijuana

Departamento de Sistemas y Computación
Ingeniería en Sistemas Computacionales

Semestre:
Febrero - Junio 2022

Materia:
Lenguajes de interfaz

Docente:
M.C. Rene Solis Reyes 

Unidad:
1

Título del trabajo:
Exposicion Tema 4

Estudiante:

Rosales Gómez Valeria
Vara Espinoza Ulises Andres 
Vera Cortez Oscar Bernardino
Gonzalez Vazquez Melanie Estefania
Quiñonez Rocha Luis Arturo

	</p>

</pre>

<pre>

	<p align=left>

Estructuras de control condicionales
En este apartado se describen las estructuras de control condicionales
if-then e if-then-else.
		
Estructura condicional if-then
La estructura condicional if-then está presente en todos los lenguajes
de programación y se usa para realizar o no un conjunto de acciones
dependiendo de una condición. A continuación se muestra un programa
escrito en Python3 que utiliza la estructura if-then.

X = 1
Y = 1
Z = 0

if (X == Y):
Z = X + Y

El programa anterior comprueba si el valor de X es igual al valor de Y
y en caso de que así sea, suma los dos valores, almacenando el resultado
en Z. Si no son iguales, Z permanecerá inalterado.
Una posible implementación del programa anterior en ensamblador
Thumb de ARM, sería la siguiente:

1 .data
2 X: .word 1
3 Y: .word 1
4 Z: .word 0
5
6 .text
7 main: ldr r0, =X
8 ldr r0, [r0] @ r0 <- [X]
9 ldr r1, =Y
10 ldr r1, [r1] @ r1 <- [Y]
11
12 cmp r0, r1
13 bne finsi
14 add r2, r0, r1 @-
15 ldr r3, =Z @ [Z] <- [X] + [Y]
16 str r2, [r3] @-
17
18 finsi: wfi

La idea fundamental para implementar la instrucción «if x==y:» ha consistido en utilizar una instrucción
de salto condicional que salte si no se cumple dicha condición, «bne». De esta forma, si los dos valores 
comparados son iguales, el programa continuará, ejecutando el bloque de instrucciones que deben ejecutarse 
solo si «x==y» (una suma en este ejemplo). En caso contrario, se producirá
el salto y dicho bloque no se ejecutará.

Estructura condicional if-then-else
Sea el siguiente programa en Python3:

1 X = 1
2 Y = 1
3 Z = 0
4
5 if (X == Y):
6 Z = X + Y
7 else:
8 Z = X + 5

En este caso, si se cumple la condición (¿son iguales X y Y?) se realiza
una acción, sumar X y Y, y si no son iguales, se realiza otra acción
diferente, sumar el número 5 a X.
Una posible implementación del programa anterior en ensamblador
Thumb de ARM, sería la siguiente:

1 .data
2 X: .word 1
3 Y: .word 1
4 Z: .word 0
5
6 .text
7 main: ldr r0, =X
8 ldr r0, [r0] @ r0 <- [X]
9 ldr r1, =Y
10 ldr r1, [r1] @ r1 <- [Y]
11
12 cmp r0, r1
13 bne else
14 add r2, r0, r1 @ r2 <- [X] + [Y]
15 b finsi
16
17 else: add r2, r0, #5 @ r2 <- [X] + 5
18
19 finsi: ldr r3, =Z
20 str r2, [r3] @ [Z] <- r2
21
22 stop: wfi

Estructuras de control repetitivas
Una vez vistas las estructuras de control condicionales, vamos a ver
ahora las estructuras de control repetitivas while y for.

Estructura de control repetitiva while
La estructura de control repetitiva while permite ejecutar repetidamente un bloque de código mientras se siga cumpliendo una determinada
condición. La estructura while funciona igual que una estructura if-then,
en el sentido de que si se cumple la condición evaluada, se ejecuta el código asociado al cumplimiento de dicha condición. Pero a diferencia de
la estructura if-then, una vez se ha ejecutado la última instrucción del código asociado a la condición, el control vuelve a la evaluación de la
condición y todo el proceso se vuelve a repetir.
	
El siguiente programa en Python3 muestra el uso de la estructura
de control repetitiva while.

1 X = 1
2 E = 1
3 LIM = 100
4
5 while (X<LIM):
6 X = X + 2 * E
7 E = E + 1
8 print(X)

El programa anterior realizará las operaciones X = X + 2 · E y
E = E + 1 mientras se cumpla que X < LIM. Por lo tanto, la variable X irá tomando los siguientes valores con cada iteración del bucle:
3, 7, 13, 21, 31, 43, 57, 73, 91, 111.
Una posible implementación del programa anterior en ensamblador
Thumb de ARM sería la siguiente:

1 .data
2 X: .word 1
3 E: .word 1
4 LIM: .word 100
5
6 .text
7 main: ldr r0, =X
8 ldr r0, [r0] @ r0 <- X
9 ldr r1, =E
10 ldr r1, [r1] @ r1 <- E
11 ldr r2, =LIM
12 ldr r2, [r2] @ r2 <- LIM
13
14 bucle: cmp r0, r2
15 bpl finbuc
16 lsl r3, r1, #1 @ r3 <- 2 * [E]
17 add r0, r0, r3 @ r0 <- [X] + 2 * [E]
18 add r1, r1, #1 @ r1 <- [E] + 1
19 ldr r4, =X
20 str r0, [r4] @ [X] <- r0
21 ldr r4, =E
22 str r1, [r4] @ [E] <- r1
23 b bucle
24
25 finbuc: wfi

Estructura de control repetitiva for
En muchas ocasiones es necesario repetir un conjunto de acciones un
número predeterminado de veces. Esto podría conseguirse utilizando un
contador que se fuera incrementando de uno en uno y un bucle while que
comprobara que dicho contador no ha alcanzado un determinado valor.
Sin embargo, como dicha estructura se da con bastante frecuencia, los
lenguajes de programación de alto nivel suelen proporcionar una forma
de llevarla a cabo directamente.
		  
El siguiente programa muestra un ejemplo de uso de la estructura
de control repetitiva for en Python3.

1 V = [2, 4, 6, 8, 10]
2 n = 5
3 suma = 0
4
5 for i in range(n): # i = [0..N-1]
6 suma = suma + V[i]

El programa anterior suma todos los valores de un vector V y almacena el resultado en la variable suma. Puesto que en dicho programa se
sabe el número de iteraciones que debe realizar el bucle (que es igual al número de elementos del vector), la estructura ideal para resolver dicho
problema es el bucle for. Se deja como ejercicio para el lector pensar en cómo resolver el mismo problema utilizando la estructura while.
Por otro lado, un programa más realista en Python3 no necesitaría la variable n, ya que sería posible obtener la longitud del vector utilizando
la función «len(V)». Si se ha utilizado la variable n ha sido para acercar el problema al caso del ensamblador, en el que sí que se va a tener que
recurrir a dicha variable.
Una posible implementación del programa anterior en ensamblador
Thumb de ARM sería la siguiente:

1 .data
2 V: .word 2, 4, 6, 8, 10
3 n: .word 5
4 suma: .word 0
5
6 .text
7 main: ldr r0, =V @ r0 <- dirección de V
8 ldr r1, =n
9 ldr r1, [r1] @ r1 <- n
10 ldr r2, =suma
11 ldr r2, [r2] @ r2 <- suma
12 mov r3, #0 @ r3 <- 0
13
14 bucle: cmp r3, r1
15 beq finbuc
16 ldr r4, [r0]
17 add r2, r2, r4 @ r2 <- r2 + V[i]
18 add r0, r0, #4
19 add r3, r3, #1
20 b bucle
21
22 finbuc: ldr r0, =suma
23 str r2, [r0] @ [suma] <- r2
24
25 stop: wfi

Como se puede comprobar en el código anterior, el índice del bucle
está almacenado en el registro r3 y la longitud del vector en el registro
r1. En cada iteración se comprueba si el índice es igual a la longitud del
vector. En caso positivo, se salta al final del bucle y en caso negativo,
se realizan las operaciones indicadas en el bucle.

		
Repositorio en el cual se desarrollaron distintos ejercicios en el lenguaje de 
programacion c++, tomados del libro "Problemas para resolver con computadora" 
1ra edicion (1985), por el autor Donald D. Spencer. 

Los ejercicios corresponden al capitulo 6 del libro, entre las paginas 77 a 86.
Se realizaron 25 problemas debido a la entrega fuera del limite de tiempo.

CONDICIONES:

	EXTEMPORÁNEOS DE LA FECHA DE ENTREGA, despues del 25 de marzo y 1 segundo:

	-Solo 25 problemas a resolver y están en aleatorio las condiciones de uso, 
		algunos simples otros de recordar, etc. CAPITULO 6 en adelante.

	-Agregar las indicaciones de los criterios de la rùbrica
	
RÚBRICA:

        Todo problema es necesario siga el templete OBLIGATORIO para entregar el 
		problema codificado, usted puede correr sus programas con su estilo 
		pero ya que este funcionando, debe arreglarlo a presentación para su 
		evaluación.

        MODIFICAR LA PORTADA CON MARKDOWN Y ACTUALIZARLA, esta libre de cambiar 
		todo.
        Los archivos deben tener su extensión .CPP (no .txt, etc.)

	Los problemas están en la relación siguiente:
	
	- 100% Sigue el templete proporcionado por el docente y corren 10 
		Problemas (o si incremento en programas por supuesta dificultad) 
		completamente en GITHUB Classroom (no repositorio personal),  los 
		archivos deben tener su extensión .CPP (no .txt, .EXE, etc.) acomodados 
		en dentro de un directorio  (sin acentos o simbolos) SOLO FUENTES, y 
		modifica el README.md que sea una portada.
	- 80% Sigue el templete proporcionado por el docente y corre 8 Problemas 
		(o si incremento en programas por supuesta dificultad) completamente 
		en GITHUB Classroom (no repositorio personal), los archivos deben 
		tener su extensión .CPP (no .txt, etc.) acomodados en dentro de un 
		directorio (sin acentos o simbolos) SOLO FUENTES, y modifica el 
		README.md que sea una portada.
	- 70% Sigue el templete proporcionado por el docente y corre 7 Problemas 
		(o si incremento en programas por supuesta dificultad) completamente 
		en GITHUB Classroom (no repositorio personal), los archivos deben 
		tener su extensión .CPP (no .txt, etc.) acomodados en dentro de un 
		directorio (sin acentos o simbolos) SOLO FUENTES, y modifica el 
		README.md que sea una portada.
	- 50 % EVITA Y NO USA el templete proporcionado por el docente sus Problemas 
		(o si incremento en programas por supuesta dificultad) completamente 
		en GITHUB Classroom (no repositorio personal) con mas de 7 problemas 
		resueltos, los archivos NO tener su extensión .CPP y  puede o no estar 
		acomodados en dentro de un directorio (sin acentos o simbolos) 
		SOLO FUENTES, y modifica el README.md que sea una portada.

ENTREGA:

	URL del GitHub Classroom, y recuerde arreglar la PORTADA, quitar todos los 
		elementos extras del templete, acomodarlo bien para su presentación 
		solo lo necesario.

	</p>

</pre>
