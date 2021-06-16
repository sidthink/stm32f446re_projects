CC=arm-none-eabi-gcc

#preprocessing
PPFLAGS = -g -E
#assembly 
AFLAGS  = -g -S -mcpu=cortex-m4 -mthumb -mfloat-abi=soft -std=gnu11 -Wall -O0

#obj file
OFLAGS = -g -c -mcpu=cortex-m4 -mthumb -mfloat-abi=soft -std=gnu11 -Wall -O0
#Link flags
LDFLAGS = -g -mcpu=cortex-m4 -mthumb -mfloat-abi=soft --specs=rdimon.specs -T stm32_ls.ld -Wl,-Map=final.map

all: main.o stm32_startup.o final_sh.elf
main.i: main.c 
	$(CC) $(PPFLAGS) $^ -o $@
main.s : main.i
	$(CC) $(AFLAGS) $^ -o $@
main.o : main.s
	$(CC) $(OFLAGS) $^ -o $@

#led.i: led.c 
#	$(CC) $(PPFLAGS) $^ -o $@
#led.s: led.i 
#	$(CC) $(AFLAGS) $^ -o $@
#led.o: led.s 
#	$(CC) $(OFLAGS) $^ -o $@

stm32_startup.i: stm32_startup.c 
	$(CC) $(PPFLAGS) $^ -o $@
stm32_startup.s: stm32_startup.i 
	$(CC) $(AFLAGS) $^ -o $@
stm32_startup.o: stm32_startup.s 
	$(CC) $(OFLAGS) $^ -o $@

final_sh.elf: main.o stm32_startup.o
	$(CC) $(LDFLAGS) $^ -o $@

load:
	openocd -f board/st_nucleo_f4.cfg

clean:
	rm -rf *.i *.s *.o *.elf *.map