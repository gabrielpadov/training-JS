# JSON.stringify

Não é recomendado utilizar `JSON.stringify` para comparar objetos em JavaScript.

De fato, parece ser a escolha mais óbvia e fácil para comparação pois não é necessária nenhuma dependência externa. O método converte objetos em cadeias primeiro e a comparação ocorre depois.

O problema: JavaScript não garante a ordem das chaves.

```javascript
  // mesma ordem
  JSON.stringify({ name: 'John', age: 20 }) === JSON.stringify({ name: 'John', age: 20 }) // result: true

  // desordenado
  JSON.stringify({ name: 'John', age: 20 }) === JSON.stringify({ age: 20, name: 'John' }) // result: false
```

- Se os objetos a serem comparados tiverem propriedades inseridas na mesma ordem, a comparação ocorre perfeitamente.
- Se a ordem foi alterada, a igualdade falha.

`JSON.stringify` não é a melhor opção para comparar objetos.

### Bibliotecas recomendadas para comparação entre objetos.
- [Deep's](https://www.npmjs.com/package/deep-equal)
- [Lodash's](https://lodash.com/docs/4.17.15#isEqual)
- [Fast's](https://www.npmjs.com/package/fast-equals)
