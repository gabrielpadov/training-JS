# Programação funcional em JavaScript - Parte 1

O paradigma de programação POO, modela o código e algoritmos como entidades que possuem características e comportamentos, trata-se de objetos.

> No paradigma funcional, a modelagem visa o código como uma sequência de funções e/ou passos, os quais de maneira composta irão resolver um problema.

Na prática, abstrai as lógicas de transformações do código em funções e as utilizam no momento oportuno para transformar os dados de entrada em dados de saída previsíveis.

### Imutabilidade
Primeira otientação: utilizar constantes. Ao invés de ter um código com várias variáveis, ao utilizar constantes proporcionamos códigos mais suscintos.

> O conceito possui viés matemático. Por definição, um valor sempre terá aquele valor, independente de onde esteja ou como está sendo usado. É importante entender que nas expressões matemáticas, para um mesmo valor passado a uma variável, teremos o mesmo retorno da função. O valor nunca muda.

Imutabilidade significa previsibilidade. Ao invocar essa função, teremos um retorno, avaliação do comportamento desse retorno demonstrará erro ou acerto, uma vez que entendesse quais caracterista a função possui.

```javascript
var varMutable = 3;

console.log(varMutable); // result: 3

// etapa 1
var impureFunction = () => {
  varMutable = 4;
};
impureFunction();

console.log(varMutable); // result: 4

// etapa 2
const imutableVariable = 3;
const pureFunction = number => number + 2;
const otherImutableVariable = pureFunction(imutableVariable);

console.log(number); // result: number is not defined
console.log(imutableVariable); //result: 3
console.log(otherImutableVariable); // result: 5
```
Etapas
1. A variável **varMutable** declarada como **var** pode ser modificada por uma função, porque a variável está em um escopo compartilhado,o que faz com que ela fique acessível por todo o código. Agora, apresento uma refatoração desse código.

2. Utilizando **const**, fazemos a função receber um valor e o retorne. Observamos que **number** não pode ser acessado fora da função **pureFunction**, **imutableVariable** é passado como parâmetro e assim, seu valor manipulado e **otherImutableVariable** recebe o resultado da manipulação da função **pureFunction**.

### Abstração
Abstrações são necessárias para entendermos como utilizar funções. Em programação, seria a implementação de uma função para um determinado bloco de código a ser utilizado e reutilizado.

```javascript
const isRunning = status => status === 'RUNNING'
const isEnded = status => status === 'ENDED'

const myFunction = (data) => {
  if (isRunning(data.status)) {
    // do something
  }
  if (isEnded(data.status)) {
    // do something
  }
  return // fallback
}
```
No exemplo, a estrutura condicional **if** é abstraída e assim, a **myFunction** ao receber o parametro **data** têm o comportamento previsível de executar as comparações dentro do seu escopo.

## Funções
Princípio: Uma função ao receber pelo menos um parâmetro, uma sequência de procedimentos são executados e algum tipo de valor é retornado.

As funções devem ser sem estado (stateless), ou seja, elas devem sempre agir e retornar algo como se fosse a primeira vez que elas fossem utilizadas no programa. Para uma função neste paradigma, o que aconteceu antes de ser chamada não lhe interessa e não deve influenciar em nada a sua resposta.

Observe:

```javascript
// Primeiro caso
function square(x) {
    return x * x;
}

square(2); // result: 4

//Segundo caso
function generateDate() {
    var date = new Date();
    generate(date);
}

generateDate(); // ?
```
- Primeiro caso: a função recebe como parâmetro uma variável x e retorna um int que é a multiplicação de x com ele mesmo.

- Segundo caso: a função não recebe nada como parâmetro e retorna o que parece ser uma data processada. Mesmo não declarados explicitamente os inputs e outputs dessa função não quer dizer que os mesmos não existam, apenas estão ocultos. De fato, o exemplo ilustra um dos piores problemas nas aplicações modernas: os Efeitos Colaterais (side-effects).

### Efeitos colaterais (side-effects)
> Se uma função mudar algum outro estado externo à função, é dito que ela causou um efeito colateral.

```c
int glob = 0; 
int quadrado ( int x )
{
  glob = 1 ; 
  retornar x * x ;
}

int main () // Prog. principal
{
  int res ;
  glob = 0 ; 
  res = quadrado ( 5 );
  res += glob ;
  return res ;
}
```
Se observamos somente o programa principal, a priori o retorno do valor **res** seria 25. Porém, o programa retorna o valor 26. Durante a chamada da função **quadrado**, a variável global **global** é modificada e o valor de retorno é 25. Temos um chamado efeito colateral ***(side-effects)***.

