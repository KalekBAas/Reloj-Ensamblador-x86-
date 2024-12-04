# Reloj-Ensamblador-x86-
Reloj que se actualiza en tiempo real y que para salir del programa oprimes la tecla ESC,  hecho en DosBox, 

Arquitectura de las Computadoras 2024, UNAQ

Para realizar este programa es útil dividirlo en problemas más pequeños , como en que primero debemos conocer como podemos utilizar el reloj del sistema e imprimirlo  y otro problema que debemos abordar es como hacer un loop infinito y que se pueda salir al presionar un tecla, vayamos entonces abordando cada uno de estos.  


## Reloj 
Si observamos la hoja de interrupciones del ensamblador, podemos ver que en la INT 21h del ensamblador existe el servicio 2Ch para obtener la hora del sistema, investigando acerca de esta interrupción sabemos que:  

INTERRUPCION 21H , SERVICIO 2CH  

<span style="color:red">Obtenemos la hora y se guarda en los registros siguienes:  
CH: Hora; CL: Minutos; DH: Segundos; DL: Céntesimas de segundo (0-99);</span>


```assembly
.text
main:
        MOV AH, 01        # load variables A and B into registers
        INT 16
        JZ 010E
        MOV AH, 00
        INT 16
        CMP AL,1B
        JZ 014C
        CALL 015A      # Llamar a la función 
        MOV AH, 2C       
        INT 21
        MOV AX, 0000
        MOV AL, CH
        MOV BL, 0A
        DIV BL
        CALL 0200
        CALL 022F
        MOV AX, 0000
        MOV AL, CL
        DIV BL
        CALL 0200
        CALL 022F
        MOV AX, 0000
        MOV AL, DH
        DIV BL
        CALL 0200
        MOV AX, 0000
        MOV AL, DL
        DIV BL
        CALL 0200
        MOV CX, D000
        LOOP 0148
        JMP 0100
        INT 20

Función mover la posición del cursor (015A):

        MOV AH, 00
        MOV AL, 03
        INT 10
        MOV AH, 02
        MOV DH, 00
        MOV DL, 00
        MOV BX, 0000
        INT 10
        RET




Función para convertir a ascii e imprimir en pantalla (0200):

        ADD AH, 30
        ADD AL, 30
        MOV BH, AH
        MOV AH, 02
        MOV DL, AL
        INT 21
        MOV DL, BH
        INT 21
        RET
        



Función para imprimir ":" y volver a pedir la hora del sistema (022F):

        MOV AH, 09
        MOV DX, 016E
        INT 21
        MOV AH, 2C
        INT 21
        RET

Cadena (016E):
        3A
        24



        
```

