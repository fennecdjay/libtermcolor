# libtermcolor

`libtermcolor` is a small and simple cross-platform library that allows you to add flair to your messages with colors, italics, and other graphics. Currently, it supports:

- Foreground and background
- Italics and bold
- Strikethrough, underline, and blinking

Documentation is provided through comments in [the header file](include/termcolor.h). See [`use.md`](doc/use.md) for more information.

The API is exposed through these three functions:

```c
int tcol_fprintf(FILE* stream, const char* fmt, ...);
int tcol_printf(const char* fmt, ...);
int tcol_snprintf(char *buffer, size_t N, const char *fmt, ...);
```

`tcol_printf` behaves the same as `tcol_fprintf` except that `stream` is by default the standard output. `tcol_snprintf` will write to a buffer of a size `N` that includes the null terminator.

These functions are the same as normal printf except that you can specify colors within brackets. You can escape left brackets with `{{`.

The color is given inside curly braces. Spaces are ignored, but each color must be a valid character sequence.  [`use.md`](doc/use.md) explains the sequences in full.

The following code displays `"Hello, world!"` in rainbow colors, all bold:

```c
int result = tcol_printf("{+}{R}H{G}e{Y}l{C}l{M}o{W}, {G}w{C}o{R}r{B}l{W}d{Y}!{0}\n");
if (result != TermColorErrorNone) {
    printf("error: %s\n", tcol_errorstr(result));
    return 1;
}
```

![Hello world in bold rainbow text](img/hello-world.png)

## Building

First, clone the repo and navigate into its directory:

```sh
git clone https://github.com/Gwion/libtermcolor
cd libtermcolor
```


Then, to build libtermcolor, use:

```
make
```

This command will build the static and dynamic libraries, along with a test program called `demo`.

If you want to build each library separately, use `make dynamic` or `make static`.
