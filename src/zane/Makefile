ZANE=zane
EXE=nqueen matmul sudoku bedcov

all:$(EXE)

nqueen:bin/nqueen/main.zn
	$(ZANE) build $@ -o $@

matmul:bin/matmul/main.zn
	$(ZANE) build $@ -o $@

sudoku:bin/sudoku/main.zn
	$(ZANE) build $@ -o $@

bedcov:bin/bedcov/main.zn
	$(ZANE) build $@ -o $@

clean:
	rm -rf $(EXE) out
