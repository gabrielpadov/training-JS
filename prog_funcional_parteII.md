# Programação funcional em Javascript - Parte II

[Parte I](progr_funcional_parteI.md)

### Map

A função **map** invoca um _callback_ e retorna um novo array com o resultado desse _callback_ aplicado em cada item do array inicial.

- **_Uso:_** quando é preciso traduzir/mapear todos os elementos em um array para outro conjunto de valores.

- **_O que faz:_** percorre o array da esquerda para a direita invocando uma função de retorno em cada elemento com parâmetros. Para cada chamada de retorno, o valor devolvido se torna o elemento do novo array. Depois que todos os elementos foram percorridos, `map()` retorna o novo array.

Exemplo 1: converter temperatura de Fahrenheit para Celsius.

```javascript
var fahrenheit = [0, 32, 45, 50, 75, 80, 99, 120];

var celcius = fahrenheit.map(function(elem) {
  return Math.round(((elem - 32) * 5) / 9);
});

// ES6
fahrenheit.map(elem => Math.round(((elem - 32) * 5) / 9));

celcius; //  [ -18, 0, 7, 10, 24, 27, 37, 49 ]
```

Exemplo 2: Temos um array de inteiros e a função retorna o quadrado de cada valor desse array.

```javascript
// Função map em ES5
var numbers = [1, 2, 3];

var square = function(x) {
  return x * x;
};

var squaredNumbers = numbers.map(square); // [1, 4, 9]

// Função map em ES6
const numbers = [1, 2, 3];
const square = x => x * x;
const squaredNumbers = numbers.map(square); // [1, 4, 9]
```

Exemplo 3: Visando o reaproveitamento de código ao usar o **map**. Temos dois arrays de objetos diferentes, ambos tem o campo **name**. Atibuimos uma função que retorne um novo array apenas com os **names** dos objetos:

```javascript
// ES6
const students = [
  { name: "Anna", grade: 6 },
  { name: "John", grade: 4 },
  { name: "Maria", grade: 9 }
];

const teachers = [
  { name: "Mark", salary: 2500 },
  { name: "Todd", salary: 3700 },
  { name: "Angela", salary: 1900 }
];

const byName = object => object.name;
const byNames = list => list.map(byName);

byNames(students); // ["Anna", "John", "Maria"]
byNames(teachers); // ["Mark", "Todd", "Angela"]
```

### Filter

A função **filter** recebe um _callback_ como parâmetro e também retorna um novo array, retorna um filtro dos elementos do array inicial baseado na função de _callback_.

- **_Uso:_** quando é preciso remover elementos indesejados com base em alguma(s) condição(ões).

- **_O que faz:_** percorre o array da esquerda para a direita invocando uma função de retorno em cada elemento. O valor retornado deve ser um booleano que indica se o elemento será mantido ou descartado. Depois de todos os elementos terem sido analisados, `filter()` retorna um novo array com todos os elementos que retornaram como verdadeiro.

Exemplo 1: remover elementos duplicados de um array.

```javascript
var uniqueArray = array.filter(function(elem, index, array) {
  return array.indexOf(elem) === index;
});

// ES6
array.filter((elem, index, arr) => arr.indexOf(elem) === index);
```

Exemplo 2: Temos um array de inteiros e retorna apenas aqueles element os que são maiores do que 4.

```javascript
// ES6
const numbers = [1, 4, 7, 10];
const isBiggerThanFour = value => value > 4;

const numbersBiggerThanFour = numbers.filter(isBiggerThanFour); // [7, 10]
```

### Reduce

A função recebe como parâmetro um _callback_ e um valor inicial, com o objetivo de reduzir o array a um único valor.

- **_Uso:_** quando é preciso encontrar um valor cumulativo ou concatenado com base em elementos de todo o array.
- **_O que faz:_** percorre o array da esquerda para a direita invocando uma função de retorno em cada elemento. O valor retornado é o valor acumulado passado de callback para callback. Depois de todos os elementos terem sido avaliados, `reduce()` retorna o valor acumulado/concatenado.

Exemplo 1: Soma

```javascript
const numbers = [1, 2, 3];
const sum = (x, y) => x + y;

const numbersSum = numbers.reduce(sum, 0); // 6
const numberSum10 = numbers.reduce(sum, 10); // 16 = [1+2+3]+10
```

Exemplo 2: soma de lançamentos de foguetes orbitais no período de 1 ano.

