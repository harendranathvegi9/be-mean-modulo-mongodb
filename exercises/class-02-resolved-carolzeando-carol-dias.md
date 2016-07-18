# MongoDB - Aula 02 - Exercício
autor: Carol Dias

## Crie a database be-mean-pokemons

```
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-instagram> use be-mean-pokemons
switched to db be-mean-pokemons

```

## Listagem das databases (passo 2)

```
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> show dbs
be-mean-instagram → 0.078GB
be-mean           → 0.078GB
local             → 0.078GB

```

## Listagem das coleções (passo 3)

```
vagrant-ubuntu-trusty-64(mongod-3.0.7) be-mean-pokemons> show collections

```

## Cadastro dos pokemons (passo 4)

```

be-mean-pokemons> db.pokemons.insert({name: 'Eevee', description: "Eevee has an unstable genetic makeup that suddenly mutates due to the environment in which it lives.", attack: 55, defense: 0, height: 1.0})
Inserted 1 record(s) in 4ms

be-mean-pokemons> db.pokemons.insert({name: 'Vaporeon', description: "Vaporeon underwent a spontaneous mutation and grew fins and gills that allow it to live underwater", attack: 65, defense: 60, height: 3.03})
Inserted 1 record(s) in 1ms

be-mean-pokemons> db.pokemons.insert({name: 'Jolteon', description: "Jolteon's cells generate a low level of electricity", attack: 130, defense: 60, height: 2.11})
Inserted 1 record(s) in 1ms

be-mean-pokemons> db.pokemons.insert({name: 'Flareon', description: "Flareon's fluffy fur has a functional purpose - it releases heat into the air so that its body does not get excessively hot", attack: 130, defense: 60, height: 2.11})
Inserted 1 record(s) in 2ms

be-mean-pokemons> db.pokemons.insert({name: 'Umbreon', description: "Umbreon evolved as a result of exposure to the moon's waves", attack: 65, defense: 110, height: 3.03})
Inserted 1 record(s) in 1ms

```

## Lista dos pokemons (passo 5)

```
be-mean-pokemons> db.pokemons.find()
{
  "_id": ObjectId("578c1e6459b655207c785513"),
  "name": "Eevee",
  "description": "Eevee has an unstable genetic makeup that suddenly mutates due to the environment in which it lives.",
  "attack": 55,
  "defense": 0,
  "height": 1
}
{
  "_id": ObjectId("578c1f7759b655207c785514"),
  "name": "Vaporeon",
  "description": "Vaporeon underwent a spontaneous mutation and grew fins and gills that allow it to live underwater",
  "attack": 65,
  "defense": 60,
  "height": 3.03
}
{
  "_id": ObjectId("578c21c0e9335233cf500f4a"),
  "name": "Jolteon",
  "description": "Jolteon's cells generate a low level of electricity",
  "attack": 130,
  "defense": 60,
  "height": 2.11
}
{
  "_id": ObjectId("578c2384e9335233cf500f4b"),
  "name": "Flareon",
  "description": "Flareon's fluffy fur has a functional purpose - it releases heat into the air so that its body does not get excessively hot",
  "attack": 130,
  "defense": 60,
  "height": 2.11
}
{
  "_id": ObjectId("578c2441e9335233cf500f4c"),
  "name": "Umbreon",
  "description": "Umbreon evolved as a result of exposure to the moon's waves",
  "attack": 65,
  "defense": 110,
  "height": 3.03
}
Fetched 5 record(s) in 2ms

```

## Buscando o Eevee (passo 6)

```
be-mean-pokemons> var poke = db.pokemons.findOne({name:'Eevee'})

```

## Atualização do Eevee (passo 6)

```
be-mean-pokemons> poke.description = "Eevee has an unstable genetic makeup that suddenly mutates due to the environment in which it lives"
be-mean-pokemons> db.pokemons.save(poke)
Updated 1 existing record(s) in 1ms

```