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
