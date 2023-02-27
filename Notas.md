# Notas
Aqui se encuentran las fechas en las cuales se fue abordando contenido en la materia

## 09/02/2023
La clase debería llmarse sistemas de bajo costo 

Rubrica | Ponderación
--- | ---
Proyecto (en equipo ) | 60%
Tareas (individual) </br> - Cuestionarios </br>- Investigaciones</br>-etc.  | 40%

Hay puntos extra

La clase de hoy empieza hablando del siguiente programa: 

```
AC <- AC + M[X] ; x = dirección M[x] = contenido de la dir x

;Familia PIC
W <- W + F[FFFFF]; si d = 0

F[FFFFF] <- W + F[FFFFF]; si d =1
```

Para ello iremos a mplab 

1. Vamos en el project y escogemos el wizart y ahí escogemos el Device: **PIC12F508**  ![](./img/09-02-2023.png)
   
2. ![](img/09-02-2023-02.png)
3. ![](img/09-02-2023-04.png)
4. ![](img/09-02-2023-08.png)

5. Ahora se habla del tipo de programa que estaremos utilizando en este microchip ![](./img/09-02-2023-08.png)


``` assamble
;PROGRAMA PARA SUMAR 5 MAS0 2
LIST P=12F508
;hay que poner mireg para un nombre de registro que queramos
;tambien podemo poner la dirección en cualquier nombenclatura que queramos 
MIREG equ 0x07

;ahora le decimos en qué lugar debemos de poner el programa 

org 0x0;en este caso ponemos un origen

;en uno de los registros hay que poner el 5 y el 2

;movlw 0x02 ;W<-0x2 ;si ponemos el dos primero cuando queramos subir el otro ese valor no desaparecera

movlw 0x05 ;de esta manera eliminamos el acomulador y esto hace que perdamoe el numero dos 
;ahora la línea de abajo es mi regisro de carga con el acomulador 
movwf MIREG;F[MIREG]] <- W

movlw 0x02 ;w<- 0x02

;después de estos movimientos puedo hacer la suma 

addwf MIREG, 0 ; W< W+F[MIREG] si es un bit cero es a la memoria pero si es un uno suma al acomulador 

end

```

Nota: 
la memoria de este procesador tiene una memoria capacitiva es decir tiene una tarea que se repetira infinitamente ya que esta no cuenta con **Sistema operativo**. 

## 13/02/2023

El día de hoy compararemos códigos 

````
; EJEMPLO 01
	LIST		P=12F508		;Tipo de procesador
    ;
	INCLUDE	"P12F508.INC"	;Definición registros internos
	IMPAR		EQU	0x09		;Def. de par etiqueta valor
		ORG		0x00		;Inicio programa
        ;aquí crga el acomulador con una constante
		MOVLW		b'00000001';Mueve 1 a la posición IMPAR
        ;
		MOVWF		IMPAR
		MOVLW		b'00000010';Mueve 2 a WREG
BUCLE:	ADDWF		IMPAR,1	;IMPAR + W = IMPAR
;Si onemos incf W,0 entonces el include como dice w esun bit cero entonces tenemos un error. y la cero es una dirección 
		NOP				;No hace nada
		GOTO		BUCLE		;Repite el bucle
	
		END				;Fin pograma

````

estamos observano el microchip el cual se encuentra en programas 86 segudo de microchip. 

## 27/02/2023


El día d ehoy veremos **MODOS DE DIRECCIONAMIENTO DE 16F846A**

Recordatorio de arquitectura de computadoras

Veremos el **Directo e Indirecto**

Debemos de bajar el archivo de la plataforma

Vemos el primer banco que el **pic16f84A**

- Direccionamiento directo es el recibe el código de instrucción y en esa parte estarán los bit F y la dirección que está en el código de inestrucción será la que esetará directamente en el Banco o Stack 

  - Nota en program memori podems ver el archivo en binario
- si el opcode es **0086** la dirección directa es **6** ya que el **8** es F de ruta

- direcionamiento **inmediato** lo que se está operando es lo que está allá es decir la direección pasa a ser un número o sea no la ruta a la que se refeerencia esta trabajndo inmediatamente y en el estack está el operando.
- **indirecto** aquí yo tengo la memoria en la cual tengo una dirección hasta arribal como ejemplo entonces lo que sucede llama a una parte del stack y el poperando no está en esa parte del estack si no en otro lugar este modo permite por ejemplo que en ppython una variable le aasignas una variable entera y después le pones una cadena y entonces lo que sucede es que esta en modo relativo y por eso puede cambiar el tipo de dato.

````
LIST P16F84A
INCLUDE <16f84a.INC>
CUENTA EQU 0X20
SUMA EQU  0X21

ORG 0

```