# The Shortest Go Program

Here is the shortest possible Go program:

```go
package main
func main(){}
```

Every Go program contains a package called `main`, introduced by the keyword 
`package`, and a function called `main`, introduced by the keyword `func`.
Ignore for the moment that `(){}` business.

We can refer to this function by “qualifying” the function name with the 
package name: `main.main`. If the `main` package also had a function called
`doSomething`, that function’s qualified name would be `main.doSomething`.
 
We can run this program, not that it will do us much good, by placing the 
text above in a file called `shortest.go` and then using the command

```bash
go run shortest.go
```

The result, not surprisingly, is nothing. This counts as a modest success. 
The program doesn’t do anything, but at least there were no errors.

Let’s prove this is the shortest possible program. If we try to make our 
program shorter by dropping the function:

```go
package main
```

we find that the compiler enforces the rule that there must be a `main.main`
function. Call this program `shorter.go` and run it with

```bash
go run shorter.go
```

We get this error message:

```text
runtime.main: undefined: main.main
```

Working the other way, removing the package and leaving the function:

```go
func main(){}
```

also gives an error:

```text
shorter2.go:1:1: expected 'package', found 'func'
```

This error message helpfully, if cryptically, tells us exactly where the 
error occurred. It was on line 1 in column number 1. That’s what the
`:1:1` in the error message is telling us.

To be sure that we understand that `:1:1`, we’ll add a comment before the
function:

```go
/* "f" is in column 27 */ func main(){}
```

This form of comment begins with `/*` and continues, possibly spanning
additional lines, until `*/`. Now the error message points to column 27 as
the location of the problem:

```text
shorter3.go:1:27: expected 'package', found 'func'
```

Column 27 is significant: it is the location of the `f` in `func`. This 
shows that the compiler skipped over the comment; a comment at the beginning 
isn’t a problem. But the first thing that isn’t a comment or white space must 
be the package clause. If the compiler finds anything else, it complains 
that it wants to see `package`.

There is another form of comment: two slashes mark the start of a comment
that continues until the end of the line. We can use this type of comment to
hide our function from the compiler:

```go
// func main(){}
```

Because of the two slashes, this whole line is a comment; the compiler treats 
it like a blank line. The resulting error continues to nag us for a package 
clause:

```text
shorter4.go:1:18: expected 'package', found 'EOF'
```

`EOF` means “end of file”. There are 17 characters in our file (14 printing
characters, two spaces, and a newline at the end), so the end of file comes
at position 18. That is when the compiler realizes it is never going to see 
`package`.
