# Reloj-Ensamblador-x86-
Reloj que se actualiza en tiempo real y que para salir del programa oprimes la tecla ESC,  hecho en DosBox, 

Arquitectura de las Computadoras 2024, UNAQ
Para realizar este programa es útil dividirlo en problemas más pequeños , como en que primero debemos conocer como podemos utilizar el reloj del sistema e imprimirlo  y otro problema que debemos abordar es como hacer un loop infinito y que se pueda salir al presionar un tecla, vayamos entonces abordando cada uno de estos.

## Reloj 
Si observamos la hoja de interrupciones del 



```assembly
.text
main:
        la   $s0, A              # load variables A and B into registers
        lw   $s0, 0($s0)
        la   $s1, B
        lw   $s1, 0($s1)
```
