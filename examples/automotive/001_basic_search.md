# RBx Examples - Automotive 001, Basic Search

## Description
Defines a vehicle object. The rule tests the fuel type equals a value, the year is between two values and the bodystyle is in a list of provided values.


## Examples of
- In
- Between
- Equals

## RuleSet
```json
{
    "ruleset": {
        "entity": {
            "make": "Text",
            "model": "Text",
            "bodyStyle": "Text",
            "year": "Number",
            "fuelType": "Text"
        },
        "rules": [
            {
                "predicate": {
                    "@year": {
                        "$between": [
                            2015,
                            2019
                        ]
                    },
                    "@bodyStyle": {
                        "$in": [
                            "Hatchback",
                            "Estate"
                        ]
                    },
                    "@fuelType": "Petrol"
                },
                "outcome": true,
                "stop": true
            }
        ]
    }
}
```

## Entity Examples
```json
{
    "make": "Ford",
    "model": "Fiesta",
    "bodyStyle": "Hatchback",
    "year": 2022,
    "fuelType": "Petrol"
}
```
## Match Request Example
###  Request Body
```json
{
    "testobj": {
        "make": "Ford",
        "model": "Fiesta",
        "bodyStyle": "Hatchback",
        "year": 2022,
        "fuelType": "Petrol"
    }
}
```
###  Response Body
```json
{
    "isMatch": false
}
```
## All Request Example
###  Request Body
```json
{
    "testobjs": [
        {
            "make": "Ford",
            "model": "Fiesta",
            "bodyStyle": "Hatchback",
            "year": 2019,
            "fuelType": "Petrol"
        },
        {
            "make": "Vauxhall",
            "model": "Corsa",
            "bodyStyle": "Hatchback",
            "year": 2016,
            "fuelType": "Petrol"
        },
        {
            "make": "Audi",
            "model": "A6",
            "bodyStyle": "Estate",
            "year": 2016,
            "fuelType": "Diesel"
        }
    ]
}
```
###  Response Body
```json
[
    {
        "make": "Ford",
        "model": "Fiesta",
        "bodyStyle": "Hatchback",
        "year": 2019,
        "fuelType": "Petrol",
    },
    {
        "make": "Vauxhall",
        "model": "Corsa",
        "bodyStyle": "Hatchback",
        "year": 2016,
        "fuelType": "Petrol",
    },
]
```

## First Request Example
###  Request Body
```json
{
    "testobjs": [
        {
            "make": "Ford",
            "model": "Fiesta",
            "bodyStyle": "Hatchback",
            "year": 2019,
            "fuelType": "Petrol"
        },
        {
            "make": "Vauxhall",
            "model": "Corsa",
            "bodyStyle": "Hatchback",
            "year": 2016,
            "fuelType": "Petrol"
        },
        {
            "make": "Audi",
            "model": "A6",
            "bodyStyle": "Estate",
            "year": 2016,
            "fuelType": "Diesel"
        }
    ]
}
```
###  Response Body
```json
{
    "make": "Ford",
    "model": "Fiesta",
    "bodyStyle": "Hatchback",
    "year": 2019,
    "fuelType": "Petrol",
}
```