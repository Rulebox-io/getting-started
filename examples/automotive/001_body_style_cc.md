# RBx Examples Automotive 001

## Description
Defines a vehicle object and rule that searchs for an Estate with Engine CC greater than 2000.

## RuleSet
```
{
  "ruleset":
    {
      "entity": { "make": "Text", "model": "Text", "bodyStyle": "Text","engineCC": "Number"  },
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