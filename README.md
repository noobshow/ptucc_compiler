# ptuc Compiler read me.

This is a brief ReadMe of what this is, what it offers and how to grab, 
navigate and run this software.

# What this is

This is a compiler that converts an imaginary language `ptuc` (that bears quite 
a few similarities with `Pascal`) into `C`. This is done by using `flex` and
`bison`.

# Features

There are quite a lot of commonly sought features with decent implementation 
in this project, some of them are:

 * Modules (yes, that means includes)
 * Macro support (basic) 
 * Nesting includes (up to a limit -- avoids inf. circular includes)
 * Custom multiple `flex` input buffer management
 * Accurate line tracking across includes
 * Does not *fail-fast* (that means we don't die @ first error).
 * Customize compiler using command line arguments

That's what comes to my mind right now, if you dig into the code I am sure
you'll find more.

# Requirements

I assume that you will run this in a modern (unix-like) platform
-- this includes `Linux` and `Mac OS`, sorry `Windows` users. Here is also
a more detailed dependency list:

* recent `Linux` or `Mac OS`
* `gcc` >= 4.7
* `GNU flex` >= 2.6.0
* `GNU bison` >= 3.0.4
* `GNU Make` >= 4.1
* `valgrind` >= 3.11 (optional(?))
* `git` >= 2.7.4 (optional(?))

Finally if you want to follow the tutorial on how this was made
you are going to need a good text editor like `vim`,
`gedit` or `Sublime` I have no real preference there just use
what you are most comfortable with. Should you want to use an `IDE`
I think you will find it really hard to set it up let alone have
proper syntax highlighting. I personally use `vim` but I have
tested `gedit` as well so both these editors will work fine
as they have proper syntax highlighting already implemented.
`Sublime` does not currently have good support for `flex` (`.l`)
and `bison` (`.y`) files; it's also a paid solution.


# Compiling `ptucc`

After you ensure you are on a supported platform, have
installed the required dependencies and successfully closed this
repo is to open a terminal inside the folder you just created
and type:

```
$ make all
```

The default mode compiles the project in `Debug` mode without using optimizations; this can be changed
if `DEBUG` flag is set to `0` at compile time.


# Compiling a `.ptuc` file

The next step is to compile a `.ptuc` file; if you want to create your own files you will probably
have to read the `ptuc` language definition which is located [here][5]. Alternatively, if you want to just
execute the test or the example files you have two options, which are:

## Make the test

This is a fancy wrapper to just compile and run the `sample001.ptuc` file, hence all you have to do
is to type in your console:

```
$ make test
```

## Make the samples

The other way of running the provided sample files is even more easy; you just have to type `make` and
the filename like so:

```
$ make filename
```

So if you want to make `sample005.ptuc` you would do:

```
$ make sample005
```

The output might be a little different depending on your console spam settings but
both ways would compile and execute the files. You will probably wonder why there are
no warnings generated by `gcc` upon compiling the generated `.c` files
(e.g. `sample005.c`). This is to reduce your console spam again and these
warnings are expected as they stem from the way `ptuc` compiler generates `C`. 
If you want to see them regardless you will have to compile it with `DEBUG_GEN_FILES=1`; 
although you can't really do anything about them without fiddling with the code generation.

## Compile the file manually

Should you want to compile the `.ptuc` file manually you can do so by following the instructions
below.

First you will have to compile the `.ptuc` file to its `C` representation:
```
$ ./ptucc < infile.ptuc > outfile.c
```
Then compile the `.c` file itself:
```
$ make outfile
```
Then execute it (if you wish):
```
$ ./outfile
```

## `ptucc` arguments

The console arguments supported by `ptucc` are the following:

* `-v`: produces a more verbose output during parsing (can be used with any option).
* `-i infile.ptuc`: specifies the *input file*, instead of the taking the file pipe'ed from `stdin`.
* `-o outfile.ptuc`: specifies the *output file*.
* `-d depth`: specifies the *maximum* number of `flex` input buffers that we can have.
* `-m macro_limit`: specifies the number of hashtable bins (maximum macros are 4 times this value).
* `-h`: prints up some usage patters.

So for example this: `./ptucc -h` produces this output:

```
$ ./ptucc -h
Example Usage:
  ./ptucc -v verbose output (can be used in any combination)
  ./ptucc -i [infile]
  ./ptucc -i [infile] -o [outfile]
  ./ptucc -i [infile] -o [outfile] -d [depth]
  ./ptucc -i [infile] -o [outfile] -d [depth] -m [macro_limit]
  ./ptucc -h (prints this)
  ./ptucc infile.ptuc
  ./ptucc < infile.ptuc > outfile.c
```

# Epilogue

If you are here just to clone and submit a copy-pasta (you know probably who you are and
why)... I would refrain you from doing so and point you to read the guide on how you
can make something like this on your own ([intro][1], [starting stub][2], [flex part][3],
[bison part][4]). Additionally this version has some *salts* which add more functionality,
so FYI that's quite the giveaway. Hopefully this might encourage you to learn something new
(and useful?) -- I sure hope that's the case, as this code polishing and write-up took a
good three weeks++ of my spare time :).

[1]: docs/intro.md
[2]: docs/ptuc_start.md
[3]: docs/ptuc_lexer.md
[4]: docs/ptuc_parser.md
[5]: docs/ptuc_spec.md





 
 

