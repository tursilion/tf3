#CC = D:/work/coleco/sdcc-4.2.0/bin/sdcc.exe
CC = D:/work/coleco/sdcc20230715/bin/sdcc.exe
CFLAGS = -mz80 --vc -c "-Id:/work/coleco/libti99coleco" "-ID:/work/TI/vgmcomp2/Players/libcolecovgm2" -DENABLEFX --std-sdcc11 --opt-code-speed --less-pedantic --fsigned-char
#AS = D:/work/coleco/sdcc-4.2.0/bin/sdasz80
AS = D:/work/coleco/sdcc20230715/bin/sdasz80
AFLAGS = -plosgff

.PHONY: all clean

# crt0 must be first!
objs = crt0.rel tf3_coleco.rel

all: buildcol
	d:/work/coleco/tursi/makemegacart/release/makemegacart.exe -map crt0.s crt0.ihx tf3.rom

# crt0.s contains a reference to each segment in order, so they can be linked up - put files into segments there
# if makemegacart complains about data in RAM, see if a segment is missing there

buildcol: $(objs)
	$(CC) -mz80 --vc --no-std-crt0 $(BANKS) --code-loc 0x8100 --data-loc 0x7000 -l"d:/work/coleco/libti99coleco/libti99.a" -l"D:\work\TI\vgmcomp2\Players\libcolecovgm2\libcolecovgm2.a" $(objs)
	"../parseMap.exe" crt0.map

# banks - all defined the same way, we just need to declare them
#BANKS =

clean:
	cmd //c del *.rel *.map *.lst *.sym *.asm *.ihx *.rom boss1.c boss2.c boss3.c boss4.c boss5.c

tf3_coleco.rel: tf3_coleco.c
	$(CC) $(CFLAGS) -o tf3_coleco.rel tf3_coleco.c --codeseg tf3 --constseg tf3

# libti99 crt0 copied into folder
crt0.rel: crt0.s
	$(AS) $(AFLAGS) crt0.rel crt0.s
