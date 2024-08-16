# Babel Types Cheat Sheet

This cheat sheet provides a quick reference for common Babel **AST node types** in the `@babel/types` package.

There are **AST node types** (written in **Uppercase**) that represent various elements of JavaScript, and **node creation functions** (written in **lowercase**) that generate those types programmatically.

_Example:_

- **Node Type**: `FunctionDeclaration` represents a function declaration in the AST.
- **Node Creation Function**: `functionDeclaration(id, params, body)` generates a `FunctionDeclaration` node.

### 1. General Structure

| **Node Type**                | **Description**                                                                                                                                                                                                                    |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Program**              | The root of the AST (entire program). <br> **Code**:<br> `import { x } from 'my-module'; function myFunc() { return x; }` <br> **AST**:<br> `{ type: 'Program', body: [ImportDeclaration(...), FunctionDeclaration(...)] }`  |
| **BinaryExpression**     | Binary operation (e.g., `+`, `-`). <br> **Code**:<br> `x + 10;` <br> **AST**:<br> `{ type: 'BinaryExpression', operator: '+', left: Identifier('x'), right: NumericLiteral(10) }`                                            |
| **LogicalExpression**    | Logical operation (`&&`, `                                                                                                                                                                                           |     | `). <br> **Code**:<br> `x && y;`<br> **AST**:<br>`{ type: 'LogicalExpression', operator: '&&', left: Identifier('x'), right: Identifier('y') }` |
| **MemberExpression**     | Property access (`obj.prop` or `obj[prop]`). <br> **Code**:<br> `obj.prop;` <br> **AST**:<br> `{ type: 'MemberExpression', object: Identifier('obj'), property: Identifier('prop'), computed: false }`                       |
| **AssignmentExpression** | Assignment (`=` or `+=`). <br> **Code**:<br> `x = 42;` <br> **AST**:<br> `{ type: 'AssignmentExpression', operator: '=', left: Identifier('x'), right: NumericLiteral(42) }`                                                 |
| **VariableDeclaration**  | Variable declaration (`const`, `let`, `var`). <br> **Code**:<br> `const x = 10;` <br> **AST**:<br> `{ type: 'VariableDeclaration', kind: 'const', declarations: [VariableDeclarator(Identifier('x'), NumericLiteral(10))] }` |
| **VariableDeclarator**   | A single variable declarator. <br> **Code**:<br> `const x = 10;` <br> **AST**:<br> `{ type: 'VariableDeclarator', id: Identifier('x'), init: NumericLiteral(10) }`                                                           |



### 2. Imports

| **Node Type**                | **Description**                                                                                                                                                                                                                    |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ImportDeclaration**        | Represents an import statement. <br> **Code**:<br> `import { x } from 'my-module';` <br> **AST**:<br> `{ type: 'ImportDeclaration', specifiers: [ImportSpecifier(Identifier('x'), Identifier('x'))], source: StringLiteral('my-module') }` |
| **ImportSpecifier**          | Named import (`import { x }`). <br> **Code**:<br> `import { x } from 'my-module';` <br> **AST**:<br> `{ type: 'ImportSpecifier', imported: Identifier('x'), local: Identifier('x') }`                                                      |
| **ImportDefaultSpecifier**   | Default import (`import x`). <br> **Code**:<br> `import x from 'my-module';` <br> **AST**:<br> `{ type: 'ImportDefaultSpecifier', local: Identifier('x') }`                                                                                |
| **ImportNamespaceSpecifier** | Namespace import (`import * as x`). <br> **Code**:<br> `import * as x from 'my-module';` <br> **AST**:<br> `{ type: 'ImportNamespaceSpecifier', local: Identifier('x') }`                                                                  |



### 3. Exports

| **Node Type**                | **Description**                                                                                                                                                                                                              |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ExportNamedDeclaration**   | Named export. <br> **Code**:<br> `export const x = 10;` <br> **AST**:<br> `{ type: 'ExportNamedDeclaration', declaration: VariableDeclaration('const', [VariableDeclarator(Identifier('x'), NumericLiteral(10))]), specifiers: [] }` |
| **ExportDefaultDeclaration** | Default export. <br> **Code**:<br> `export default myFunc;` <br> **AST**:<br> `{ type: 'ExportDefaultDeclaration', declaration: Identifier('myFunc') }`                                                                              |
| **ExportSpecifier**          | Named export specifier. <br> **Code**:<br> `export { x };` <br> **AST**:<br> `{ type: 'ExportSpecifier', local: Identifier('x'), exported: Identifier('x') }`                                                                        |
| **ExportAllDeclaration**     | `export * from` statement. <br> **Code**:<br> `export * from 'my-module';` <br> **AST**:<br> `{ type: 'ExportAllDeclaration', source: StringLiteral('my-module') }`                                                                  |



