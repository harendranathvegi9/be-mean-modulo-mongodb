# MongoDB - Aula 06 - Exercício
autor: Caroline Dias

#1. Fazer uma query para o campo name utilizando explain para ver o resultado da busca

```
be-mean> db.restaurantes.find({name: 'Morris Park Bake Shop'}).explain('executionStats')
{
  "queryPlanner": {
    "plannerVersion": 1,
    "namespace": "be-mean.restaurantes",
    "indexFilterSet": false,
    "parsedQuery": {
      "name": {
        "$eq": "Morris Park Bake Shop"
      }
    },
    "winningPlan": {
      "stage": "COLLSCAN",
      "filter": {
        "name": {
          "$eq": "Morris Park Bake Shop"
        }
      },
      "direction": "forward"
    },
    "rejectedPlans": [ ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "executionTimeMillis": 19,
    "totalKeysExamined": 0,
    "totalDocsExamined": 25359,
    "executionStages": {
      "stage": "COLLSCAN",
      "filter": {
        "name": {
          "$eq": "Morris Park Bake Shop"
        }
      },
      "nReturned": 1,
      "executionTimeMillisEstimate": 10,
      "works": 25361,
      "advanced": 1,
      "needTime": 25359,
      "needFetch": 0,
      "saveState": 198,
      "restoreState": 198,
      "isEOF": 1,
      "invalidates": 0,
      "direction": "forward",
      "docsExamined": 25359
    }
  }
  "ok": 1
}

```

#2. Criar index para name e refazer a query para o campo name utilizando explain para ver o resultado da busca

```
be-mean> db.restaurantes.createIndex({name: 1})

be-mean>db.restaurantes.find({name: 'Morris Park Bake Shop'}).explain('executionStats')
{
  "queryPlanner": {
    "plannerVersion": 1,
    "namespace": "be-mean.restaurantes",
    "indexFilterSet": false,
    "parsedQuery": {
      "name": {
        "$eq": "Morris Park Bake Shop"
      }
    },
    "winningPlan": {
      "stage": "FETCH",
      "inputStage": {
        "stage": "IXSCAN",
        "keyPattern": {
          "name": 1
        },
        "indexName": "name_1",
        "isMultiKey": false,
        "direction": "forward",
        "indexBounds": {
          "name": [
            "[\"Morris Park Bake Shop\", \"Morris Park Bake Shop\"]"
          ]
        }
      }
    },
    "rejectedPlans": [ ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "executionTimeMillis": 0,
    "totalKeysExamined": 1,
    "totalDocsExamined": 1,
    "executionStages": {
      "stage": "FETCH",
      "nReturned": 1,
      "executionTimeMillisEstimate": 0,
      "works": 2,
      "advanced": 1,
      "needTime": 0,
      "needFetch": 0,
      "saveState": 0,
      "restoreState": 0,
      "isEOF": 1,
      "invalidates": 0,
      "docsExamined": 1,
      "alreadyHasObj": 0,
      "inputStage": {
        "stage": "IXSCAN",
        "nReturned": 1,
        "executionTimeMillisEstimate": 0,
        "works": 2,
        "advanced": 1,
        "needTime": 0,
        "needFetch": 0,
        "saveState": 0,
        "restoreState": 0,
        "isEOF": 1,
        "invalidates": 0,
        "keyPattern": {
          "name": 1
        },
        "indexName": "name_1",
        "isMultiKey": false,
        "direction": "forward",
        "indexBounds": {
          "name": [
            "[\"Morris Park Bake Shop\", \"Morris Park Bake Shop\"]"
          ]
        },
        "keysExamined": 1,
        "dupsTested": 0,
        "dupsDropped": 0,
        "seenInvalidated": 0,
        "matchTested": 0
      }
    }
  },
  "ok": 1
}


```

#3. Fazer uma query para dois campos juntos utilizando explain para ver o resultado da busca

