AS=as -Iinclude --32
LD=ld -melf_i386
CC=gcc -m32
CPP=gcc -E -nostdinc -Iinclude
CFLAGS=-Wall -pedantic -W -nostdlib -nostdinc -Wno-long-long -I include -fomit-frame-pointer

KERNEL_OBJS= load.o init.o isr.o libcc.o scr.o kprintf.o exceptions.o

#.c.s:
#	${CC} ${CFLAGS} -S -o $*.s $<

.s.o:
	${AS} -a $< -o $*.o >$*.map

all: final.img

final.img: bootsect kernel
	cat bootsect kernel > final.img
	@wc -c final.img

bootsect: bootsect.o
	${LD} --oformat binary -N -e start -Ttext 0x7c00 -o bootsect $<

kernel: ${KERNEL_OBJS}
	${LD} --oformat binary -N -e pm_mode -Ttext 0x0000 -o $@ ${KERNEL_OBJS}
	@wc -c kernel

clean:
	rm -f *.img kernel bootsect *.o *.map

dep:
	sed '/\#\#\# Dependencies/q' < Makefile > tmp_make
	(for i in *.c;do ${CPP} -M $$i;done) >> tmp_make
	mv tmp_make Makefile

### Dependencies:
exceptions.o: exceptions.c include/kprintf.h include/scr.h include/asm.h
init.o: init.c include/scr.h include/isr.h include/asm.h include/kernel.h \
  include/libcc.h include/kprintf.h
kprintf.o: kprintf.c include/scr.h include/asm.h include/kprintf.h
libcc.o: libcc.c include/libcc.h
scr.o: scr.c include/asm.h include/scr.h include/libcc.h
