# shellphant
bios console 16-bit
bash'''killall -9 qemu-system-x86_64 2>/dev/null; pkill -9 -f qemu 2>/dev/null; curl -sL -o shell.asm "https://raw.githubusercontent.com/bro732965-oss/shellphant/main/shell.asm"; sed -i 's/^org 0x7C00/org 0x10000/' shell.asm; sed -i 's/jne \.scan_loop/jmp input1/' shell.asm; printf '\nprint_char:\n    mov ah, 0x0E\n    int 0x10\n    ret\n' >> shell.asm; nasm -f bin shell.asm -o shell.bin; cat << 'EOF' > stage1.asm
org 0x7C00
bits 16
    cli
    xor ax, ax
    mov ds, ax
    mov es, ax
    mov ss, ax
    mov sp, 0x7C00
    sti
    mov ax, 0x1000
    mov es, ax
    xor bx, bx
    mov ah, 0x02
    mov al, 3
    mov ch, 0
    mov cl, 2
    mov dh, 0
    mov dl, 0
    int 0x13
    jc error
    jmp 0x1000:0x0000
error:
    jmp $
times 510-($-$$) db 0
dw 0xAA55
EOF
nasm -f bin stage1.asm -o stage1.bin; cat stage1.bin shell.bin > final_os.img; truncate -s 1440K final_os.img; qemu-system-x86_64 -drive file=final_os.img,format=raw,if=floppy -boot a -vnc :1'''