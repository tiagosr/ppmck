# mckc makefile for MinGW

ifndef DEBUG

  CC = gcc
  CFLAGS = -O2 -Wall # -mno-cygwin
  CDEFS =
  LDFLAGS=-mno-cygwin
  STRIP = strip

else

  CC = gcc
  CFLAGS = -g
  CDEFS =
  LDFLAGS =
  STRIP =

endif

CFLAGS += --input-charset=utf-8 --exec-charset=cp932

OBJS = datamake.o file.o mckc.o strings.o 
EXESFX=.exe
EXEDIR=../../bin


.PHONY: all clean strip

TARGET_E = $(EXEDIR)/ppmckc_e$(EXESFX)
TARGET = $(EXEDIR)/ppmckc$(EXESFX)

all: $(TARGET_E) $(TARGET) $(STRIP)

$(TARGET_E): $(OBJS) version_e.o
	$(CC) $(LDFLAGS) -o $@ $(OBJS) version_e.o

$(TARGET): $(OBJS) version.o
	$(CC) $(LDFLAGS) -o $@ $(OBJS) version.o

version_e.o: version.c
	$(CC) $(CFLAGS) $(CDEFS) -DENGLISH -o $@ -c version.c

.c.o:
	$(CC) $(CFLAGS) $(CDEFS) -c $<

strip:
	strip $(TARGET) $(TARGET_E)

mckc.o: mckc.h
datamake.o: mckc.h

clean:
	$(RM) $(OBJS) version.o version_e.o $(TARGET) $(TARGET_E)
	