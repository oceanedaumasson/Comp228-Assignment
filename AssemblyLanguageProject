; Group Members
; Oceane Daumasson ID 40275138
; Vanessa Sanders ID 40325226
; Masha Shtrevensky ID 40311423

section .data
number db 3     ; holds the number that will be tested for being a prime
answer db 1    ; holding the information on whether the number is prime (answer is 1) or not (answer is 0)  starting by assuming it is prime
prime_msg db 'Number is prime', 0x0a	; text displayed in the case if number is a prime
not_prime_msg db 'Number is NOT prime', 0x0a	; text displayed in the case if number is not a prime   

section .text
display_prime:	; prints "Number is prime" 
	mov eax, 4	; system call: write()
        mov ebx, 1	; writing to the screen
        mov ecx, prime_msg	; gets the message address
        mov edx, 16	; message length, number of bytes to print
        int 0x80	; calls the kernel to display the message
        ret

display_not_prime:	; prints "Number is NOT prime"
        mov eax, 4	; system call: write()
        mov ebx, 1	; writing to the screen
        mov ecx, not_prime_msg	; gets the message address
        mov edx, 20	; message length, number of bytes to print
        int 0x80	; calls the kernel to display the message
        ret

; helper labels to call the print functions
call_display_prime:
        call display_prime
        jmp exit

call_display_not_prime:
        call display_not_prime
        jmp exit

; sets answer to zero if a divisor is found
change_answer:
	mov byte [answer], 0	; sets answer to zero
        jmp done_loop

global _start
_start:
        mov al, [number]
        movzx eax, al
	cmp eax, 2	; display not prime if number is less than 2 
	jl call_display_not_prime
        mov ecx, eax
       	mov ebx,2
check_loop:
	cmp ebx, ecx	; compare divisor with the number
        jge done_loop	; if divisor >= number, exit loop

prime_loop:	; loop that tests the number for being a prime with divisors from 2 to (number-1)
        mov eax, ecx	; EAX gets the value of the number
        xor edx, edx	; clear EDX
        div ebx	; does EAX/EBX and puts remainder in EDX
        cmp edx, 0	; seeing if edx = 0
        je change_answer	; if the remainder is 0, then the number is not prime
	inc ebx	; incrementing the divisor
        jmp check_loop

done_loop:
        cmp byte [answer], 1
        je call_display_prime	; if answer is 1, printing number is prime message
        cmp byte [answer], 0
        je call_display_not_prime	; if answer is 0, printing number is not prime message

exit:
	mov eax, 1	; system call: exit()
        xor ebx, ebx	; exit code 0
        int 0x80	; call kernel to quit program
