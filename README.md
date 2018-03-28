	.data
num1: .asciiz "Digite o primeiro número:  "
num2: .asciiz "Digite o segundo número: "
result: .asciiz "O resultado é: "

	.text	
	.globl main
	
main:		
	#comando de impressão na tela
	li $v0,4 
	la $a0, num1
	syscall 
	#entrada 1 do usuário
	li $v0, 5 
	syscall
	move $s1, $v0
	
	#comando de impressão na tela
	li $v0,4 
	la $a0, num2 
	syscall
	#entrada 2 do usuário
	li $v0, 5
	syscall
	move $s2, $v0
While:
	#Se o num1 < num2 va pra exit
	slt $s0, $s1, $s2
	bne $s0,$zero, Exit 
	
	#se o num1 != 0 va pra else
	bne $s1, $zero, Else            
        #num1 = num1+num2-1;
        add $s1, $s1, $s2
        addi $s1, $s1, -1              
        j While              
Else:   
	#num1 = num1-num2+1;
	sub $s1, $s1, $s2
        addi $s1, $s1,1
	j While
Exit:
	#comando de impressão do resultado na tela
	li $v0,4 
	la $a0, result 
	syscall
	
	li $v0,1
	la $a0, ($s1)
	syscall	
