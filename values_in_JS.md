# Valor primitivo em JavaScript

> "Valor primitivo ou tipo de dados primitivos é um dado que não é representado através de um Objeto e, por consequência, não possui metódos." - MDN web docs

Seis tipos primitivos no JavaScript:

- String
- Number
- Boolean
- Null
- undefined
- Symbol (ECMAScript 6)

***Todos os primitivos são imutáveis.***

***Wrapper*** é uma função destinada a chamar uma ou mais funções, às vezes diretamente por conveniência, e às vezes adaptá-las para fazer uma tarefa ligeiramente diferente no processo.

***Wrappers*** possuem primitivos equivalentes: String, Number, boolean, Symbol. Exceção null e undefined.

## valueOf e typeOf

- O método *valueOf* retorna o valor primitivo do objeto especificado.
- O operador *typeOf* retorna uma ***string*** indicando o tipo de um operando.

```javascript
// object.valueOf()
const str = "Hello World!"
str.valueOf() //"Hello World!"

const MyNumber = 100
MyNumber.valueOf() // 100

const num = 0/0
num.valueOf() // NaN

// typeOf operador
typeof 37 === "number" // true

const num = 102
typeOf num // "number"

const str = "anything"
typeOf str // "string"
```

## Valores reais

Um valor verdadeiro significa, simplismente, um valor que é considerado verdadeiro quando avaliado em um contexto booleano, utilizando uma declaração `if` ou o operador `?`.

Qualquer tipo primitivo será avaliado como verdadeiro em JavaScript, com exceção de 7 valores chamados de ***"valores falsos"***:

 1. Number - `0`
 2. BigInt - `0n`
 3. Palavra-chave - `null`
 4. Palavra-chave - `undefined`
 5. String vazia - `""`, `''`, ` `` `
 6. boolean - `false`
 7. Number - `NaN`

Os ***"valores reais"*** incluem a matriz vazia `[ ]` ou o objeto vazio `{ }`.

- Valores são chamados de verdadeiros quando avaliados como `true`.
- Valores são chamados de falsos quando avaliados como `false`.

```javascript
const verdadeiro = "V";
const falso = "F";

const vazio = {};
vazio ? verdadeiro : falso; // V

[] ? verdadeiro : falso; // V
0 ? verdadeiro : falso; // F
37 ? verdadeiro : falso; // V
false ? verdadeiro : falso; // F
true ? verdadeiro : falso; // V
0n ? verdadeiro : falso; // F
37n ? verdadeiro : falso; // V
"" ? verdadeiro : falso; // F
"anything" ? verdadeiro : falso; // V
null ? verdadeiro : falso; // F
undefined ? verdadeiro : falso; // F
NaN ? verdadeiro : falso; // F
```
