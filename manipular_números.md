# Manipular números em JavaScript

## Arredondamento

 1. ***Math.round***

Arredonda um número para o número inteiro mais próximo. Se a parte decimal do número for menor que 0.5, a função arredonda para baixo. Se a for 0.5 ou superior, a função arredondada para cima.

 2. ***toFixed***

A função define o número de dígitos que aparece após a casa decimal. A função retorna a representação de sequência do número como o valor.

3. ***toPrecision***

Retorna a representação de seqüência de caracteres de um número, mas você pode arredondá-lo para o número especificado de dígitos significativos,que pode ser especificado ou deixá-lo arredondar automaticamente para o número correto de dígitos significativos

```javascript
// 1
Math.round (12,5); // 13
Math.round (12.49); // 12

// 2
const a = 12,8888888888;
const b = a.toFixed (2); // 12,88

// 3
const a = 12.8888888888;
const b = a.toPrecision(2); // 13, since 2 significant digits is specified
const c = a.toPrecision(); // 12.8888888888, since all digits are significant in the original number
```

## Arredondar para o incremento mais próximo

1. Pega o número original, dividi-lo pelo incremento que você deseja arredondar, depois pegar o limite máximo e multiplicar pelo incremento. Isso significa que o número deve sempre arredondar para cima.

2. Pega o número original, dividi-lo pelo incremento que você deseja arredondar, depois pegar o chão e multiplicar pelo incremento. Isso significa que o número deve sempre arredondar para baixo.

Da mesma forma, você pode arredondar para baixo para o incremento mais próximo com `floor`

```javascript
// 1
const roundNumberUp = (num, incremento) => {
  retornar Math.ceil (num / incremento) * incremento;
}
console.log (roundNumberUp (12.2, 0.5)) // 12.5

// 2
const roundNumberUp = (num, incremento) => {
  retornar Math.floor (num / incremento) * incremento;
}
console.log (roundNumberUp (12.2, 0.5)) // 12.5
```

### Exponenciação

 ES2016 ou superior:

- Utiliza o operador `**`.
- Associatividade à direita: `a ** b ** c` é igual à `a ** (b ** c)`.

`Math.pow(arg1, arg2)`

- Dois argumentos, o primeiro é a base e o segundo é o expoente.

```javascript
const a = 2 ** 3; // 8

// Associatividade à direita
const a = 2 ** (3 ** 4);
const b = 2 ** 3 ** 4;
a == b // verdadeiro, ambos são 2.4178516392292583e + 24

// Math.pow
const a = Math.pow (2,3) // 8
```
