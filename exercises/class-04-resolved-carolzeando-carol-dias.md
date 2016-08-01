# MongoDB - Aula 04 - Exercício
autor: Carol Dias

## **Adicionar** 2 ataques ao mesmo tempo para os seguintes pokemons: Vaporeon, Leafeon, Umbreon e Glaceon.

```
be-mean-pokemons> var query = {name: /vaporeon/i}
be-mean-pokemons> var mod = {$pushAll: {moves: ['Quick Attack', 'Water Pulse']}}
be-mean-pokemons> db.pokemons.update(query, mod)

be-mean-pokemons> var query = {name: /leafeon/i}
be-mean-pokemons> var mod = {$pushAll: {moves: ['Quick Attack', 'Giga Drain']}}
be-mean-pokemons> db.pokemons.update(query, mod)

be-mean-pokemons> var query = {name: /umbreon/i}
be-mean-pokemons> var mod = {$pushAll: {moves: ['Quick Attack', 'Pursuit']}}
be-mean-pokemons> db.pokemons.update(query, mod)

be-mean-pokemons> var query = {name: /glaceon/i}
be-mean-pokemons> var mod = {$pushAll: {moves: ['Quick Attack', 'Ice Fang']}}
be-mean-pokemons> db.pokemons.update(query, mod)

```

## **Adicionar** 1 movimento em todos os pokemons: `desvio`.##
```
be-mean-pokemons> var mod = {$push: {moves: 'Desvio'}}
be-mean-pokemons> var opt = {multi: true}
be-mean-pokemons> db.pokemons.update({}, mod, opt)

Updated 7 existing record(s) in 1ms
WriteResult({
  "nMatched": 7,
  "nUpserted": 0,
  "nModified": 7
})

```

## **Adicionar** o pokemon `AindaNaoExisteMon` caso ele não exista com todos os dados com o valor `null` e a descrição: "Sem maiores informações".##
```

be-mean-pokemons> var query = {name: /AindaNaoExisteMon/i}
be-mean-pokemons> var mod = {
	$setOnInsert:
	{
		name: 'AindaNaoExisteMon',
		description: 'Sem maiores informações',
		attack: null,
		defense: null,
		height: null,
		type: null
	}
}

be-mean-pokemons> var opt = {upsert: true}
be-mean-pokemons> db.pokemons.update(query, mod, opt)

Updated 1 new record(s) in 6ms
WriteResult({
  "nMatched": 0,
  "nUpserted": 1,
  "nModified": 0,
  "_id": ObjectId("579ea27a1b58436dfda30e7e")
})

```

## Pesquisar todos o pokemons que possuam o ataque `Quick Attack` e mais um que você adicionou, escolha seu pokemon favorito.##
```
be-mean-pokemons> var query = {moves: {$in: [/quick attack/i, /pursuit/i]}}
be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("579184c39132d860eb7c429c"),
  "name": "Leafeon",
  "description": "When you see Leafeon asleep in a patch of sunshine, you'll know it is using photosynthesis to produce clean air",
  "attack": 110,
  "defense": 130,
  "height": 1,
  "type": "grass",
  "moves": [
    "Quick Attack",
    "Giga Drain",
    "Desvio"
  ]
}
{
  "_id": ObjectId("578c1f7759b655207c785514"),
  "name": "Vaporeon",
  "description": "Vaporeon underwent a spontaneous mutation and grew fins and gills that allow it to live underwater",
  "attack": 65,
  "defense": 60,
  "height": 1,
  "type": "water",
  "moves": [
    "Quick Attack",
    "Water Pulse",
    "Desvio"
  ]
}
{
  "_id": ObjectId("5795405a9e8c756a92975aa0"),
  "name": "Glaceon",
  "description": "By controlling its body heat, it can freeze the atmosphere around it to make a diamond-dust flurry",
  "attack": 60,
  "defense": 110,
  "height": 0.8,
  "type": "ice",
  "moves": [
    "Quick Attack",
    "Ice Fang",
    "Desvio"
  ]
}
{
  "_id": ObjectId("578c2441e9335233cf500f4c"),
  "name": "Umbreon",
  "description": "Umbreon evolved as a result of exposure to the moon's waves",
  "attack": 65,
  "defense": 110,
  "height": 1,
  "type": "dark",
  "moves": [
    "Quick Attack",
    "Pursuit",
    "Desvio"
  ]
}

Fetched 4 record(s) in 8ms

```

## Pesquisar **todos** os pokemons que possuam os ataques que você adicionou, escolha seu pokemon favorito.##
```
be-mean-pokemons> var query = {moves: {$in: [/pursuit/i]}}
be-mean-pokemons> db.pokemons.find(query)

{
  "_id": ObjectId("578c2441e9335233cf500f4c"),
  "name": "Umbreon",
  "description": "Umbreon evolved as a result of exposure to the moon's waves",
  "attack": 65,
  "defense": 110,
  "height": 1,
  "type": "dark",
  "moves": [
    "Quick Attack",
    "Pursuit",
    "Desvio"
  ]
}

Fetched 1 record(s) in 1ms

```

