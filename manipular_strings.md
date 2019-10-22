# Manipular string em JavaScript

- Uma ***string*** é uma sequência de um ou mais caracteres que podem consistir em letras, números ou símbolos. 
- Cada caractere em uma string JavaScript pode ser acessado por um número de índice e todas as strings têm métodos e propriedades disponíveis para eles.

## String Primitives and String Objects

O JavaScript diferencia entre a primitiva `string`, um tipo de dados imutável e o objeto **String**.

```javascript
// Initializing a new string primitive
const stringPrimitive = "A new string.";

// Initializing a new String object
const stringObject = new String("A new string.");

typeof stringPrimitive; // result: string
typeof stringObject; // result: object
```

Na maioria das vezes, você criará primitivas de string. O JavaScript é capaz de acessar e utilizar as propriedades e os métodos Stringinternos do wrapper de objeto sem realmente alterar a primitiva de string que você criou em um objeto.

Embora esse conceito seja um pouco desafiador a princípio, você deve estar ciente da distinção entre primitivo e objeto. Essencialmente, existem métodos e propriedades disponíveis para todas as seqüências de caracteres e, em segundo plano, o JavaScript realizará uma conversão em objeto e voltará a primitiva sempre que um método ou propriedade for chamado.


### .trim()

> "A função de recorte (trim) é útil para remover espaços extras digitados pelos usuários. Muitas vezes, os usuários nem sabem que digitaram espaços extras. Esse fato também pode levar a problemas de login se, por exemplo, um usuário se registrar com espaço em branco à direita." - “Trimming Strings em JavaScript” by @AurelioDeRosa

O JavaScript possui o ***String.prototype.trim()***, uma função interna para remover os espaços em branco iniciais e finais.

- Os métodos ***trimStart() / trimLeft()*** retornam a string removida do espaço em branco da extremidade esquerda.

- Os métodos ***trimEnd() / trimRight()*** retornam a string removida do espaço em branco da extremidade direita.

- ***trimStart() / trimLeft() e trimEnd() / trimRight()*** não afetam o valor da própria string.

```javascript
// .trim()
const  myString = " Olá mundo! ";
console.log(myString.trim()); // Os espaços em branco à esquerda e à direita são removidos: "Olá mundo!"
console.log(myString); // A string original permanece inalterada: " Olá mundo! "

// Exemplos: trimStart()/trimLeft() e trimEnd()/trimRight()
const csvManifest = "William Brian,William Martin,Henry Ravens,Richard Knowles,Stephen Hopkins";
console.log(csvManifest.split(","));
// Result: ["William Brian", "William Martin", "Henry Ravens", "Richard Knowles", "Stephen Hopkins"]

const passengerManifest = "William Brian, William Martin, Henry Ravens, Richard Knowles, Stephen Hopkins";
console.log(passengerManifest.split(","));
// Result: ["William Brian", " William Martin", " Henry Ravens", " Richard Knowles", " Stephen Hopkins"]
console.log(passengerManifest.split(", ")); // Não recomendado
// Result: ["William Brian", "William Martin", "Henry Ravens", "Richard Knowles", "Stephen Hopkins"]
console.log(passengerManifest.split(",").map(person => person.trimStart())); // Retira somente whitespaces à esquerda
// Result: ["William Brian", "William Martin", "Henry Ravens", "Richard Knowles", "Stephen Hopkins"]

const formattedManifest = "William Brian    ,  William Martin   ,  Henry Ravens ,Richard Knowles   ,  Stephen Hopkins   ";
console.log(formattedManifest.split(",").map(person => person.trim())); // Retira os whitespaces
// Result: ["William Brian", "William Martin", "Henry Ravens", "Richard Knowles", "Stephen Hopkins"]

console.log(formattedManifest.split(",").map(person => person.trimEnd())); // Retira somente whitespaces à direita
// Result: ["William Brian", "  William Martin", "  Henry Ravens", "Richard Knowles", "  Stephen Hopkins"]
```
