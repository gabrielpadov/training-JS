# Programação funcional

## Conceito

Paradigma de programação
Exemplo: POO - Modela o código e algoritmos como entidades que possuem características e comportamentos, trata-se de objetos.

> No paradigma funcional pensa o código como uma sequência de funções e/ou passos, os quais de maneira composta irão resolver um problema.

Código funcional é um código composto de múltiplas funções que se compõe
para solucionar um problema. Na prática, abstrai as lógicas de transformações do código em funções e as utilizam no momento oportuno para transformar nos dados de saída desejados.

### Imutabilidade

Primeira otientação: utilizam-se constantes. Ao invés de ter um código com várias variáveis, ao utilizar constantes proporcionamos códigos mais suscintos.

> O conceito possui viés matemático. Por definição, um valor sempre terá aquele valor, independente de onde esteja ou como está sendo usado. É importante entender que nas expressões matemáticas, para um mesmo valor passado a uma variável, teremos o mesmo retorno da função. O valor nunca muda.

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

Imutabilidade significa previsibilidade,programas previsíveis significam programas que os processadores vão lidar melhor. Ao invocar essa função, teremos um retorno, avaliação do comportamento desse retorno demonstrará erro ou acerto, uma vez que entendesse quais caracterista a função possui.

### Abstração

ssss

### Vida real

crescido a adesão a chamada computação paralela, e consequentemente a programação paralela. Um exemplo disso Muitas empresas tem optado por usar linguagens não bloqueantes, como por exemplo Node.js em seus projetos. Outras tem usados linguagens multi thread para lidar com a grande carga de processamento dos seus dados. Mas já imaginou a implementação de códigos paralelos? Pois bem, não vou me aprofundar no assunto, As linguagens funcionais tendem a ser mais amigáveis quando o assunto é programação paralela, e um dos motivos é exatamente a imutabilidade! Por que? Códigos previsíveis e sem efeitos colaterais nos ajudam a desenvolver de forma que múltiplos pedaços do nosso sistema rode em múltiplos processadores, e não teremos muitas dores de cabeça.

### Pontos importantes

- Um código imutável é um código sem efeitos colaterais
- Programas com este paradigma consomem menos memória
- Visa utilizar o máximo do poder de processamento

## Funções

### Funções puras

### Funções de primeira classe - First Class Functions

### Funções de primeira ordem — High Order Functions

### Currying

> Currying é o processo de transformar uma função que espera vários argumentos em uma função que espera um único argumento e retorna outra função curried. Por exemplo, uma função que recebe três argumentos, ao sofrer currying, resulta em uma função que recebe um argumento e retorna uma função que recebe um argumento, que por sua vez retorna uma função que recebe um argumento e retorna o resultado da função original.