```
be-mean> db.restaurantes.find({$and: [{name: 'Morris Park Bake Shop'}, {borough: 'Bronx'}]}).explain('executionStats')
{
  "queryPlanner": {
    "plannerVersion": 1,
    "namespace": "be-mean.restaurantes",
    "indexFilterSet": false,
    "parsedQuery": {
      "$and": [
        {
          "borough": {
            "$eq": "Bronx"
          }
        },
        {
          "name": {
            "$eq": "Morris Park Bake Shop"
          }
        }
      ]
    },
    "winningPlan": {
      "stage": "COLLSCAN",
      "filter": {
        "$and": [
          {
            "borough": {
              "$eq": "Bronx"
            }
          },
          {
            "name": {
              "$eq": "Morris Park Bake Shop"
            }
          }
        ]
      },
      "direction": "forward"
    },
    "rejectedPlans": [ ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "executionTimeMillis": 23,
    "totalKeysExamined": 0,
    "totalDocsExamined": 25359,
    "executionStages": {
      "stage": "COLLSCAN",
      "filter": {
        "$and": [
          {
            "borough": {
              "$eq": "Bronx"
            }
          },
          {
            "name": {
              "$eq": "Morris Park Bake Shop"
            }
          }
        ]
      },
      "nReturned": 1,
      "executionTimeMillisEstimate": 20,
      "works": 25361,
      "advanced": 1,
      "needTime": 25359,
      "needFetch": 0,
      "saveState": 198,
      "restoreState": 198,
      "isEOF": 1,
      "invalidates": 0,
      "direction": "forward",
      "docsExamined": 25359
    }
  },
  "ok": 1
}

```

#4. Criar index composto e refazer a query para os dois campos juntos utilizando explain para ver o resultado da busca

```
be-mean> db.restaurantes.createIndex({name: 1, borough: 1})
be-mean> db.restaurantes.find({$and: [{name: 'Morris Park Bake Shop'}, {borough: 'Bronx'}]}).explain('executionStats')
{
  "queryPlanner": {
    "plannerVersion": 1,
    "namespace": "be-mean.restaurantes",
    "indexFilterSet": false,
    "parsedQuery": {
      "$and": [
        {
          "borough": {
            "$eq": "Bronx"
          }
        },
        {
          "name": {
            "$eq": "Morris Park Bake Shop"
          }
        }
      ]
    },
    "winningPlan": {
      "stage": "FETCH",
      "inputStage": {
        "stage": "IXSCAN",
        "keyPattern": {
          "name": 1,
          "borough": 1
        },
        "indexName": "name_1_borough_1",
        "isMultiKey": false,
        "direction": "forward",
        "indexBounds": {
          "name": [
            "[\"Morris Park Bake Shop\", \"Morris Park Bake Shop\"]"
          ],
          "borough": [
            "[\"Bronx\", \"Bronx\"]"
          ]
        }
      }
    },
    "rejectedPlans": [ ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "executionTimeMillis": 0,
    "totalKeysExamined": 1,
    "totalDocsExamined": 1,
    "executionStages": {
      "stage": "FETCH",
      "nReturned": 1,
      "executionTimeMillisEstimate": 0,
      "works": 2,
      "advanced": 1,
      "needTime": 0,
      "needFetch": 0,
      "saveState": 0,
      "restoreState": 0,
      "isEOF": 1,
      "invalidates": 0,
      "docsExamined": 1,
      "alreadyHasObj": 0,
      "inputStage": {
        "stage": "IXSCAN",
        "nReturned": 1,
        "executionTimeMillisEstimate": 0,
        "works": 2,
        "advanced": 1,
        "needTime": 0,
        "needFetch": 0,
        "saveState": 0,
        "restoreState": 0,
        "isEOF": 1,
        "invalidates": 0,
        "keyPattern": {
          "name": 1,
          "borough": 1
        },
        "indexName": "name_1_borough_1",
        "isMultiKey": false,
        "direction": "forward",
        "indexBounds": {
          "name": [
            "[\"Morris Park Bake Shop\", \"Morris Park Bake Shop\"]"
          ],
          "borough": [
            "[\"Bronx\", \"Bronx\"]"
          ]
        },
        "keysExamined": 1,
        "dupsTested": 0,
        "dupsDropped": 0,
        "seenInvalidated": 0,
        "matchTested": 0
      }
    }
  },
  "ok": 1
}


```