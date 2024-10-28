#Generate little endian binary from big endian binary
build/nuc_rev.bin: build/nuc.bin
	xxd -c 4 -e build/nuc.bin > build/nuc_rev.hex
	xxd -r build/nuc_rev.hex build/nuc_rev.bin

#Generate binary from hex file
build/nuc.bin: build/nuc.hex
	xxd -r -p build/nuc.hex build/nuc.bin

build/nuc.hex: cross.fs basewords.fs nuc.fs
	gforth cross.fs basewords.fs nuc.fs

bootstrap: build/nuc.hex verilator/bootstrap
	make -C verilator
	(cd ./verilator/; ./bootstrap)

clean:
	rm -f build/nuc.hex
	make -C xilinx clean
	make -C verilator clean

