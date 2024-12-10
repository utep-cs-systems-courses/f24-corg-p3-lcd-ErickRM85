# Set CPU type and flags
CPU             = msp430g2553
CFLAGS          = -mmcu=${CPU} -Os -I../h
LDFLAGS          = -L../lib -L/opt/ti/msp430_gcc/include/

# Switch the compiler (for the internal make rules)
CC              = msp430-elf-gcc
AS              = msp430-elf-gcc -mmcu=${CPU} -c

# Define the object file
COMMON_OBJECTS  = buzzer.o  

# Target
all: wakedemo.elf

# Link object files to create the final executable
wakedemo.elf: ${COMMON_OBJECTS} wakedemo.o wdt_handler.o
	${CC} ${CFLAGS} ${LDFLAGS} -o $@ $^ -lTimer -lLcd

# Load the program onto the MSP430
load: wakedemo.elf
	msp430loader.sh $^

# Clean up the compiled files
clean:
	rm -f *.o *.elf

# Add rules for buzzer.o to compile buzzer.c
buzzer.o: buzzer.c buzzer.h
	${CC} ${CFLAGS} -c buzzer.c
