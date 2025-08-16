# project

flowchart:
<img width="1024" height="1536" alt="projectflowchrt" src="https://github.com/user-attachments/assets/7713f8e2-afa6-457b-a720-59b34eab0a23" />

Working code: 
[project.txt](https://github.com/user-attachments/files/21808191/project.txt)
section .data
plain_text db "MANGO"
msg_len equ $-plain_text
key db "LEMON"
label_plain db "Plain text: "
len_label_plain equ $-label_plain
label_key db " Key: "
len_label_key equ $-label_key
label_enc db " Encrypted text: "
len_label_enc equ $-label_enc
label_dec db " Decrypted text: "
len_label_dec equ $-label_dec
nl db 10

section .bss
encrypted resb msg_len
decrypted resb msg_len

section .text
global _start

_start:
    mov ecx, msg_len
    xor esi, esi
enc_loop:
    mov al, [plain_text + esi]
    mov bl, [key + esi]
    xor al, bl
    mov [encrypted + esi], al
    inc esi
    loop enc_loop

    mov ecx, msg_len
    xor esi, esi
dec_loop:
    mov al, [encrypted + esi]
    mov bl, [key + esi]
    xor al, bl
    mov [decrypted + esi], al
    inc esi
    loop dec_loop

    mov edi, 1

    mov eax, 4
    mov ebx, edi
    mov ecx, label_plain
    mov edx, len_label_plain
    int 0x80
    mov eax, 4
    mov ebx, edi
    mov ecx, plain_text
    mov edx, msg_len
    int 0x80

    mov eax, 4
    mov ebx, edi
    mov ecx, label_key
    mov edx, len_label_key
    int 0x80
    mov eax, 4
    mov ebx, edi
    mov ecx, key
    mov edx, msg_len
    int 0x80

    mov eax, 4
    mov ebx, edi
    mov ecx, label_enc
    mov edx, len_label_enc
    int 0x80
    mov eax, 4
    mov ebx, edi
    mov ecx, encrypted
    mov edx, msg_len
    int 0x80

    mov eax, 4
    mov ebx, edi
    mov ecx, label_dec
    mov edx, len_label_dec
    int 0x80
    mov eax, 4
    mov ebx, edi
    mov ecx, decrypted
    mov edx, msg_len
    int 0x80

    mov eax, 4
    mov ebx, edi
    mov ecx, nl
    mov edx, 1
    int 0x80

    mov eax, 1
    xor ebx, ebx
    int 0x80

    ![project](https://github.com/user-attachments/assets/8e04838b-97af-4c97-a776-bdc0485c1a3d)
