# Destructuring

[Voltar](JavaScript_pro_tips.md)

**Destructuring** é um novo recurso disponível no ES6 que permite atribuir elementos em objetos ou matrizes a variáveis ​​de maneira declarativa e rápida.

Podemos acessar estruturas profundamente aninhadas e até eliminar a necessidade de verificação nula, capturando apenas os elementos que precisamos, levando a um código mais sucinto.

```javascript
  // Obtendo todos os elementos
  const blackMirror = ['black', 'mirror', 'technology', 'bad']
  
  const [first, second, third, fourth] = blackMirror
  
  console.log(first) // 'black'
  console.log(second) // 'mirror'
  console.log(third) // 'technology'
  console.log(fourth) // 'bad'

  // Obtendo o primeiro elemento
  const blackMirror = ['black', 'mirror', 'technology', 'bad']

  const [first] = blackMirror

  console.log(first) // 'black'

  // Agarrando elementos não sequenciais / fora de ordem
  const blackMirror = ['black', 'mirror', 'technology', 'bad'] 

  const [first ,, third] = blackMirror // vírgulas necessárias para separar os elementos 

  console.log (first) // 'black'
  console.log (third) // 'tecnologia "

  //Spread Operator
  const blackMirror = ['black', 'mirror', 'technology', 'bad']

  const [firstElem, ...rest] = blackMirror

  console.log(first) // 'black'
  console.log(rest) // ['mirror', 'technology', 'bad']

  // Array Destructuring from an Object
  const blackMirror = ['black', 'mirror', 'technology', 'bad']
  
  const cereal = {
    frosties: blackMirror
  }
  
  const [first] = cereal.frosties

  console.log(first) // 'black'

  // Array Destructing from a Function
  function sugarPuffs(){
    return blackMirror
  }

  const [,,third] = sugarPuffs()
  
  console.log(third) // 'technology'
```

- **Array Destructing** pode ajudá-lo a escrever um código conciso e mais eficaz, evitando a necessidade de declarar variáveis ​​extras e destruindo apenas os dados necessários para criar seu aplicativo.
