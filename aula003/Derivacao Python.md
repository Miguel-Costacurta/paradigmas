# Derivação Sintática de um `for` em Python

## Código analisado

```python
for i in x:
    i += 1
Esta é uma derivação sintática do código acima utilizando como referência a gramática do Python 3.9.
```
# 1. Derivação

A derivação parte do símbolo inicial file e aplica as produções da gramática até chegar aos tokens que representam o código Python.
```
file
⇒ statements ENDMARKER
⇒ statement ENDMARKER
⇒ compound_stmt ENDMARKER
⇒ for_stmt ENDMARKER
⇒ 'for' star_targets 'in' star_expressions ':' block ENDMARKER
⇒ 'for' star_target 'in' star_expressions ':' block ENDMARKER
⇒ 'for' target_with_star_atom 'in' star_expressions ':' block ENDMARKER
⇒ 'for' star_atom 'in' star_expressions ':' block ENDMARKER
⇒ 'for' NAME 'in' star_expressions ':' block ENDMARKER
⇒ 'for' i 'in' star_expressions ':' block ENDMARKER
⇒ 'for' i 'in' star_expression ':' block ENDMARKER
⇒ 'for' i 'in' expression ':' block ENDMARKER
⇒ 'for' i 'in' disjunction ':' block ENDMARKER
⇒ 'for' i 'in' conjunction ':' block ENDMARKER
⇒ 'for' i 'in' inversion ':' block ENDMARKER
⇒ 'for' i 'in' comparison ':' block ENDMARKER
⇒ 'for' i 'in' bitwise_or ':' block ENDMARKER
⇒ 'for' i 'in' bitwise_xor ':' block ENDMARKER
⇒ 'for' i 'in' bitwise_and ':' block ENDMARKER
⇒ 'for' i 'in' shift_expr ':' block ENDMARKER
⇒ 'for' i 'in' sum ':' block ENDMARKER
⇒ 'for' i 'in' term ':' block ENDMARKER
⇒ 'for' i 'in' factor ':' block ENDMARKER
⇒ 'for' i 'in' power ':' block ENDMARKER
⇒ 'for' i 'in' await_primary ':' block ENDMARKER
⇒ 'for' i 'in' primary ':' block ENDMARKER
⇒ 'for' i 'in' atom ':' block ENDMARKER
⇒ 'for' i 'in' NAME ':' block ENDMARKER
⇒ 'for' i 'in' x ':' block ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT statements DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT statement DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT simple_stmt DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT assignment NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT single_target augassign (yield_expr | star_expressions) NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT NAME augassign (yield_expr | star_expressions) NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i augassign (yield_expr | star_expressions) NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' (yield_expr | star_expressions) NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' star_expressions NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' star_expression NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' expression NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' disjunction NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' conjunction NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' inversion NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' comparison NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' bitwise_or NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' bitwise_xor NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' bitwise_and NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' shift_expr NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' sum NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' term NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' factor NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' power NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' await_primary NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' primary NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' atom NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' NUMBER NEWLINE DEDENT ENDMARKER
⇒ 'for' i 'in' x ':' NEWLINE INDENT i '+=' 1 NEWLINE DEDENT ENDMARKER
```
# 2. Regras da gramática utilizadas
Estrutura geral
```
file:
    statements ENDMARKER

statements:
    statement+

statement:
    compound_stmt
    | simple_stmts

compound_stmt:
    for_stmt
Estrutura do for
for_stmt:
    'for' star_targets 'in' star_expressions ':' [TYPE_COMMENT] block [else_block]

star_targets:
    star_target

star_target:
    target_with_star_atom

target_with_star_atom:
    star_atom

star_atom:
    NAME

Essas regras permitem derivar a estrutura:

'for' i 'in' x
Expressão x
star_expressions:
    star_expression
    | star_expressions ',' star_expression [',']

star_expression:
    expression
    | '*' bitwise_or

Para o caso analisado:

star_expressions
⇒ star_expression
⇒ expression
⇒ ...
⇒ NAME
⇒ x
Bloco do for
block:
    NEWLINE INDENT statements DEDENT
    | simple_stmts
```
Como o for possui um bloco indentado:
```
block
⇒ NEWLINE INDENT statements DEDENT
Instrução i += 1
simple_stmt:
    assignment
    | type_alias
    | star_expressions
    | return_stmt
    | import_stmt
    | ...
```
Neste caso:
```
simple_stmt
⇒ assignment
```
A produção de assignment utilizada é:
```
assignment:
    NAME ':' expression ['=' annotated_rhs]
    | single_target augassign ~ (yield_expr | star_expressions)
    | single_target ':' expression ['=' annotated_rhs]
```
Para i += 1:
```
assignment
⇒ single_target augassign (yield_expr | star_expressions)
⇒ NAME augassign (yield_expr | star_expressions)
⇒ i augassign (yield_expr | star_expressions)
⇒ i '+=' (yield_expr | star_expressions)
```
Operador +=

```
augassign:
    '+='
    | '-='
    | '*='
    | '@='
    | '/='
    | '%='
    | '&='
    | '|='
    | '^='
    | '<<='
    | '>>='
    | '**='
    | '//='
```
Neste caso:
```
augassign
⇒ '+='
```
Número 1

A expressão 1 passa pelas regras de expressão até chegar em atom:
```
expression
⇒ disjunction
⇒ conjunction
⇒ inversion
⇒ comparison
⇒ bitwise_or
⇒ bitwise_xor
⇒ bitwise_and
⇒ shift_expr
⇒ sum
⇒ term
⇒ factor
⇒ power
⇒ await_primary
⇒ primary
⇒ atom
⇒ NUMBER
⇒ 1
```
A produção relevante de atom é:
```
atom:
    | '(' [yield_expr|star_expressions] ')'
    | '[' [star_named_expressions] ']'
    | '{' [dict | set | dictcomp | setcomp] '}'
    | NAME
    | NUMBER
    | STRING+
    | '...'
    | 'None'
    | 'True'
    | 'False'
```
Portanto:
```
atom
⇒ NUMBER
⇒ 1
```

# 3. Resultado final

A derivação termina em:
```
'for' i 'in' x ':' NEWLINE INDENT i '+=' 1 NEWLINE DEDENT ENDMARKER
```
Que corresponde ao código-fonte:

for i in x:
    i += 1

# 4. Observações

Os elementos NEWLINE, INDENT, DEDENT e ENDMARKER são tokens utilizados pelo analisador léxico/parser do Python para representar a estrutura do código.

Eles não são escritos explicitamente pelo programador.

Por exemplo:
```
NEWLINE
INDENT
    i += 1
DEDENT
```
representa a quebra de linha e a indentação presentes no código-fonte.

Nota: a sequência ⇒ representa uma etapa da derivação. Em cada passo, um símbolo não terminal é substituído por uma produção válida da gramática.

# 5. Conclusão

A derivação demonstra que o código
```
for i in x:
    i += 1
```
pode ser derivado a partir do símbolo inicial file utilizando as produções da gramática sintática do Python 3.9.

O resultado final da derivação corresponde aos tokens que formam o programa:

```
'for' i 'in' x ':' NEWLINE INDENT i '+=' 1 NEWLINE DEDENT ENDMARKER
```
Referência
[Python 3.9 — Full Grammar specification](https://docs.python.org/pt-br/3.9/reference/grammar.html)
