# MongoDB - Aula 05 - Exercício
autor: Carol Dias

## Importar as collections restaurantes e pokemons

```
mongoimport --host 127.0.0.1 --db be-mean --collection restaurantes --drop --file restaurantes.json
2016-08-09T01:27:37.557+0000    connected to: 127.0.0.1
2016-08-09T01:27:37.558+0000    dropping: be-mean.restaurantes
2016-08-09T01:27:40.569+0000    [#####################...] be-mean.restaurantes 10.0 MB/11.3 MB (88.6%)
2016-08-09T01:27:40.921+0000    imported 25359 documents

mongoimport --host 127.0.0.1 --db be-mean --collection pokemons --drop --file pokemons.json
2016-08-09T01:28:45.419+0000    connected to: 127.0.0.1
2016-08-09T01:28:45.422+0000    dropping: be-mean.pokemons
2016-08-09T01:28:45.496+0000    imported 610 documents

```

## Distinct por `cuisine` na collection restaurantes

```
be-mean> db.restaurantes.distinct('cuisine')

[
  "Bakery",
  "Hamburgers",
  "Irish",
  "American ",
  "Jewish/Kosher",
  "Delicatessen",
  "Ice Cream, Gelato, Yogurt, Ices",
  "Chinese",
  "Other",
  "Chicken",
  "Turkish",
  "Caribbean",
  "Donuts",
  "Sandwiches/Salads/Mixed Buffet",
  "Bagels/Pretzels",
  "Continental",
  "Pizza",
  "Italian",
  "Steak",
  "Polish",
  "Latin (Cuban, Dominican, Puerto Rican, South & Central American)",
  "German",
  "French",
  "Pizza/Italian",
  "Mexican",
  "Spanish",
  "Café/Coffee/Tea",
  "Tex-Mex",
  "Pancakes/Waffles",
  "Soul Food",
  "Seafood",
  "Hotdogs",
  "Greek",
  "Not Listed/Not Applicable",
  "African",
  "Japanese",
  "Indian",
  "Armenian",
  "Thai",
  "Chinese/Cuban",
  "Mediterranean",
  "Korean",
  "Bottled beverages, including water, sodas, juices, etc.",
  "Russian",
  "Eastern European",
  "Middle Eastern",
  "Asian",
  "Ethiopian",
  "Vegetarian",
  "Barbecue",
  "Egyptian",
  "English",
  "Sandwiches",
  "Portuguese",
  "Indonesian",
  "Chinese/Japanese",
  "Filipino",
  "Juice, Smoothies, Fruit Salads",
  "Brazilian",
  "Afghan",
  "Vietnamese/Cambodian/Malaysia",
  "CafÃ©/Coffee/Tea",
  "Soups & Sandwiches",
  "Tapas",
  "Moroccan",
  "Pakistani",
  "Peruvian",
  "Bangladeshi",
  "Czech",
  "Salads",
  "Creole",
  "Fruits/Vegetables",
  "Iranian",
  "Cajun",
  "Scandinavian",
  "Polynesian",
  "Soups",
  "Australian",
  "Hotdogs/Pretzels",
  "Southwestern",
  "Nuts/Confectionary",
  "Hawaiian",
  "Creole/Cajun",
  "Californian",
  "Chilean"
]

```

## Distinct por `types` na collection pokemons

```
be-mean> db.pokemons.distinct('types')

[
  "normal",
  "fire",
  "water",
  "bug",
  "flying",
  "poison",
  "electric",
  "steel",
  "ice",
  "ghost",
  "fighting",
  "psychic",
  "grass",
  "ground",
  "fairy",
  "rock",
  "dark",
  "dragon"
]

```

## As primeiras 3 páginas com .limit() e .skip() de pokemons (5 em 5)

```
### be-mean> db.pokemons.find({}, {_id: 0, name: 1}).limit(5).skip(5 * 0)
{
  "name": "Rattata"
}
{
  "name": "Charmander"
}
{
  "name": "Charmeleon"
}
{
  "name": "Wartortle"
}
{
  "name": "Blastoise"
}

Fetched 5 record(s) in 8ms

### be-mean> db.pokemons.find({}, {_id: 0, name: 1}).limit(5).skip(5 * 1)
{
  "name": "Caterpie"
}
{
  "name": "Metapod"
}
{
  "name": "Butterfree"
}
{
  "name": "Spearow"
}
{
  "name": "Kakuna"
}

Fetched 5 record(s) in 1ms


###  be-mean> db.pokemons.find({}, {_id: 0, name: 1}).limit(5).skip(5 * 2)
{
  "name": "Farfetchd"
}
{
  "name": "Magnemite"
}
{
  "name": "Magneton"
}
{
  "name": "Doduo"
}
{
  "name": "Seel"
}

Fetched 5 record(s) in 3ms

```

## Group ou Aggregate contando a quantidade de pokemons de cada tipo

```
be-mean > db.pokemons.aggregate([{ $unwind: '$types' }, { $group: { _id: '$types', count: { $sum: 1 }} }])

```

## Realizar 3 counts na collection pokemons

```
### todos

be-mean> db.pokemons.count()
610

### apenas tipo fire

be-mean> db.pokemons.count({types: /fire/i})
47

### que possuem a defesa maior que 70 

be-mean> db.pokemons.count({defense: {$gt: 70}})
250

```