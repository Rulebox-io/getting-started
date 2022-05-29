# RBx Examples - Business Process 001, Max

## Description
Defines a business process and array of historic execution times, the rule checks whether the execution time is greater than the maximum historic execution times.


## Examples of
- Min Function
- Greater than
- Number Array

## RuleSet
```json
{
    "ruleset": {
        "entity": {
            "name": "Text",
            "id": "Text",
            "executionTime": "Number",
            "historicExecutionTimes": { "dataType": "Array", "of": "Number" }
        },
        "rules": [
            {
                "predicate": {
                    "@executionTime": { "$gt": {"$function": { "name": "max", "arguments": [ "@historicExecutionTimes" ] }}
                }},
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
    "name": "Process 1",
    "id": "P0001",
    "executionTime": 6.3,
    "historicExecutionTimes": [2.3,4.7,6.2]
}
```
## Match Request Example
###  Request Body
```json
{
    "testobj": {
        "name": "Process 1",
        "id": "P0001",
        "executionTime": 6.3,
        "historicExecutionTimes": [
            2.3,
            4.7,
            6.2
        ]
    }
}
```
###  Response Body
```json
{
    "isMatch": true
}
```
## All Request Example
###  Request Body
```json
{
    "testobjs": [
        {
            "name": "Process 1",
            "id": "P0001",
            "executionTime": 6.3,
            "historicExecutionTimes": [
                2.3,
                4.7,
                6.2
            ]
        },
        {
            "name": "Process 2",
            "id": "P0002",
            "executionTime": 10,
            "historicExecutionTimes": [
                2.3,
                4.7,
                6.2
            ]
        },
        {
            "name": "Process 3",
            "id": "P0003",
            "executionTime": 6.1,
            "historicExecutionTimes": [
                2.3,
                4.7,
                6.2
            ]
        }

    ]
}
```
###  Response Body
```json
[
    {
        "name": "Process 1",
        "id": "P0001",
        "executionTime": 6.3,
        "historicExecutionTimes": [
            2.3,
            4.7,
            6.2,
        ],
    },
    {
        "name": "Process 2",
        "id": "P0002",
        "executionTime": 10,
        "historicExecutionTimes": [
            2.3,
            4.7,
            6.2,
        ],
    },
]
```

## First Request Example
###  Request Body
```json
{
    "testobjs": [
        {
            "name": "Process 1",
            "id": "P0001",
            "executionTime": 6.3,
            "historicExecutionTimes": [
                2.3,
                4.7,
                6.2
            ]
        },
        {
            "name": "Process 2",
            "id": "P0002",
            "executionTime": 10,
            "historicExecutionTimes": [
                2.3,
                4.7,
                6.2
            ]
        },
        {
            "name": "Process 3",
            "id": "P0003",
            "executionTime": 6.1,
            "historicExecutionTimes": [
                2.3,
                4.7,
                6.2
            ]
        }

    ]
}
```
###  Response Body
```json
{
    "name": "Process 1",
    "id": "P0001",
    "executionTime": 6.3,
    "historicExecutionTimes": [
        2.3,
        4.7,
        6.2,
    ],
}
```