```javascript
var rockets = [
  { country: "Russia", launches: 32 },
  { country: "US", launches: 23 },
  { country: "China", launches: 16 },
  { country: "Europe(ESA)", launches: 7 },
  { country: "India", launches: 4 },
  { country: "Japan", launches: 3 }
];

var sum = rockets.reduce(function(prevVal, elem) {
  return prevVal + elem.launches;
}, 0);

// ES6
rockets.reduce((prevVal, elem) => prevVal + elem.launches, 0);

sum; // 85
```

Exemplo 3: Temos um array de meses e precisamos retornar os meses no formato: **JAN/FEV/MAR … /DEZ**.

```javascript
const months = ["JAN", "FEV", "MAR" /*...*/, , "DEZ"];

const monthsShortener = (previous, current) => {
  if (previous === "") {
    return current;
  } else {
    return previous + "/" + current;
  }
};

const shortenedMonths = months.reduce(monthsShortener, "");
// JAN/FEV/MAR ... /DEZ
```

#### Sobre map(), filter() e reduce()

- Métodos de manipulação de array mais voltados à programação funcional.
- Cada um deles é um método no objeto de protótipo (prototype) Array.
- Alterar um elemento no parâmetro array em qualquer callback persistirá através de todos os callbacks restantes, mas não apresentará quaisquer efeitos no array retornado.
- Funções de callback são invocadas nos índices com qualquer valor, até `undefined`, mas não valores excluídos ou que nunca tiveram um valor atribuído.

> **Importante!**
>
> Esses métodos não vieram para substituir loops que ainda têm seu lugar em diversas situações, porém são alternativas poderosas tanto para se trabalhar com valores cumulativos, quanto para criar subconjuntos com base em condições. Estes métodos são úteis para reduzir a complexidade, trabalhar sem “efeitos colaterais” e, muitas vezes, tornar o código mais legível.

### Currying

A princípio é transformar o código em pequenos trechos expressivos e com maior reuso.

> A técnica de transformar uma função com múltiplos parâmetros em uma sequência de funções que aceitam apenas um parâmetro.

Exemplo 1: Transformar uma função de somar

```javascript
// trecho
var add = function(x, y) {
  return x + y;
};

add(1, 2); // 3

// trecho reescrito (currying)
var add = function(x) {
  return function(y) {
    return x + y;
  };
};

add(1)(2); // 3

var addFive = add(5);
var addTen = add(10);

addFive(3); // 8
addFive(1); // 6

addTen(1); // 11
addTen(10); //20

// Manipulando string
const greeting = greet => name => greet + " " + name;
const hello = greeting("Hello");

hello("World"); // Hello World
hello("Matheus"); // Hello Matheus
```

Exemplo 2: As funções **getUidAuthorFromTopic** recebe três parâmetros. Dois parâmetros são passados na execução da função. O curry transforma esta e uma função que recebe um parâmetro. O mesmo ocorre com a função **acceptOrder** que recebe três parâmetros, mas como foi passado dois parâmetros, retorna uma outra função que recebe um parâmetro.

```javascript
// on getUidAuthorFromTopic module
import { curry } from "ramda";

const getUidAuthorFromTopic = (db, uid, _) => {
  // logic function on here
};

module.exports = curry(getUidAuthorFromTopic);

// acceptOrder module
const acceptOrder = (data, db, uidAuthorFromTopic) => {
  // logic function on here
};

module.exports = curry(acceptOrder);

// on index.js
import getUidAuthorFromTopic from "./getUidAuthorFromTopic";
import acceptOrder from "./acceptOrder";
import canCreateCard from "./canCreateCard";

const createCard = (data, db) => {
  return canCreateCard(db, data.uid_author, data.uid_topic)
    .then(getUidAuthorFromTopic(db, data.uid_topic))
    .then(acceptOrder(data, db))
    .catch(console.error);
};
```

### Compose

Compor funções pequenas para gerar outras mais complexas. A vantagem é o poder de usar essas funções mais complexas, de forma simples, em toda aplicação. Ou seja, aumentamos o reuso.

Exemplo: Manipular uma **string** para caracteres maiúsculos e adicionar uma exclamação no final.

```javascript
const compose = (f, g) => x => f(g(x));

const toUpperCase = x => x.toUpperCase();
const exclaim = x => x + "!";

const angry = compose(
  toUpperCase,
  exclaim
);

angry("ahhh"); // AHHH!
```
