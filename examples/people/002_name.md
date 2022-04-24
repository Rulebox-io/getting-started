# RBx Examples - People 002, Name

## Description
Defines a person object, the rules look for a person with a last name of *Smith* where the first name is not *John*.


## Examples of
- Equals
- Not

## RuleSet
```json
{
    "ruleset": {
        "entity": {
            "firstName": "Text",
            "lastName": "Text"
        },
        "rules": [
            {
                "predicate": {
                    "$not": {
                        "@firstName": "John"
                    },
                    "@lastName": "Smith"
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
    "firstName": "John",
    "id": "Smith"
}
```
## Match Request Example
###  Request Body
```json
{
    "testobj": {
        "firstName": "John",
        "lastName": "Smith"
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
            "firstName": "John",
            "lastName": "Smith"
        },
        {
            "firstName": "Dave",
            "lastName": "Smith"
        },
        {
            "firstName": "John",
            "lastName": "Jackson"
        },
        {
            "firstName": "Mike",
            "lastName": "Smith"
        }
    ]
}
```
###  Response Body
```json
[
    {
        "firstName": "Dave",
        "lastName": "Smith",
    },
    {
        "firstName": "Mike",
        "lastName": "Smith",
    },
]
```

## First Request Example
###  Request Body
```json
{
    "testobjs": [
        {
            "firstName": "John",
            "lastName": "Smith"
        },
        {
            "firstName": "Dave",
            "lastName": "Smith"
        },
        {
            "firstName": "John",
            "lastName": "Jackson"
        },
        {
            "firstName": "Mike",
            "lastName": "Smith"
        }
    ]
}
```
###  Response Body
```json
{
    "firstName": "Dave",
    "lastName": "Smith",
}
```