# RBx Examples - Sport 001, Swimming Times

## Description
Defines a person object that represents a swimmer including competition entries and times. The rule check entities for 'Gold' medal times across the different races and age groups.

## RuleSet
```
{
  "ruleset":
    {
      "entity": 
      { 
        "name": "Text", 
        "age": "Numer", 
        "galas":
          { 
            "dataType": "Array", 
            "of": 
            { 
                "name": "Text", 
                "location": "Text", 
                "date": "DateTime" 
                "races":
                {
                  "dataType": "Array", 
                  "of": 
                  { 
                      "stroke": "Text", 
                      "length": "Number", 
                      "time": "Number" 
                  }
                }
            }
          }  
      },
      "rules": 
      [                          
          { 
              "predicate":{ "@engineCC": { "$gte" : 2000}, "@bodyStyle" : "Estate" },
              "outcome": true,
              "stop": true
          }
      ]
    }
}
```

## Entitie Examples
```
{ "make": "Audi", "model": "A6", "bodyStyle": "Estate",  "engineCC": 2050  }

{ "make": "Audi", "model": "A6", "bodyStyle": "Saloon",  "engineCC": 2050  }

{ "make": "Ford", "model": "Focus RS", "bodyStyle": "Hatchback",  "engineCC": 2200  }
```
## Match Request Example
###  Request Body
###  Response Body

## Any Request Example
###  Request Body
###  Response Body

## All Request Example
###  Request Body
###  Response Body