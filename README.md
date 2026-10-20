# Matrix Operations in C

A small console application that reads two integer matrices and lets the user
add them or multiply them. The program is implemented in
[`Matrix Calculus.c`](./Matrix%20Calculus.c) using standard C input and output.
Its prompts and messages are in French.

## Features

- Reads the row and column counts for two matrices.
- Reads and displays each matrix.
- Adds the matrices when they have the same dimensions.
- Multiplies the matrices when the first matrix's column count equals the
  second matrix's row count.
- Displays a message when the selected operation's dimension requirements are
  not met.

## Requirements

- A C compiler, such as GCC (including MinGW-w64 on Windows).
- A terminal or command prompt for entering matrix values.

The program uses fixed-size arrays with a capacity of 100 rows and 100 columns.
Enter dimensions from 1 to 100. The program does not check that dimensions or
input values are valid.

## Build

From the directory containing `Matrix Calculus.c`, compile with GCC:

**Windows (MinGW-w64):**

```sh
gcc "Matrix Calculus.c" -o matrix-calculus.exe
```

**Linux or macOS:**

```sh
gcc "Matrix Calculus.c" -o matrix-calculus
```

## Run

**Windows:**

```sh
.\matrix-calculus.exe
```

**Linux or macOS:**

```sh
./matrix-calculus
```

Follow the French prompts. Enter integer values when requested; matrix
elements are requested row by row.

## Input and operations

The program requests, in this order:

1. The number of rows in matrix `M1`.
2. The number of columns in matrix `M1`.
3. The number of rows in matrix `M2`.
4. The number of columns in matrix `M2`.
5. The elements of `M1`, row by row.
6. The elements of `M2`, row by row.
7. An operation: `1` for addition or `2` for multiplication.

Matrix element prompts use one-based row and column numbers, for example
`M1[1][1]`. Internally, C stores the first element at index `[0][0]`.

### Addition

For matrices `M1` of size `L × M` and `M2` of size `N × O`, addition is
available only when `L == N` and `M == O`. Each result element is calculated
as:

```text
A[i][j] = M1[i][j] + M2[i][j]
```

For example, the matrices

```text
M1 =       M2 =
1  2       5  6
3  4       7  8
```

produce:

```text
6   8
10 12
```

### Multiplication

Multiplication is available only when the number of columns in `M1` equals the
number of rows in `M2` (`M == N`). The result has `L` rows and `O` columns.
Each result element is calculated as the dot product of a row of `M1` and a
column of `M2`:

```text
P[i][j] = sum(M1[i][k] * M2[k][j])
```

> **Current implementation limitation:** the multiplication result array is
> not initialized before the accumulation loop. As a result, multiplication
> output is undefined and may be incorrect. The code contains a comparison
> (`== 0`) where initialization (`= 0`) is needed. Do not rely on multiplication
> results until this is corrected.

## Limitations

- Dimensions are stored in fixed arrays of at most `100 × 100`; the program
  does not reject zero, negative, or greater-than-100 dimensions. Such input
  can cause invalid array access.
- Input is read with `scanf`, but its return value is not checked. Enter
  integers as requested.
- The operation menu accepts `1` or `2`. For another value, it prints the
  prompt again once, but does not repeat the operation selection.
- Matrix elements and intermediate results use the C `int` type. Very large
  values can overflow.
- Multiplication currently has the uninitialized-result issue described above.
