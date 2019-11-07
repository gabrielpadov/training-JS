# Async / Await

O exemplo demonstra uma consulta simples. A sintaxe é bem similar, o uso do `Async/Await` é apenas um refinamento. O benefício imediato é que não precisamos mais nos preocupar com o aninhamento dos `.then`.

```javascript
const getFirstUser = () => {
  const url = "https://jsonplaceholder.typicode.com/users/1";
  fetch(url)
    .then(response => response.json())
    .then(json => console.log(json));
};

const getSecondUser = async () => {
  const url = "https://jsonplaceholder.typicode.com/users/2";
  const response = await fetch(url);
  console.log(await response.json());
};
```

A palavra-chave `async` é colocada no início da função. O uso da palavra-chave `await` é dentro de uma função `async`.

Na função `async`, qualquer **promise** que colocavamos encadeado com um `.then`, agora acompanha um `await`.

O `await` espera a **promise** ao lado dela se resolver antes de prosseguir com o programa. Em suma, torna as ações assíncronas síncronas. Pode atribuí-lo a uma variável, mas não precisa. Se você não se importa em usar o valor resolvido, posteriormente, não há necessidade de atribuí-lo.

```javascript
const response = await fetch(url);
// also valid:
await fetch(url);
```

### Valores de retorno Async

Diga-me, o que aconteceria se tentássemos registrar o resultado final fora da função?

Alerta de spoiler, dá-lhe esse lixo: `Promise { <pending> }`. Qual é o problema? Embora você possa chamar uma função assíncrona em qualquer lugar, ela sempre retorna uma promessa.

> Uma função assíncrona sempre envolverá seu valor de retorno em **_Promise.resolve_**.

```javascript
const getThirdUser = async () => {
  const url = "https://jsonplaceholder.typicode.com/users/3";
  const response = await fetch(url);
  const json = await response.json();
  return json;
};

console.log(getThirdUser()); // resulta em lixo: Promise { <pending> }

// standalone function
const handleSubmit = event => {
  event.preventDefault();
  UserAdapter.checkUser(user).then(validUser => setCurrentUser(validUser));
};

// is now:
const handleSubmit = async event => {
  event.preventDefault();
  const validUser = await UserAdapter.checkUser(user);
  setCurrentUser(validUser);
};
```

Na prática, **promises** são encontradas em funções independentes, como manipuladores de eventos ou funções de montagem. A única diferença agora é fornecer a palavra-chave `async`.

Mesmo utilizando funções `async` como uma função regular, isso pode ocorrer em comportamentos diferentes.