## Pesquisar **todos** os pokemons que não são do tipo `elétrico`.##
```
be-mean-pokemons> var query = {type: {$not: /electric/i}}
be-mean-pokemons> db.pokemons.find(query) 

{
  "_id": ObjectId("578c2384e9335233cf500f4b"),
  "name": "Flareon",
  "description": "Flareon's fluffy fur has a functional purpose - it releases heat into the air so that its body does not get excessively hot",
  "attack": 130,
  "defense": 60,
  "height": 0.9,
  "type": "fire",
  "moves": [
    "Desvio"
  ]
}
{
  "_id": ObjectId("579184c39132d860eb7c429c"),
  "name": "Leafeon",
  "description": "When you see Leafeon asleep in a patch of sunshine, you'll know it is using photosynthesis to produce clean air",
  "attack": 110,
  "defense": 130,
  "height": 1,
  "type": "grass",
  "moves": [
    "Quick Attack",
    "Giga Drain",
    "Desvio"
  ]
}
{
  "_id": ObjectId("578c1e6459b655207c785513"),
  "name": "Eevee",
  "description": "Eevee has an unstable genetic makeup that suddenly mutates due to the environment in which it lives",
  "attack": 55,
  "defense": 0,
  "height": 0.3,
  "type": "normal",
  "moves": [
    "Desvio"
  ]
}
{
  "_id": ObjectId("578c1f7759b655207c785514"),
  "name": "Vaporeon",
  "description": "Vaporeon underwent a spontaneous mutation and grew fins and gills that allow it to live underwater",
  "attack": 65,
  "defense": 60,
  "height": 1,
  "type": "water",
  "moves": [
    "Quick Attack",
    "Water Pulse",
    "Desvio"
  ]
}
{
  "_id": ObjectId("5795405a9e8c756a92975aa0"),
  "name": "Glaceon",
  "description": "By controlling its body heat, it can freeze the atmosphere around it to make a diamond-dust flurry",
  "attack": 60,
  "defense": 110,
  "height": 0.8,
  "type": "ice",
  "moves": [
    "Quick Attack",
    "Ice Fang",
    "Desvio"
  ]
}
{
  "_id": ObjectId("578c2441e9335233cf500f4c"),
  "name": "Umbreon",
  "description": "Umbreon evolved as a result of exposure to the moon's waves",
  "attack": 65,
  "defense": 110,
  "height": 1,
  "type": "dark",
  "moves": [
    "Quick Attack",
    "Pursuit",
    "Desvio"
  ]
}

Fetched 6 record(s) in 2ms

```

## Pesquisar **todos** os pokemons que tenham o ataque `Quick Attack` **E** tenham a defesa **não menor ou igual** a 49.##
```
be-mean-pokemons> var query = {$and: [{moves: {$in: [/quick attack/i]}}, {defense: {$not: {$lte: 49}}}]}
be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("579184c39132d860eb7c429c"),
  "name": "Leafeon",
  "description": "When you see Leafeon asleep in a patch of sunshine, you'll know it is using photosynthesis to produce clean air",
  "attack": 110,
  "defense": 130,
  "height": 1,
  "type": "grass",
  "moves": [
    "Quick Attack",
    "Giga Drain",
    "Desvio"
  ]
}
{
  "_id": ObjectId("578c1f7759b655207c785514"),
  "name": "Vaporeon",
  "description": "Vaporeon underwent a spontaneous mutation and grew fins and gills that allow it to live underwater",
  "attack": 65,
  "defense": 60,
  "height": 1,
  "type": "water",
  "moves": [
    "Quick Attack",
    "Water Pulse",
    "Desvio"
  ]
}
{
  "_id": ObjectId("5795405a9e8c756a92975aa0"),
  "name": "Glaceon",
  "description": "By controlling its body heat, it can freeze the atmosphere around it to make a diamond-dust flurry",
  "attack": 60,
  "defense": 110,
  "height": 0.8,
  "type": "ice",
  "moves": [
    "Quick Attack",
    "Ice Fang",
    "Desvio"
  ]
}
{
  "_id": ObjectId("578c2441e9335233cf500f4c"),
  "name": "Umbreon",
  "description": "Umbreon evolved as a result of exposure to the moon's waves",
  "attack": 65,
  "defense": 110,
  "height": 1,
  "type": "dark",
  "moves": [
    "Quick Attack",
    "Pursuit",
    "Desvio"
  ]
}

Fetched 4 record(s) in 12ms


```

## Remova **todos** os pokemons do tipo água e com attack menor que 50.
```
be-mean-pokemons> var query = {$and: [{type: /water/i}, {attack: {$lt: 50}}]}
be-mean-pokemons> db.pokemons.remove(query)
Removed 0 record(s) in 2ms
WriteResult({
  "nRemoved": 0
})

```
