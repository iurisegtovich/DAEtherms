#este é um arquivo Makefile - um script para chamar o compilador (compiler), e montadores (linkers) para gerar o seu executável
#com recomendações, em uma forma acessível - arquivo de texto que poder ser usado em qualquer computador
#que pode ser usado diretamente ou servir de guia para quem quiser usar um ambiente de desenvolvimento interativo IDE diferente.

#Aqui definimos opções recomendadas
# -g: Produce debugging information in the operating system's native format (stabs, COFF, XCOFF, or DWARF 2). GDB can work with this debugging information.
# -Wall: Enables commonly used warning options pertaining to usage that we recommend avoiding and that we believe are easy to avoid.
# -fcheck=all:Enable the generation of run-time checks; the argument shall be a delimited list of the following keywords.
# -cpp: Enable preprocessing.
# -fmax-errors=1: Limits the maximum number of error messages to n, at which point GNU Fortran bails out rather than attempting to continue processing the source code.
# -ffree-line-length-none: Set column after which characters are ignored in typical free-form lines in the source file. The default value is 132. n may be none, meaning that the entire line is meaningful.
# -O3: These options control various sorts of optimizations. Without any optimization option, the compiler's goal is to reduce the cost of compilation and to make debugging produce the expected results. Statements are independent: if you stop the program with a breakpoint between statements, you can then assign a new value to any variable or change the program counter to any other statement in the function and get exactly the results you expect from the source code. Turning on optimization flags makes the compiler attempt to improve the performance and/or code size at the expense of compilation time and possibly the ability to debug the program. The compiler performs optimization based on the knowledge it has of the program. Compiling multiple files at once to a single output file mode allows the compiler to use information gained from all of the files when compiling each of them. Not all optimizations are controlled directly by a flag. Only optimizations that have a flag are listed in this section. Most optimizations are only enabled if an -Olevel is set on the command line. Otherwise they are disabled, even if individual optimization flags are specified. Depending on the target and how GCC was configured, a slightly different set of optimizations may be enabled at each -Olevel than those listed here. You can invoke GCC with -Q --help=optimizers to find out the exact set of optimizations that are enabled at each level.
F90_BASIC_OPTIONS = -g -Wall -fmax-errors=1 -ffree-line-length-none
F90_DEBUG_OPTIONS = -fcheck=all
F90_RELEASE_OPTIONS = -O3

DASSLOPTIONS = -O3

COMPILER = gfortran
LINKER = gfortran

.DEFAULT_GOAL = RUN

.PHONNY: RUN

tudo = objdir/daux.o objdir/ddassl.o objdir/dlinpk.o objdir/res.o objdir/jac.o objdir/program.o

objdir/daux.o: ../DASSLsrc/daux.f
	$(COMPILER) $(DASSLOPTIONS) -c ../DASSLsrc/daux.f -o objdir/daux.o
	
objdir/ddassl.o: ../DASSLsrc/ddassl.f objdir/dlinpk.o objdir/daux.o objdir/jac.o objdir/res.o
	$(COMPILER) $(DASSLOPTIONS) -c ../DASSLsrc/ddassl.f -o objdir/ddassl.o
	
objdir/dlinpk.o: ../DASSLsrc/dlinpk.f
	$(COMPILER) $(DASSLOPTIONS) -c ../DASSLsrc/dlinpk.f -o objdir/dlinpk.o
	
objdir/jac.o: jac.f90
	$(COMPILER) $(F90_BASIC_OPTIONS) $(F90_DEBUG_OPTIONS) -c jac.f90 -o objdir/jac.o
	
objdir/res.o: res.f90
	$(COMPILER) $(F90_BASIC_OPTIONS) $(F90_DEBUG_OPTIONS) -c res.f90 -o objdir/res.o
	
objdir/program.o: program.f90
	$(COMPILER) $(F90_BASIC_OPTIONS) $(F90_DEBUG_OPTIONS) -c program.f90 -o objdir/program.o
	
objdir/program.elf: program.f90 objdir/program.o objdir/ddassl.o
	$(LINKER) $(F90_BASIC_OPTIONS) $(F90_DEBUG_OPTIONS) $(tudo) -o objdir/program.elf
	
RUN: objdir/program.elf
	./objdir/program.elf
