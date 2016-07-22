# MongoDB - Aula 03 - Exercício
autor: Carol Dias

## Liste todos Pokemons com a altura **menor que** 0.5;

```

be-mean-pokemons> var query = {height: {$lt: 0.5}}
be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("578c1e6459b655207c785513"),
  "name": "Eevee",
  "description": "Eevee has an unstable genetic makeup that suddenly mutates due to the environment in which it lives",
  "attack": 55,
  "defense": 0,
  "height": 0.3,
  "type": "normal"
}
Fetched 1 record(s) in 1ms

```

## Liste todos Pokemons com a altura **maior ou igual que** 0.5

```
be-mean-pokemons> var query = {height: {$gte: 0.5}}
be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("579184c39132d860eb7c429c"),
  "name": "Leafeon",
  "description": "When you see Leafeon asleep in a patch of sunshine, you'll know it is using photosynthesis to produce clean air",
  "attack": 110,
  "defense": 130,
  "height": 1,
  "type": "grass"
}
{
  "_id": ObjectId("578c21c0e9335233cf500f4a"),
  "name": "Jolteon",
  "description": "Jolteon's cells generate a low level of electricity",
  "attack": 130,
  "defense": 60,
  "height": 0.8,
  "type": "electric"
}
{
  "_id": ObjectId("578c1f7759b655207c785514"),
  "name": "Vaporeon",
  "description": "Vaporeon underwent a spontaneous mutation and grew fins and gills that allow it to live underwater",
  "attack": 65,
  "defense": 60,
  "height": 1,
  "type": "water"
}
{
  "_id": ObjectId("578c2384e9335233cf500f4b"),
  "name": "Flareon",
  "description": "Flareon's fluffy fur has a functional purpose - it releases heat into the air so that its body does not get excessively hot",
  "attack": 130,
  "defense": 60,
  "height": 0.9,
  "type": "fire"
}
{
  "_id": ObjectId("578c2441e9335233cf500f4c"),
  "name": "Umbreon",
  "description": "Umbreon evolved as a result of exposure to the moon's waves",
  "attack": 65,
  "defense": 110,
  "height": 1,
  "type": "dark"
}
Fetched 5 record(s) in 7ms

```

## Liste todos Pokemons com a altura **menor ou igual que** 1 (adaptado :p) **E** do tipo grama

```
be-mean-pokemons> var query = {$and: [{height: {$lte: 1}}, {type: 'grass'}]}
be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("579184c39132d860eb7c429c"),
  "name": "Leafeon",
  "description": "When you see Leafeon asleep in a patch of sunshine, you'll know it is using photosynthesis to produce clean air",
  "attack": 110,
  "defense": 130,
  "height": 1,
  "type": "grass"
}
Fetched 1 record(s) in 1ms

```

## Liste todos Pokemons com o name `Umbreon` (adaptado :p) **OU** com attack **menor ou igual que** 0.5

```
be-mean-pokemons> var query = {$or: [{name: 'Umbreon'}, {attack: {$lte: 0.5}}]}
be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("578c2441e9335233cf500f4c"),
  "name": "Umbreon",
  "description": "Umbreon evolved as a result of exposure to the moon's waves",
  "attack": 65,
  "defense": 110,
  "height": 1,
  "type": "dark"
}
Fetched 1 record(s) in 1ms

```

## Liste todos Pokemons com o attack **MAIOR OU IGUAL QUE** 48 **E** com  height **menor ou igual que** 0.5

```
be-mean-pokemons> var query = {$and: [{attack: {$gte: 48}}, {height: {$lte: 0.5}}]}
be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("578c1e6459b655207c785513"),
  "name": "Eevee",
  "description": "Eevee has an unstable genetic makeup that suddenly mutates due to the environment in which it lives",
  "attack": 55,
  "defense": 0,
  "height": 0.3,
  "type": "normal"
}
Fetched 1 record(s) in 5ms

```