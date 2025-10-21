## Statement
A statement is an expression that may have an observable side effect. Statements without any effects on the runtime may not be translated. Statements must end with a semicolon.

## Expression
An expression is a syntactic notation that mey evaluate to a value.
An expression mey translate to 0 or more sub-expressions.

Note: Assignemnt shall not be considered an expression but a statement.

## Block body
A block body is 0 or more collection of statements. Block body must start with a '\{' and end with a '\}', any statements within these braces must be considered 'in scope'.

## Variable declaration and initialization
A variable declaration is a __statement__ (1) that lexically binds a __well formed identifier__ (2) to the nearest __scope element__ (3).

```
var identifier;
var identifier = expression;
```

An empty initializer expression may be translated with compatible default value at entry.

By "well formed identifier",
1. Identifier can begin with alpha charecters ('a'-'z' upper/lower case)
2. Identifier can continue after the first charecter with alphanumeric ('a'-'z' upper/lower case, 0-9) charecters and underscore ('\_')
3. Identifier may not be longer than 16 charecters.
4. A '\$' or '\!' at the beggining may occur exactly 0 or 1 time.
5. Must not shadow reserved keywords. (A list of reserved keywords is undergoing discussion)

By "scope element",
1. Top level module code.
2. Function body.
3. Lexical block body.

A identifier that is "well formed" shall have the following traits,
1. Must be translated 1 to 1 without any changes (except the '\_' charecter, which can be translated to a space charecter).
2. Shall raise an exception if conflict arises with name resolution at compile time.

Storage class:
1. Identifiers starting with '\$' charecter should be translated to a global variable storage location.
2. Identifiers starting with '\!' charecter should be translated to a saved variable storage location.

## Loop statements
A loop is a construct that should evaluate a __block body__ / __statement__ 0 or many times.

```
for ident in (expr1 .. expr2) statement;
for ident in (expr1 .. expr2) {
  exprs;
}

for (expr1 .. expr2) statement;
```

A "well formed" loop must hold the following true,
1. The expressions `expr1` and `expr2` must evaluate to a number (integer / float).
2. The identifier `ident` must be well formed.

If a loop is "well formed" then,
1. The `expr1` must be evaluated once at entry.
2. The `expr2` must be evaluated before each iteration.
3. The `ident` identifier, if any, must begin at the value evaluated to `expr1`.
3. The `ident` identifier, if any, must be incremented by `1` after each iteration.

## If statements
An if statement is a construct that creates a branch point.

```
if (expr) statement;
if (expr) {
  statement;
}
```

An if statement may have a trailing `else`

```
if (expr) statement1; else statement2;
if (expr) {
  statement;
} else {
  statement;
}
```

### Drafts
- named function parameters
- snake case for everything
- replace `_` with space charecter in compiled fancode
- loops `for i in (0..1) {}`
- variables `var num = 1;`
- multiple wires `var [hit, hitPos, hitObj] = raycast(from, to)`
