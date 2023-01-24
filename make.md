### Makefile

- Reasons to use makeflie

  - First: To not type long commands again and again.
  - Second: Make recompile only compile files that changed.

- Solutions:

  - First: Using make rules to automate commands
  - Second: Using make rules to specify dependencies :)

- Make rule has a form

      target: dependencies
          commands

- A simple Makefile example:

  This file compiles file named input.c to output.out and runs it. Places object files  
  in ./obj dir and checks for header files in ./include dir

  ```makefile

    # header files dir
    IDIR=./include
    CC=gcc
    CFLAGS=-I$(IDIR)
    # libraries to include in compile command
    # LIBS=-lm
    LIBS=

    # object files dir
    ODIR=./obj
    OUTFILE=output.out

    # files to compile
    COMPFILES=$(wildcard *.c)
    # header files of same name in ./include dir
    DEPS = $(patsubst %,$(IDIR)/%,$(wildcard $(IDIR)/*.h))
    # object files of same name generated in ./obj dir
    OBJ = $(patsubst %.c,$(ODIR)/%.o,$(COMPFILES))

    # if directory does not exist make it
    dir_guard=@mkdir -p $(@D)

    $(ODIR)/%.o: %.c $(DEPS)
    	$(dir_guard)
    	@$(CC) -c -o $@ $< $(CFLAGS)

    default: $(OBJ) $(DEPS)
    	@$(CC) -o $(OUTFILE) $^ $(CFLAGS) $(LIBS)
    	@./$(OUTFILE)

    compile: $(OBJ) $(DEPS)
    	@$(CC) -o $(OUTFILE) $^ $(CFLAGS) $(LIBS)

    .PHONY: clean default compile

    clean:
    	$(RM) $(ODIR)/*.o *~ core $(INCDIR)/*~


    # Other methods of doing things
    #
    #
    #
    # 1. 	SHELL=/bin/bash
    #		_OBJ = $(shell find $(IDIR) -name '*.h')
    #
    # 2.	_CFILES:=$(wildcard *.c)
    # 		OBJ:=$(_CFILES:%.c=%.o)
    #


    #
    # 1. Search for binary in path and return full address
    # pathsearch = $(firstword $(wildcard $(addsuffix /$(1),$(subst :, ,$(PATH)))))
    #
    # 2. Make does not offer a recursive wildcard function, so here's one:
    # rwildcard=$(wildcard $1$2) $(foreach d,$(wildcard $1*),$(call rwildcard,$d/,$2))
    #
  ```

- Symbols:

  - % : used to denote pattern in target and dependencies section
  - $@ : target
  - $^ : dependencies
  - $< : first dependency
  - $\* : used to use pattern (%) in commands section
  - @D : dir in $@

### Links:

- Blogs:

  - [A Simple Makefile Tutorial](https://web.archive.org/web/20230110211045/https://www.cs.colby.edu/maxwell/courses/tutorials/maketutor/)
  - [File Dependencies: make by Steven J Zeil](https://web.archive.org/web/20230124101656/https://www.cs.odu.edu/~zeil/cs350/latest/Public/make/index.html)

- From Manual:

  - [Variables Used by Implicit Rules](https://www.gnu.org/software/make/manual/html_node/Implicit-Variables.html)
  - [Automatic Variables](https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html#Automatic-Variables)
  - [The call Function](https://www.gnu.org/software/make/manual/html_node/Call-Function.html)
  - [Functions for String Substitution and Analysis](https://www.gnu.org/software/make/manual/html_node/Text-Functions.html)
  - [Substitution References](https://www.gnu.org/software/make/manual/html_node/Substitution-Refs.html)
  - [The Function wildcard](https://www.gnu.org/software/make/manual/html_node/Wildcard-Function.html)
  - [Defining and Redefining Pattern Rules](https://www.gnu.org/software/make/manual/html_node/Pattern-Rules.html#Pattern-Rules)
  - [Using Implicit Rules](https://www.gnu.org/software/make/manual/html_node/Implicit-Rules.html)
  - [Catalogue of Built-In Rules](https://www.gnu.org/software/make/manual/html_node/Catalogue-of-Rules.html)
  - [What Makefiles Contain](https://www.gnu.org/software/make/manual/html_node/Makefile-Contents.html)
  - [The Two Flavors of Variables](https://www.gnu.org/software/make/manual/html_node/Flavors.html)
  - [Complete Manual](https://www.gnu.org/software/make/manual/make.html)

- Other Posts:

  - [What do @, - and + do as prefixes to recipe lines in Make?](https://stackoverflow.com/a/3477400)
  - [Create directories using make file](https://stackoverflow.com/a/1951111)
