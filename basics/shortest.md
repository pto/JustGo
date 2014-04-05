# The Shortest Go Program

> “Begin at the beginning,” the King said, very gravely, “and go on till you
> come to the end: then stop.”
>
><p style="text-align:right">– Lewis Carroll, _Alice in Wonderland_</p>

Here is the shortest possible Go program:

```go
package main
func main(){}
```
[Run](http://play.golang.org/p/xb5ovJaPFq)

Programs in this book are followed by a link to the [Go
Playground](http://play.golang.org), so you can run them without installing Go
on your computer. Program output will also be included in the text.

Every Go program contains a package called `main`, introduced by the keyword
`package`, and a function called `main`, introduced by the keyword `func`.
Ignore for the moment that `(){}` business.

We can refer to this function by “qualifying” the function name with the
package name: `main.main`. If the `main` package also had a function called
`doSomething`, that function’s qualified name would be `main.doSomething`.
 
Running this program has an unsurprising result. In the Go Playground you see

```
[no output]
```

This counts as a modest success.  The program doesn’t do anything, but at least
there were no errors.

### But No Shorter

Let’s prove this is the shortest possible program. If we try to make our
program shorter by dropping the function:

```go
package main
```
[Run](http://play.golang.org/p/q0_itBEfzN)

we find that the compiler enforces the rule that there must be a `main.main`
function:

```bash
runtime.main: undefined: main.main
 [process exited with non-zero status]
```

### Every Program in its Package

Working the other way, removing the package and leaving the function:

```go
func main(){}
```
[Run](http://play.golang.org/p/k_Lqx9ORfK)

also gives an error:

```bash
prog.go:1: package statement must be first
 [process exited with non-zero status]
```

The `:1` in the error message tells us the error occurred on line 1.

### Multi-line Comments

It is possible to have something before `package`, though, and that is a
comment. Here is an example: function:

```go
/* This is a useless program
   that does not even compile */
func main(){}
```
[Run](http://play.golang.org/p/vXroUNbrD8)

This form of comment begins with `/*` and continues, possibly spanning
additional lines, until `*/`. Now the error message points to line 3 as
the location of the problem:

```bash
prog.go:3: package statement must be first
 [process exited with non-zero status]
```

### Single-line Comments

There is another form of comment: two slashes mark the start of a comment
that continues until the end of the line. We can use this type of comment to
hide our function from the compiler:

```go
// func main(){}
```
[Run](http://play.golang.org/p/Bwdn2l9mAc)

Because of the two slashes, this whole line is a comment; the compiler treats 
it like a blank line. The resulting error continues to nag us for a package 
clause:

```bash
prog.go:2: package statement must be first
 [process exited with non-zero status]
```
