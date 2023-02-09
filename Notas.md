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

1. Vamos en el project y escogemos el wizart y ahí escogemos el Device: **PIC12F508**
   
2. 

3. Ahora se habla del tipo de programa que estaremos utilizando en este microchip ![](./img/09-02-2023-08.png)


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