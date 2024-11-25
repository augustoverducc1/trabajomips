.data
newcaterogy:
	addiu $sp, $sp, -4
	sw $ra, 4($sp)
	la $a0, catName # input category name
	jal getblock
	move $a2, $v0 # $a2 = *char to category name
		la $a0, cclist # $a0 = list
	li $a1, 0 # $a1 = NULL
	jal addnode
	lw $t0, wclist
	bnez $t0, newcategory_end
	sw $v0, wclist # update working list if was NULL
newcategory_end:
	li $v0, 0 # return success
	lw $ra, 4($sp)
	addiu $sp, $sp, 4
	jr $ra
 
    # Categorías
    categoria_deportes: .asciiz "Deportes"
    categoria_tecnologia: .asciiz "Tecnología"
    categoria_cultura: .asciiz "Cultura"
    
    # Objetos de cada categoría
    deportes: .word 1, 2, 3  # Objetos: Futbol, Baloncesto, Tenis
    tecnologia: .word 101, 102, 103  # Objetos: Computadora, Smartphone, Tablet
    cultura: .word 201, 202  # Objetos: Pintura, Literatura
    
    # Tamanio de cada categoría 
    tamano_deportes: .word 3
    tamano_tecnologia: .word 3
    tamano_cultura: .word 2

    # Mensaje de salida
    mensaje: .asciiz "Objetos en la categoría: "
    salto_linea: .asciiz "\n"

.text
    .globl main
main:
    # Imprimir objetos en la categoría "Deportes"
    li $v0, 4               # Syscall para imprimir string
    la $a0, mensaje         # Cargar la dirección del mensaje
    syscall

    li $v0, 4               # Syscall para imprimir string (nombre de categoría)
    la $a0, categoria_deportes
    syscall

    li $v0, 4               # Syscall para imprimir salto de línea
    la $a0, salto_linea
    syscall

    # Imprimir los objetos en deportes
    la $t0, deportes        # Cargar la dirección de los objetos de deportes
    lw $t1, tamano_deportes # Cargar el tamaño de la lista de objetos
    li $t2, 0               # Inicializar el índice 

imprimir_objetos_deportes:
    bge $t2, $t1, fin_deportes  # Si el índice es mayor o igual al tamaño, salir
    lw $a0, 0($t0)              # Cargar el objeto actual en $a0
    li $v0, 1                   # Syscall para imprimir un número 
    syscall

    li $v0, 4                   # Syscall para imprimir salto de línea
    la $a0, salto_linea
    syscall

    addi $t2, $t2, 1            # Incrementar el índice
    addi $t0, $t0, 4            # Mover al siguiente objeto
    j imprimir_objetos_deportes # Repetir el ciclo

fin_deportes:
    # Hacer lo mismo para las otras categorías

    # Imprimir objetos en la categoría "Tecnología"
    li $v0, 4
    la $a0, mensaje
    syscall

    li $v0, 4
    la $a0, categoria_tecnologia
    syscall

    li $v0, 4
    la $a0, salto_linea
    syscall

    la $t0, tecnologia        # Cargar la dirección de los objetos de tecnología
    lw $t1, tamano_tecnologia # Cargar el tamaño de la lista de objetos
    li $t2, 0                 # Inicializar el índice 

imprimir_objetos_tecnologia:
    bge $t2, $t1, fin_tecnologia  # Si el índice es mayor o igual al tamaño, salir
    lw $a0, 0($t0)                 # Cargar el objeto actual en $a0
    li $v0, 1                      # Syscall para imprimir un número
    syscall

    li $v0, 4                      # Syscall para imprimir salto de línea
    la $a0, salto_linea
    syscall

    addi $t2, $t2, 1               # Incrementar el índice
    addi $t0, $t0, 4               # Mover al siguiente objeto 
    j imprimir_objetos_tecnologia  # Repetir el ciclo

fin_tecnologia:
    # Imprimir objetos en la categoría "Cultura"
    li $v0, 4
    la $a0, mensaje
    syscall

    li $v0, 4
    la $a0, categoria_cultura
    syscall

    li $v0, 4
    la $a0, salto_linea
    syscall

    la $t0, cultura             # Cargar la dirección de los objetos de cultura
    lw $t1, tamano_cultura      # Cargar el tamaño de la lista de objetos
    li $t2, 0                   # Inicializar el índice

imprimir_objetos_cultura:
    bge $t2, $t1, fin_cultura     # Si el índice es mayor o igual al tamaño, salir
    lw $a0, 0($t0)                # Cargar el objeto actual en $a0
    li $v0, 1                     # Syscall para imprimir un número
    syscall

    li $v0, 4                     # Syscall para imprimir salto de línea
    la $a0, salto_linea
    syscall

    addi $t2, $t2, 1              # Incrementar el índice
    addi $t0, $t0, 4              # Mover al siguiente objeto 
    j imprimir_objetos_cultura    # Repetir el ciclo

fin_cultura:
    # Terminar el programa
    li $v0, 10                    # Syscall para terminar
    syscall


