# MongoDB - Aula 03 - Exercício
autor: Carol Dias

## Liste todos Pokemons com a altura **menor que** 0.5;

```

vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> var query = {height: {$lt: 0.5}}
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("564a758879bb040edf39e99a"),
  "name": "Eevee",
  "description": "Raposa coelho indefesa",
  "attack": 55,
  "defense": 0,
  "height": 0.3,
  "type": "normal"
}
{
  "_id": ObjectId("564a75a579bb040edf39e99c"),
  "name": "Jolteon",
  "description": "Raposa coelho elétrica",
  "attack": 65,
  "height": 0.4,
  "defense": 60,
  "type": "eletric"
}
{
  "_id": ObjectId("564a75c579bb040edf39e99e"),
  "name": "Umbreon",
  "description": "Raposa coelho trevosa",
  "attack": 65,
  "defense": 110,
  "height": 0.4,
  "type": "dark"
}
Fetched 3 record(s) in 22ms

```

## Liste todos Pokemons com a altura **maior ou igual que** 0.5

```
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> var query = {height: {$gte: 0.5}}
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("564a759679bb040edf39e99b"),
  "name": "Vaporeon",
  "description": "Raposa coelho da água",
  "attack": 65,
  "defense": 60,
  "height": 0.6,
  "type": "water"
}
{
  "_id": ObjectId("564a75b379bb040edf39e99d"),
  "name": "Flareon",
  "description": "Raposa coelho de fogo",
  "attack": 130,
  "defense": 60,
  "height": 0.5,
  "type": "fire"
}
{
  "_id": ObjectId("564d28527208ab8fc85f1098"),
  "name": "Leafeon",
  "description": "Raposa coelho de folha",
  "attack": 110,
  "defense": 130,
  "height": 0.5,
  "type": "grass"
}
Fetched 3 record(s) in 5ms

```

## Liste todos Pokemons com a altura **menor ou igual que** 0.5 **E** do tipo grama

```
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> var query = { $and: [{height: {$lte: 0.5}}, {type: /grass/}]}
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("564d28527208ab8fc85f1098"),
  "name": "Leafeon",
  "description": "Raposa coelho de folha",
  "attack": 110,
  "defense": 130,
  "height": 0.5,
  "type": "grass"
}
Fetched 1 record(s) in 1ms

```

## Liste todos Pokemons com o name `Umbreon` (adaptado :p) **OU** com attack **menor ou igual que** 0.5

```
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> var query = {$or: [{name: /umbreon/i}, {attack: {$lte: 0.5}}]}
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("564a75c579bb040edf39e99e"),
  "name": "Umbreon",
  "description": "Raposa coelho trevosa",
  "attack": 65,
  "defense": 110,
  "height": 0.4,
  "type": "dark"
}
Fetched 1 record(s) in 2ms

```

## Liste todos Pokemons com o attack **MAIOR OU IGUAL QUE** 48 **E** com  height **menor ou igual que** 0.5

```
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> var query = {$and: [{attack: {$gte: 48}}, {height: {$lte: 0.5}}]}
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("564a758879bb040edf39e99a"),
  "name": "Eevee",
  "description": "Raposa coelho indefesa",
  "attack": 55,
  "defense": 0,
  "height": 0.3,
  "type": "normal"
}
{
  "_id": ObjectId("564a75a579bb040edf39e99c"),
  "name": "Jolteon",
  "description": "Raposa coelho elétrica",
  "attack": 65,
  "height": 0.4,
  "defense": 60,
  "type": "eletric"
}
{
  "_id": ObjectId("564a75b379bb040edf39e99d"),
  "name": "Flareon",
  "description": "Raposa coelho de fogo",
  "attack": 130,
  "defense": 60,
  "height": 0.5,
  "type": "fire"
}
{
  "_id": ObjectId("564a75c579bb040edf39e99e"),
  "name": "Umbreon",
  "description": "Raposa coelho trevosa",
  "attack": 65,
  "defense": 110,
  "height": 0.4,
  "type": "dark"
}
{
  "_id": ObjectId("564d28527208ab8fc85f1098"),
  "name": "Leafeon",
  "description": "Raposa coelho de folha",
  "attack": 110,
  "defense": 130,
  "height": 0.5,
  "type": "grass"
}
Fetched 5 record(s) in 4ms

```