# JavaScript pro tips

### Exemplos de output no console.log

```javascript
  // bad cod
  const foo = { name: 'Tom', age: 30, nervous: false };
  const bar = { name: 'Anne', age: 50, nervous: false };
  const baz = { name: 'Harry', age: 60, nervous: true }

  console.log(foo); // [Object object]
  console.log(bar);  // [Object object]
  console.log(baz); // [Object object]

  // good code
    // computed property names
     console.log({ foo, bar, baz }); 
    // console.table(...)
     console.log([ foo, bar, baz ]); 

  // stack trace logs
  const deleteMe = () => console.trace('bye bye database')

  deleteMe(); 
  deleteMe();
```

### Destructuring
[More](destructuring.md)

```javascript
  const turtle = {
    name: 'Bob',
    legs: 4,
    shell: true,
    type: 'amphibious',
    meal: 10,
    diet: 'berries'
  }

  // Bad Code
  function feed(animal) {
    return `Feed ${animal.name} ${animal.meal} kilos of ${animal.diet}`;
  }

  // Good Code
  function feed({name, meal, diet}) {
    return `Feed ${name} ${meal} kilos of ${diet}`;
  }
  // OR
  function feed(animal) {
    const { name, meal, diet } = animal;
     return `Feed ${name} ${meal} kilos of ${diet}`;
  }

```
### Template literals

```javascript
  const horse = {
    name: 'Thopher',
    size: 'large',
    skills: ['jousting','rancing'],
    age: 7
  }

  // Bad string Code
  let bio = horse.name + 'is a ' + horse.size + 'horse skilled in' + horse.skills.join(' & ');

  // Good string Code
  const { name, size, skills } = horse;
  bio = `${name} is a ${size} skilled in ${skills.join(' & ')}`;

  console.log(bio);

  // Advance tag exemple
  function horseAge(str, age){
    const ageStr = age> 5 ? 'old' : 'young'; 
    return `${str[0]}${ageStr} at ${age} years`;
  }

  const bio2 = horseAge`This horse is ${horse.age}`;
```

### Spread syntax

```javascript
  const pikachu = { name: 'Pikachu' };
  const stats = { hp: 40, attack: 60, defense: 45 };

  // Bad object Code
  pikachu['hp'] = status.hp;
  pikachu['attack'] = status.attack;
  pikachu['defense'] = status.defense;

  //OR
  const lv10 = Object.assign(pikachu, stats);
  const lv11 = Object.assign(pikachu, {hp: 45});

  // Good object Code
  const lv10 = { ...pikachu, ...stats };
  const lv11 = { ...pikachu, hp: 45 };

  // Arrays
  let pokemon = ['Arbok', 'Raichu', 'Sandshrew'];

  // Bad array Code
  pokemon.push('Bulbasaur');
  pokemon.push('Zubat');
  pokemon.push('Weedle');

  // Good object Code
  // push
  pokemon = [...pokemon, 'Bulbasaur', 'Zubat', 'Weedle'];
 // ["Arbok", "Raichu", "Sandshrew", "Bulbasaur", "Zubat", "Weedle"]
 
 //shift
  pokemon = ['Metapod', 'Evee', ...pokemon];
  //  ["Metapod", "Evee", "Arbok", "Raichu", "Sandshrew"]
  pokemon = ['Goldeen', 'Cartepie', ...pokemon, 'Kakuna', ];
   // ["Goldeen", "Cartepie", "Arbok", "Raichu", "Sandshrew", "Kakuna"]
```

### Loops

```javascript
  const orders = [500, 30, 99, 15, 223];

  // Bad loop code 
  const total = 0;
  const withTax = [];
  const highValue = [];

  for (i=0; i < orders.length; i++) {
    // Reduce
    total += orders[i];

    // Map
    withTax.push(orders[i] * 1.1);

    // Filter
    if (orders[i] > 100) {
      highValue.push(orders[i]);
    }
  }

  // Good loop code
    // Reduce
    const total = orders.reduce((acc, cur) => acc + cur);

    // Map 
    const withTax = orders.map(v => v * 1.1);

    // Filter
    const highValue = orders.filter(v => v > 100 );
```

### Async/Await

```javascript
  const random = () => {
    return Promise.resolve(Math.random());
  }

  // Bad promise code
  const sumRandomAsyncNums = () => {
    let first;
    let second;
    let third;

    return random()
      .then(v => {
          first = v;
          return random();
      })
      .then(v => {
          second = v;
          return random();
      })
      .then(v => {
          third = v;
          return first = second + third;
      })
      .then( v => {
          console.log(`Result ${v}`);
      });
  }

  // Good promise code
  const sumRandomAsyncNums = async() => {
    const first = await random();
    const second = await random();
    const third = await random();

    console.log(`Result ${first + second + third}`);
    // other logics
  }

```
