# PyScal
small example AST parser / Lexer for pascal

# Usage: 

``` bash
python main.py [--scope] [--stack] your_program.pas
```

Example output:

``` bash
python main.py --scope --stack example.pas
ENTER scope: global
Insert: INTEGER
Insert: REAL
Insert: Alpha
ENTER scope: Alpha
Lookup: INTEGER. (Scope name: global)
Lookup: INTEGER. (Scope name: global)
Lookup: INTEGER. (Scope name: global)
ENTER scope: Beta
Lookup: INTEGER. (Scope name: global)
Lookup: INTEGER. (Scope name: global)
Lookup: INTEGER. (Scope name: global)


SCOPE (SCOPED SYMBOL TABLE)
===========================
Scope name     : Beta
Scope level    : 3
Enclosing scope: Alpha
Scope (Scoped symbol table) contents
------------------------------------
      a: <VarSymbol(name='a', type='INTEGER')>
      b: <VarSymbol(name='b', type='INTEGER')>
      x: <VarSymbol(name='x', type='INTEGER')>


LEAVE scope: Beta


SCOPE (SCOPED SYMBOL TABLE)
===========================
Scope name     : Alpha
Scope level    : 2
Enclosing scope: global
Scope (Scoped symbol table) contents
------------------------------------
      a: <VarSymbol(name='a', type='INTEGER')>
      b: <VarSymbol(name='b', type='INTEGER')>
      x: <VarSymbol(name='x', type='INTEGER')>
   Beta: <ProcedureSymbol(name=Beta, parameters=[<VarSymbol(name='a', type='INTEGER')>, <VarSymbol(name='b', type='INTEGER')>])>


LEAVE scope: Alpha
Lookup: Alpha. (Scope name: global)


SCOPE (SCOPED SYMBOL TABLE)
===========================
Scope name     : global
Scope level    : 1
Enclosing scope: None
Scope (Scoped symbol table) contents
------------------------------------
INTEGER: INTEGER
   REAL: REAL
  Alpha: <ProcedureSymbol(name=Alpha, parameters=[<VarSymbol(name='a', type='INTEGER')>, <VarSymbol(name='b', type='INTEGER')>])>


LEAVE scope: global
ENTER: PROGRAM Main
CALL STACK
1: PROGRAM Main


ENTER: PROCEDURE Alpha
CALL STACK
2: PROCEDURE Alpha
   a                   : 8
   b                   : 7
1: PROGRAM Main


ENTER: PROCEDURE Beta
CALL STACK
3: PROCEDURE Beta
   a                   : 5
   b                   : 10
2: PROCEDURE Alpha
   a                   : 8
   b                   : 7
   x                   : 30
1: PROGRAM Main


LEAVE: PROCEDURE Beta
CALL STACK
3: PROCEDURE Beta
   a                   : 5
   b                   : 10
   x                   : 70
2: PROCEDURE Alpha
   a                   : 8
   b                   : 7
   x                   : 30
1: PROGRAM Main


LEAVE: PROCEDURE Alpha
CALL STACK
2: PROCEDURE Alpha
   a                   : 8
   b                   : 7
   x                   : 30
1: PROGRAM Main


LEAVE: PROGRAM Main
CALL STACK
1: PROGRAM Main
```
