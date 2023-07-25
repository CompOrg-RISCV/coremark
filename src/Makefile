# Path to clang inside Codasip package
CLANG=../../../sdk/bin/bk3-32IMCB-Upid-ia-clang

# Benchmark settings
CFLAGS=-O3 -flto -funroll-loops -mllvm -unroll-runtime -mllvm -enable-loop-flatten -mllvm -loop-flatten-assume-no-overflow -funroll-loops
USER_CFLAGS=
LDFLAGS=-O3 -flto -Wl,--plugin-opt=-use-codasip-jump-threading -Wl,--plugin-opt=-inline-threshold=10000 -Xlinker --defsym=_STACK_SIZE=0x4000 -Xlinker --defsym=_HEAP_SIZE=0x4000 -stdlib=newlib -Xllc -disable-block-placement=false -Wl,--plugin-opt=-codasip-jump-threading-cost-threshold=22
DEPS=codasip/core_portme.h coremark.h
OBJ=codasip/core_portme.o core_list_join.o core_main.o core_matrix.o core_state.o core_util.o
LIBS=-lm -lsim

# Build object files
%.o: %.c $(DEPS)
	$(CLANG) -c -o $@ $< $(CFLAGS) $(USER_CFLAGS)

# Link benchmark application
coremark.xexe: $(OBJ)
	$(CLANG) -o $@ $^ $(LDFLAGS) $(LIBS)

# All target
all: coremark.xexe

# Clean target
clean:
	rm -f $(OBJ) coremark.xexe
