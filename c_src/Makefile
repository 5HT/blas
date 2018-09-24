
C_SRC_OUTPUT = ../priv/eblas.so

ERL_INCLUDE_DIR = $(ERLANG_ROOT_DIR)/include
BLAS_I = /usr/local/opt/openblas/include
BLAS_L = /usr/local/opt/openblas/lib

UNAME_SYS := $(shell uname -s)
ifeq ($(UNAME_SYS), Darwin)
	CC ?= cc
	CFLAGS ?= -O3 -std=c99 -arch x86_64 -flat_namespace -undefined suppress -finline-functions -Wall -Wmissing-prototypes
else ifeq ($(UNAME_SYS), FreeBSD)
	CC ?= cc
	CFLAGS ?= -O3 -std=c99 -finline-functions -Wall -Wmissing-prototypes
else ifeq ($(UNAME_SYS), Linux)
	CC ?= gcc
	CFLAGS ?= -O3 -std=c99 -finline-functions -Wall -Wmissing-prototypes
endif

$(C_SRC_OUTPUT): *.c
	$(CC) $(CFLAGS) *.c -g -fPIC -shared -o $(C_SRC_OUTPUT) -I $(ERL_INCLUDE_DIR) -I $(BLAS_I) \
		$(C_SRC_OPTS) -L$(BLAS_L) -lopenblas -v
#-l:libatlas.so.3

clean:
	rm -f $(C_SRC_OUTPUT)
	rm -f *.o
	rm -f *~