### 4. Functions

| **Node Type**               | **Description**                                                                                                                                                                                                                        |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **FunctionDeclaration**     | Function declaration. <br> **Code**:<br> `function myFunc(x) { return x; }` <br> **AST**:<br> `{ type: 'FunctionDeclaration', id: Identifier('myFunc'), params: [Identifier('x')], body: BlockStatement([ReturnStatement(Identifier('x'))]) }` |
| **FunctionExpression**      | Function expression. <br> **Code**:<br> `const myFunc = function(x) { return x; }` <br> **AST**:<br> `{ type: 'FunctionExpression', id: null, params: [Identifier('x')], body: BlockStatement([ReturnStatement(Identifier('x'))]) }`           |
| **ArrowFunctionExpression** | Arrow function expression. <br> **Code**:<br> `const myFunc = (x) => x + 1;` <br> **AST**:<br> `{ type: 'ArrowFunctionExpression', params: [Identifier('x')], body: BinaryExpression('+', Identifier('x'), NumericLiteral(1)) }`               |
| **ReturnStatement**         | Return statement. <br> **Code**:<br> `return x;` <br> **AST**:<br> `{ type: 'ReturnStatement', argument: Identifier('x') }`                                                                                                                    |
| **CallExpression**          | Function call expression. <br> **Code**:<br> `myFunc(5);` <br> **AST**:<br> `{ type: 'CallExpression', callee: Identifier('myFunc'), arguments: [NumericLiteral(5)] }`                                                                         |



### 5. Statements

| **Node Type**    | **Description**   |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IfStatement**         | `if` statement. <br> **Code**:<br> `if (x > 10) { log('greater'); } else { log('less or equal'); }` <br> **AST**:<br> `{ type: 'IfStatement', test: BinaryExpression('>', Identifier('x'), NumericLiteral(10)), consequent: BlockStatement([ExpressionStatement(CallExpression(Identifier('log'), [StringLiteral('greater')]))]), alternate: BlockStatement([ExpressionStatement(CallExpression(Identifier('log'), [StringLiteral('less or equal')]))]) }`                                |
| **ForStatement**        | `for` loop. <br> **Code**:<br> `for (let i = 0; i < 10; i++) { console.log(i); }` <br> **AST**:<br> `{ type: 'ForStatement', init: VariableDeclaration('let', [VariableDeclarator(Identifier('i'), NumericLiteral(0))]), test: BinaryExpression('<', Identifier('i'), NumericLiteral(10)), update: UpdateExpression('++', Identifier('i')), body: BlockStatement([ExpressionStatement(CallExpression(MemberExpression(Identifier('console'), Identifier('log')), [Identifier('i')]))]) }` |
| **WhileStatement**      | `while` loop. <br> **Code**:<br> `while (x > 0) { x--; }` <br> **AST**:<br> `{ type: 'WhileStatement', test: BinaryExpression('>', Identifier('x'), NumericLiteral(0)), body: BlockStatement([ExpressionStatement(UpdateExpression('--', Identifier('x')))]) }`                                                                                                                                                                                                                           |
| **BlockStatement**      | Block of statements (`{ ... }`). <br> **Code**:<br> `{ log('test'); }` <br> **AST**:<br> `{ type: 'BlockStatement', body: [ExpressionStatement(CallExpression(Identifier('log'), [StringLiteral('test')]))] }`                                                                                                                                                                                                                                                                            |
| **ExpressionStatement** | Wraps an expression as a statement. <br> **Code**:<br> `log('test');` <br> **AST**:<br> `{ type: 'ExpressionStatement', expression: CallExpression(Identifier('log'), [StringLiteral('test')]) }` |



### 6. Literals

| **Node Type**      | **Description**                                                                                                  |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- |
| **StringLiteral**  | String literal. <br> **Code**:<br> `'Hello';` <br> **AST**:<br> `{ type: 'StringLiteral', value: 'Hello' }`              |
| **NumericLiteral** | Numeric literal. <br> **Code**:<br> `42;` <br> **AST**:<br> `{ type: 'NumericLiteral', value: 42 }`                      |
| **BooleanLiteral** | Boolean literal (`true`/`false`). <br> **Code**:<br> `true;` <br> **AST**:<br> `{ type: 'BooleanLiteral', value: true }` |
| **NullLiteral**    | Null literal. <br> **Code**:<br> `null;` <br> **AST**:<br> `{ type: 'NullLiteral' }`                                     |