Funções que possuem inputs e outputs ocultos e podem gerar side-effects são chamadas de Funções Impuras (impure functions). Característica importante: se invocarmos uma função impura diversas vezes, o retorno dela provavelmente não será o mesmo. O que dificulta a manutenção e os testes de uma aplicação.

Considera-se má prática de programação escrever programas que dependam de efeitos colaterais, pois o programa torna-se de difícil manutenção.

### Funções puras
> Funções puras são funções que não modificam o escopo ao redor delas.

Se uma função tem inputs e outputs declarados e não geram side-effects, o retorno de uma função pura dado um parâmetro será sempre o mesmo.

Em programação funcional uma função pura sempre deve retornar um valor, devido a possibilidade do *Encadeamento de operações*: ***fn1(fn2(fn3(value)))***.

```javascript
import localforage from 'localforage'

const storeValue = value => localforage.setItem('myValue', value)

const sumForTwo = number => number + 2
const doubleMe = number => number * 2

const result = storeValue(sumForTwo(doubleMe(3)))

result.then(console.log) // result: 8
```

### Funções de primeira classe - First Class Functions
> Uma função que representa um valor no código, pode ser um array, um objeto…

Significa que funções podem ser usadas como valores, sendo passadas como parâmetros e recebidas como resultados. 

```javascript
const { head } = require('lodash')

/**
 * Insert query
 * @param  {Function} db knex instance
 * @param  {String} database database name
 * @param  {Array} fields
 * @param  {Object} obj object for insert
 * @return {Promise}
 */
const insertQuery = (db, database, fields, obj) => db(database).returning(fields).insert(obj).then(head)

module.exports = insertQuery
```

### Funções de primeira ordem — High Order Functions
> Funções que operam sobre outras funções ou as recebendo como parâmetro ou as retornando.

Permitem fazer abstrações não apenas de valores mas também de ações. Noexemplo abaixo, a função **calculate** recebe três parâmetros. O primeiro é uma função qualquer que será invocada passando como parâmetro x e y.

```javascript
// Exemplo
var calculate = function(fn, x, y) {
    return fn(x, y);
};

// ES5
var sum = function(x, y) {
    return x + y;
};

var mult = function(x, y) {
    return x * y;
};

calculate(sum, 2, 5); // 7
calculate(mult, 2, 5); // 10

// ES6
const sum = (x, y) => x + y;
const mult = (x, y) => x * y;

calculate(sum, 2, 5); // 7
calculate(mult, 2, 5); // 10
```
*Higher-order functions* estão em todos os lugares no ecossistema do JavaScript. 

[Continuação](prog_funcional_parteII.md)

#
### Vida real
 Muitas empresas tem optado por usar linguagens não bloqueantes, como por exemplo Node.js em seus projetos. Outras tem usados linguagens multi thread para lidar com a grande carga de processamento dos seus dados. As linguagens funcionais tendem a ser mais inteligíveis quando o assunto é programação paralela, e um dos motivos é exatamente a imutabilidade. Códigos previsíveis e sem efeitos colaterais ajudam a desenvolver de forma que múltiplos módulos de um sistema executem em múltiplos processadores.

### Pontos importantes
- Um código imutável é um código sem efeitos colaterais
- Programas com este paradigma consomem menos memória
- Visa utilizar o máximo do poder de processamento

#
#### Referências e leituras complementares
Conteúdo baseados nestes artigos
- [Prog. Funcional para iniciantes](https://medium.com/trainingcenter/programa%C3%A7%C3%A3o-funcional-para-iniciantes-9e2beddb5b43)
- [Don't Be Scared Of Functional Programming](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/)
- [Side-effect](https://www.quora.com/What-is-a-side-effect-in-programming)
- [Entender prog. Funcional em JavaScript](https://medium.com/tableless/entendendo-programa%C3%A7%C3%A3o-funcional-em-javascript-de-uma-vez-c676489be08b)
- [Destructuring](https://medium.com/@quinnlashinsky/destructuring-arrays-in-javascript-2cb003160b3a)
- [Manipulação de numbers](https://medium.com/better-programming/the-ultimate-guide-for-manipulating-numbers-in-javascript-44c6343e94cf)

Conteúdo baseados nestes videos
- [Code this, NOT that](https://www.youtube.com/watch?v=Mus_vwhTCq0&list=WL)
