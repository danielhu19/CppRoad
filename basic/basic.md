# How C++ Works

## **Author: Daniel Hu**

## The compilation system

![image-20230221202051461](https://raw.githubusercontent.com/danielhu19/mypicgocloud/master/img/image-20230221202051461.png)

**1. Preprocessor**

Translate c/cpp source file into an ASCII intermediate file **(.i)**

```shell
# -E: Preprocess only; do not compile, assemble or link
g++ -E main.cc -o main.i 
g++ -E fun.cc -o fun.i
```

```shell
cpp main.cpp main.i
cpp fun.cpp fun.i
```

**2. Compile**

Translates .i file into an ASCII assembly-language file **(.s)**

```shell
# -S: Compile only; do not assemble or link
g++ -S main.cc -o main.s
g++ -S fun.cc -o fun.s 
```

```shell
cc1plus main.i -o main.s
cc1plus fun.i -o fun.s
```

**3. Assemble**

Translate main.s into a **binary relocatable object file (.o)** 

```shell
# -c: Compile and assemble, but do not link 
g++ -c main.cc -o main.o
g++ -c fun.cc -o fun.o  
```

```shell
as main.s -o main.o
as fun.s -o fun.o
```

Read .o file by

```shell
objdump -d main.o
```

**4. Link**

Combines .o files, along with the necessary systemobject files, to create the binary **executable object file(a.out by default in unix)**

```shell
# one line
g++ main.cc fun.cc -o main
# or use ld
ld main.o fun.o -o main --entry main
# TODO: Got a error from ld
[1]    34946 segmentation fault (core dumped)  ./main
```

[Why --entry main]: https://stackoverflow.com/questions/34758769/load-warning-cannot-find-entry-symbol-start

![image-20230221224319029](https://raw.githubusercontent.com/danielhu19/mypicgocloud/master/img/image-20230221224319029.png)

Figures above were screenshots from CSAPP

