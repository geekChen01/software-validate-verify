.PRECIOUS: %.ll %.instrumented.ll

TARGETS=simple0 simple1 simple2 branch0 branch1 branch2 infeasable

all: ${TARGETS}

%: %.c
	clang -emit-llvm -S -fno-discard-value-names -c -o $@.ll $<
	opt -load ../build/InstrumentPass.so -Instrument -S $*.ll -o $*.instrumented.ll
	clang -o $@ -L../build -lruntime $*.instrumented.ll

clean:
	rm -f *.ll *.out *.err *.smt2 input.txt branch.txt ${TARGETS}
