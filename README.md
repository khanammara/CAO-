# CAO-
I m uploading here TOH in MIPS Assembly Languauge
.data
	msg: .asciiz "Enter number of disks: "
	part1: .asciiz "\nMove disk "
	part2: .asciiz " from rod "
	part3: .asciiz " to rod "
	 
	.text
	.globl main
	main:
	    li $v0,  4          # print string
	    la $a0,  msg
	    Syscall
	    li $v0,  5          # read integer
	    Syscall
	 
	    # parameters for the routine
	    add $a0, $v0, $zero # move to $a0
	    li $a1, 'A' #source
	    li $a3, 'B' #aux
	    li $a2, 'C' #destination
	 
	    jal tower_of_hanoi           # call hanoi routine
	 
	    li $v0, 10          # exit
	    Syscall
	 
	tower_of_hanoi:
	 
	    #save in stack
	    addi $sp, $sp, -20 
	    sw   $ra, 0($sp)
	    sw   $s0, 4($sp)
	    sw   $s1, 8($sp)
	    sw   $s2, 12($sp)
	    sw   $s3, 16($sp)
	 
	    add $s0, $a0, $zero
	    add $s1, $a1, $zero
	    add $s2, $a2, $zero
	    add $s3, $a3, $zero
	 
	    addi $t1, $zero, 1
	    beq $s0, $t1, solution
	 
