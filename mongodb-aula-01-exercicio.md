# MongoDB - Aula 01 - Exercício
autor: Caroline Dias

## Importando os restaurantes

    ```
    PS C:\projects\be-mean\mongodb\aula-1> mongoimport --db be-mean --collection restaurantes --drop --file restaurantes.json
    2015-11-09T23:52:24.229-0200    connected to: localhost
    2015-11-09T23:52:24.247-0200    dropping: be-mean.restaurantes
    2015-11-09T23:52:26.576-0200    imported 25359 documents

    ```

## Contando os restaurantes

    ```
    PS C:\projects\be-mean\mongodb\aula-1> mongo be-mean
    MongoDB shell version: 3.0.7
    connecting to: be-mean
    > db.restaurantes.find({}).count()
    25359

    ```