# RBx Examples - People 001, Swimming Times

## Description
Defines a person object that represents a swimmer including competition entries and times. The rules check for ages, length and times in different strokes using a `startsWith` function.

## Examples of
- startsWith function
- Less than or equal to
- Equals
- Some

## RuleSet
```json
{
  "ruleset": {
    "entity": {
      "name": "Text",
      "age": "Number",
      "galas": {
        "dataType": "Array",
        "of": {
          "date": "DateTime",
          "races": {
            "dataType": "Array",
            "of": {
              "stroke": "Text",
              "length_metres": "Number",
              "time_seconds": "Number"
            }
          }
        }
      }
    },
    "rules": [
      {
        "predicate": {
          "@galas": {
            "$some": {
              "@races": {
                "$some": {
                  "@time_seconds": { "$lte": 40 },
                  "@length_metres": 50,
                  "$function": { "name": "startsWith", "arguments": [ "@stroke", "F" ] }
                }
              }
            }
          },
          "@age": { "$lte": 10 }          
        },
        "outcome": true,
        "stop": true
      },
      {
        "predicate": {
          "@galas": {
            "$some": {
              "@races": {
                "$some": {
                  "@time_seconds": { "$lte": 40 },
                  "@length_metres": 50,
                  "$function": { "name": "startsWith", "arguments": [ "@stroke", "B" ] }
                }
              }
            }
          },
          "@age": { "$lte": 10 }          
        },
        "outcome": true,
        "stop": true
      }
    ]
  }
}
```

## Entity Example
```json
{
    "name": "Fred",
    "age": 9,
    "galas": [
        {
            "location": "Darlington",
            "date": "01/01/2022",
            "races": [
                {
                    "stroke": "Butterfly",
                    "length_metres": 50,
                    "time_seconds": 20
                }
            ]
        }
    ]
}
```
## Match Request Example
###  Request Body
```json
{
    "testobj": {
        "name": "Fred",
        "age": 9,
        "galas": [
            {
                "location": "Darlington",
                "date": "01/01/2022",
                "races": [
                    {
                        "stroke": "Butterfly",
                        "length_metres": 50,
                        "time_seconds": 20
                    }
                ]
            }
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
            "name": "Fred",
            "age": 9,
            "galas": [
                {
                    "location": "Darlington",
                    "date": "01/01/2022",
                    "races": [
                        {
                            "stroke": "Butterfly",
                            "length_metres": 50,
                            "time_seconds": 20
                        }
                    ]
                }
            ]
        },
        {
            "name": "Jack",
            "age": 10,
            "galas": [
                {
                    "location": "Darlington",
                    "date": "01/01/2022",
                    "races": [
                        {
                            "stroke": "Freestyle",
                            "length_metres": 50,
                            "time_seconds": 20
                        }
                    ]
                }
            ]
        }
    ]
}
```
###  Response Body
```json
[
    {
        "name": "Jack",
        "age": 10,
        "galas": [
            {
                "date": "1/1/2022 12:00:00 AM",
                "races": [
                    {
                        "stroke": "Freestyle",
                        "length_metres": 50,
                        "time_seconds": 20,
                    },
                ],
            },
        ],
    },
    {
        "name": "Fred",
        "age": 9,
        "galas": [
            {
                "date": "1/1/2022 12:00:00 AM",
                "races": [
                    {
                        "stroke": "Butterfly",
                        "length_metres": 50,
                        "time_seconds": 20,
                    },
                ],
            },
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
            "name": "Fred",
            "age": 9,
            "galas": [
                {
                    "location": "Darlington",
                    "date": "01/01/2022",
                    "races": [
                        {
                            "stroke": "Butterfly",
                            "length_metres": 50,
                            "time_seconds": 20
                        }
                    ]
                }
            ]
        },
        {
            "name": "Jack",
            "age": 10,
            "galas": [
                {
                    "location": "Darlington",
                    "date": "01/01/2022",
                    "races": [
                        {
                            "stroke": "Freestyle",
                            "length_metres": 50,
                            "time_seconds": 20
                        }
                    ]
                }
            ]
        }
    ]
}
```
###  Response Body
```json
{
    "name": "Fred",
    "age": 9,
    "galas": [
        {
            "date": "1/1/2022 12:00:00 AM",
            "races": [
                {
                    "stroke": "Butterfly",
                    "length_metres": 50,
                    "time_seconds": 20,
                },
            ],
        },
    ],
}
```