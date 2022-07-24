
all: build/boot.bin

build/boot.bin: ./src/boot.asm
	nasm -f bin ./src/boot.asm -o ./build/boot.bin

# Ctrl + A X で終了
qemu: build/boot.bin
	qemu-system-x86_64 -nographic -curses ./build/boot.bin

clean:
	rm ./build/*.bin