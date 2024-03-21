
<!---
   Para comentarios usar este bloque para documentar pendientes, secuencias, etc.
--->


![](https://s3.amazonaws.com/videos.pentesteracademy.com/videos/badges/low/arm-assembly.png)



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

# Marco teórico
Instrucciones de salto condicional e incondicional, bucles y estructuras de decisión en Assembly.

# Instrucciones de salto
```
JMP
JA (JNBE)
JAE (JNBE)
JB (JNAE)
JBE (JNA)
JE (JZ)
JNE (JNZ)
JG (JNLE)
JGE (JNL)
JL (JNGE)
JLE (JNG)
JC
JNC
JNO
JNP (JPO)
JNS
JO
JP (JPE)
JS
```
# Salto incondicional
#### Sintaxis
```
JMP destino
```
Esta instrucción se utiliza para desviar el flujo de un programa sin tomar en cuenta las condiciones actuales de las banderas ni de los datos.

# Saltos condicionales
Los saltos condicionales transfieren el control del programa a la ubicación que se les dé como parámetro si al hacer una comparación se cumple la condición establecida en el salto

#### Sintaxis
```
JAE etiqueta
```
Salta si está arriba o si es igual o salta si no está abajo.
El salto se efectua si CF esta desactivada.

#### Sintaxis
```
JB etiqueta
```
Salta si está abajo o salta si no está arriba o si no es igual.
Se efectúa el salto si CF esta activada.

#### Sintaxis
```
JBE etiqueta
```
Sintaxis:
JBE etiqueta
Salta si está abajo o si es igual o salta si no está arriba.
El salto se efectúa si CF está activado o si ZF está activado (que cualquiera sea igual a 1).

# Estructuras de control condicionales
En este apartado se describen las estructuras de control condicionales
if-then e if-then-else.
	
## Estructura condicional if-then
La estructura condicional if-then está presente en todos los lenguajes
de programación y se usa para realizar o no un conjunto de acciones
dependiendo de una condición. A continuación se muestra un programa
escrito en Python3 que utiliza la estructura if-then.
```python
X = 1
Y = 1
Z = 0

if (X == Y):
Z = X + Y
```
El programa anterior comprueba si el valor de X es igual al valor de Y
y en caso de que así sea, suma los dos valores, almacenando el resultado
en Z. Si no son iguales, Z permanecerá inalterado.
Una posible implementación del programa anterior en ensamblador ARM, sería la siguiente:

```asm
.data
X: .word 1
Y: .word 1
Z: .word 0

    .text
main:
    ldr r0, =X
    ldr r0, [r0] @ r0 <- [X]
    ldr r1, =Y
    ldr r1, [r1] @ r1 <- [Y]

    cmp r0, r1
    bne finsi
    add r2, r0, r1 @-
    ldr r3, =Z @ [Z] <- [X] + [Y]
    str r2, [r3] @-

finsi:
    b .
```
La idea fundamental para implementar la instrucción «if x==y:» ha consistido en utilizar una instrucción
de salto condicional que salte si no se cumple dicha condición, «bne». De esta forma, si los dos valores 
comparados son iguales, el programa continuará, ejecutando el bloque de instrucciones que deben ejecutarse 
solo si «x==y» (una suma en este ejemplo). En caso contrario, se producirá
el salto y dicho bloque no se ejecutará.

## Estructura condicional if-then-else
Sea el siguiente programa en Python3:
```python
X = 1
Y = 1
Z = 0

if (X == Y):
Z = X + Y
else:
Z = X + 5
```
En este caso, si se cumple la condición (¿son iguales X y Y?) se realiza
una acción, sumar X y Y, y si no son iguales, se realiza otra acción
diferente, sumar el número 5 a X.
Una posible implementación del programa anterior en ensamblador ARM, sería la siguiente:
```asm
.data
X: .word 1
Y: .word 1
Z: .word 0

.text
main: 
    ldr r0, =X
    ldr r0, [r0] @ r0 <- [X]
    ldr r1, =Y
    ldr r1, [r1] @ r1 <- [Y]

    cmp r0, r1
    bne else
    add r2, r0, r1 @ r2 <- [X] + [Y]
    b finsi

else: 
    add r2, r0, #5 @ r2 <- [X] + 5

finsi: 
    ldr r3, =Z
    str r2, [r3] @ [Z] <- r2

stop: 
    b stop
```
# Estructuras de control repetitivas
Una vez vistas las estructuras de control condicionales, vamos a ver
ahora las estructuras de control repetitivas while y for.

## Estructura de control repetitiva while
La estructura de control repetitiva while permite ejecutar repetidamente un bloque de código mientras se siga cumpliendo una determinada
condición. La estructura while funciona igual que una estructura if-then,
en el sentido de que si se cumple la condición evaluada, se ejecuta el código asociado al cumplimiento de dicha condición. Pero a diferencia de
la estructura if-then, una vez se ha ejecutado la última instrucción del código asociado a la condición, el control vuelve a la evaluación de la
condición y todo el proceso se vuelve a repetir.
	
El siguiente programa en Python3 muestra el uso de la estructura
de control repetitiva while.
```python
X = 1
E = 1
LIM = 100

while (X<LIM):
X = X + 2 * E
E = E + 1
print(X)
```
El programa anterior realizará las operaciones X = X + 2 · E y
E = E + 1 mientras se cumpla que X <. LIM. Por lo tanto, la variable X irá tomando los siguientes valores con cada iteración del bucle:
3, 7, 13, 21, 31, 43, 57, 73, 91, 111.
Una posible implementación del programa anterior en ensamblador ARM sería la siguiente:
```asm
.data
X: .word 1
E: .word 1
LIM: .word 100

.text
main: 
    ldr r0, =X
    ldr r0, [r0] @ r0 <- X
    ldr r1, =E
    ldr r1, [r1] @ r1 <- E
    ldr r2, =LIM
    ldr r2, [r2] @ r2 <- LIM

bucle: 
    cmp r0, r2
    bpl finbuc
    lsl r3, r1, #1 @ r3 <- 2 * [E]
    add r0, r0, r3 @ r0 <- [X] + 2 * [E]
    add r1, r1, #1 @ r1 <- [E] + 1
    ldr r4, =X
    str r0, [r4] @ [X] <- r0
    ldr r4, =E
    str r1, [r4] @ [E] <- r1
    b bucle

finbuc: 
    b finbuc
```
## Estructura de control repetitiva for
En muchas ocasiones es necesario repetir un conjunto de acciones un
número predeterminado de veces. Esto podría conseguirse utilizando un
contador que se fuera incrementando de uno en uno y un bucle while que
comprobara que dicho contador no ha alcanzado un determinado valor.
Sin embargo, como dicha estructura se da con bastante frecuencia, los
lenguajes de programación de alto nivel suelen proporcionar una forma
de llevarla a cabo directamente.
		  
El siguiente programa muestra un ejemplo de uso de la estructura
de control repetitiva for en Python3.
```python
V = [2, 4, 6, 8, 10]
n = 5
suma = 0

for i in range(n): # i = [0..N-1]
suma = suma + V[i]
```
El programa anterior suma todos los valores de un vector V y almacena el resultado en la variable suma. Puesto que en dicho programa se
sabe el número de iteraciones que debe realizar el bucle (que es igual al número de elementos del vector), la estructura ideal para resolver dicho
problema es el bucle for. Se deja como ejercicio para el lector pensar en cómo resolver el mismo problema utilizando la estructura while.
Por otro lado, un programa más realista en Python3 no necesitaría la variable n, ya que sería posible obtener la longitud del vector utilizando
la función «len(V)». Si se ha utilizado la variable n ha sido para acercar el problema al caso del ensamblador, en el que sí que se va a tener que
recurrir a dicha variable.
Una posible implementación del programa anterior en ensamblador
Thumb de ARM sería la siguiente:
```asm
.data
V: .word 2, 4, 6, 8, 10
n: .word 5
suma: .word 0

.text
main: 
    ldr r0, =V @ r0 <- dirección de V
    ldr r1, =n
    ldr r1, [r1] @ r1 <- n
    ldr r2, =suma
    ldr r2, [r2] @ r2 <- suma
    mov r3, #0 @ r3 <- 0

bucle: 
    cmp r3, r1
    beq finbuc
    ldr r4, [r0]
    add r2, r2, r4 @ r2 <- r2 + V[i]
    add r0, r0, #4
    add r3, r3, #1
    b bucle

finbuc: 
    ldr r0, =suma
    str r2, [r0] @ [suma] <- r2

stop: 
    b stop
```
Como se puede comprobar en el código anterior, el índice del bucle
está almacenado en el registro r3 y la longitud del vector en el registro
r1. En cada iteración se comprueba si el índice es igual a la longitud del
vector. En caso positivo, se salta al final del bucle y en caso negativo,
se realizan las operaciones indicadas en el bucle.

# Saltos incondicionales y condicionales
En este apartado se describen las instrucciones de salto disponibles
en el ensamblador ARM32. En primer lugar se verá qué son los
saltos incondicionales y a continuación, los saltos condicionales.

## Saltos incondicionales
Se denominan saltos incondicionales a aquéllos que se realizan siempre, que no dependen de que se cumpla una determinada condición. La
instrucción de salto incondicional es «b etiqueta», donde «etiqueta»
referencia la línea del programa a la que se quiere saltar. Al tratarse de
una instrucción de salto incondicional, cada vez que se ejecuta la instrucción «b etiqueta», el programa saltará a la instrucción etiquetada
con «etiqueta», independientemente de qué valor tenga el registro CCR.
El siguiente programa muestra un ejemplo de salto incondicional.
```asm
.text
main: 
    mov r0, #5
    mov r1, #10
    mov r2, #100
    mov r3, #0
    b salto
    add r3, r1, r0
salto: 
    add r3, r3, r2
stop: 
    b stop
```

## Saltos condicionales
Las instrucciones de salto condicional tiene la forma «bXX etiqueta»,
donde «XX» se sustituye por un nemotécnico que indica el tipo de condición que se debe cumplir para realizar el salto y «etiqueta» referencia
a la línea del programa a la que se quiere saltar. Las instrucciones de
salto condicional comprueban ciertos indicadores del registro CCR para
decidir si se debe saltar o no. Por ejemplo, la instrucción «beq etiqueta»
(branch if equal) comprueba si el indicador Z está activo. Si está activo,
entonces salta a la instrucción etiquetada con «etiqueta». Si no lo está, el programa continúa con la siguiente instrucción. De forma similar,
«bne etiqueta» (branch if not equal) saltará a la instrucción etiquetada
con «etiqueta» si el indicador Z no está activo, si esta activo, no saltará.

#### Sintaxis
```
JAE etiqueta
```
Salta si está arriba o si es igual o salta si no está abajo.
El salto se efectua si CF esta desactivada.

#### Sintaxis
```
JB etiqueta
```
Salta si está abajo o salta si no está arriba o si no es igual.
Se efectúa el salto si CF esta activada.

#### Sintaxis
```
JBE etiqueta
```
Salta si está abajo o si es igual o salta si no está arriba.
El salto se efectúa si CF está activado o si ZF está activado (que cualquiera sea igual a 1).

#### Sintaxis
```
JE etiqueta
```
Salta si es igual o salta si es cero.
El salto se realiza si ZF está activada.

#### Sintaxis
```
JNE etiqueta
```
Salta si no es igual o salta si no es cero.
El salto se efectua si ZF está desactivada.

#### Sintaxis
```
JG etiqueta
```
Salta si es más grande o salta si no es menor o igual.
El salto ocurre si ZF = 0 u OF = SF.

El siguiente Cuadro muestra las distintas instrucciones de salto condicional.

El siguiente Cuadro muestra las distintas instrucciones de salto condicional.

### Instrucciones de salto condicional
| Instrucción 				| Condición de salto 		  |
|---------------------------------------|---------------------------------|
| «beq» (branch if equal) 		| Iguales (Z)			  |
| «bne» (branch if not equal) 		| No iguales (z)		  |
| «bcs» (branch if carry set) 		| Mayor o igual sin signo (C)	  |
| «bcc» (branch if carry clear) 	| Menor sin signo (c)		  |
| «bmi» (branch if minus) 		| Negativo (N)			  |
| «bpl» (branch if plus) 		| Positivo o cero (n)		  |
| «bvs» (branch if overflow set) 	| Desbordamiento (V)		  |
| «bvc» (branch if overflow clear) 	| No hay desbordamiento (v)	  |
| «bhi» (branch if higher) 		| Mayor sin signo (Cz)		  |
| «bls» (branch if lower of same) 	| Menor o igual sin signo (c o Z) |
| «bge» (branch if greater or equal) 	| Mayor o igual (NV o nv)	  |
| «blt» (branch if less than) 		| Menor que (Nv o nV)		  |
| «bgt» (branch if greater than) 	| Mayor que (z y (NV o nv))	  |
| «ble» (branch if less than or equal) 	| Menor o igual (Nv o nV o Z)	  |

El siguiente ejemplo muestra un programa en el que se utiliza la
instrucción «beq» para saltar en función del resultado de la operación
anterior.
```asm
.text
main: 
    mov r0, #5
    mov r1, #10
    mov r2, #5
    mov r3, #0
    cmp r0, r2
    beq salto
    add r3, r0, r1
salto: 
    add r3, r3, r1
stop: 
    b stop
```
		
<!-- Repositorio en el cual se desarrollaron distintos ejercicios en el lenguaje de 
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
		solo lo necesario.-->
