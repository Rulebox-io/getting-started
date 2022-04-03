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
        "age": "Number", 
        "race_results":
                {
                  "dataType": "Array", 
                  "of": 
                  { 
                      "stroke": "Text", 
                      "length_metres": "Number", 
                      "time_seconds": "Number" 
                  }
                } 
      },
      "rules": 
      [                          
          { 
              "predicate":
              { 
                "@race_results": { "$some": { "@stroke": "Freestyle" } } 
              },
              "outcome": true,
              "stop": true
          }
      ]
    }
}
```

## Entity Examples
```
{ 
  "name": "Fred", 
  "age": 15, 
  "galas": 
  [
    {
      "location": "Darlington",
      "date" : "01/01/2022",
      "races" :
      [
        {
            "stroke": "Freestyle",
            "length_metres": 50,
            "time_seconds": 35
        }
      ]
    }
  ],  
}
```
```
{ 
  "name": "Arthur", 
  "age": 15, 
  "galas": 
  [
    {
      "location": "Darlington",
      "date" : "01/01/2022",
      "races" :
      [
        {
            "stroke": "Freestyle",
            "length_metres": 50,
            "time_seconds": 45
        }
      ]
    }
  ],  
}

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