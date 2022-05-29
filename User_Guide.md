# RuleBox User Guide

## Table of contents
1. [Introduction](#introduction)
2. [Entity](#entity)
   1. [Property Types](#entityPropertyTypes)
      1. [Text](#entityPropertyTypeText)
      1. [Number](#entityPropertyTypeNumber)
      1. [DateTime](#entityPropertyTypeDateTime)
      1. [Boolean](#entityPropertyTypeBoolean)
      1. [Entity](#entityPropertyTypeEntity)
      1. [Array](#entityPropertyTypeArray)
3. [Rules](#rules)
   1. [Operators](#ruleOperators)
      1. [Equals](#ruleOperatorEquals)
      1. [Less Than](#ruleOperatorLT)
      1. [Less Than or Equal To](#ruleOperatorLTE)
      2. [Greater Than](#ruleOperatorGT)
      1. [Greater Than or Equal To](#ruleOperatorGTE)
      2. [Not](#ruleOperatorNot)
      3. [Some, All, None](#ruleOperatorAnyAllNone)
      4. [Is One Of](#ruleOperatorIsOneOf)
      5. [Contains](#ruleOperatorContains)
      6. [Between](#ruleOperatorBetween)
      7. [Logical And](#ruleOperatorAnd)
      8. [Logical Or](#ruleOperatorOr)
   2. [Functions](#functions)
      1. [Starts with](#ruleFunctionStartsWith)
      1. [To uppercase](#ruleFunctionToUpperCase)
      1. [Substring](#ruleFunctionSubStr)
      1. [Squareroot](#ruleFunctionSqrt)
      1. [Min](#ruleFunctionMin)
      1. [Max](#ruleFunctionMax)
      1. [Average](#ruleFunctionAvg)
      2. [Years from now](#ruleFunctionYearsFromNow)
4. [RuleSet](#ruleSet)
   1. [RBxId](#ruleSetRbxId)
   2. [Version](#ruleSetVersion)
   3. [IsDraft](#ruleSetDraft)
5. [APIs](#apis)
   1. [Compilation](#apisCompilation)
   2. [Execution](#apisExecution)
      1. [Match](#apisExecutionMatch)
      2. [All](#apisExecutionAll)
      3. [First](#apisExecutionFirst)
6. [Getting Started](#gettingStarted)
   1. [Define an Entity](#gettingStartedEntity)
   2. [Build some Rules](#gettingStartedRules)
   3. [Create a Ruleset](#gettingStartedRuleset)
   4. [Test the Entity objects](#gettingStartedTest)

## Introduction <a name="introduction"></a>
RuleBox is a SaaS Solution that allows you to create and execute business rules agaisnt your own entities objects. Use the RBx APIs to describe your entities and author rules, creating an RBx RuleSet. When you're ready you can pass entity objects to our APIs and we'll test them using your RuleSet.

## Entity <a name="entity"></a>
A RuleBox entity is a client defined object that RBx rules test agaisnt. It is made up of properties that are either primitive values,  entities themselves or an array.

Entities are defined as JSON, for example

```json
{ "name": "Text","age": "Number" ,"height": "Number"  }
```

Currently RuleBox supports the primitive data types listed below.

- text
- number
- datetime
- boolean

### Property Types <a name="entityPropertyTypes"></a>

#### Text <a name="entityPropertyTypeText"></a>
Defines a string value.
##### Example Definition
```json
{ "name": "Text" }
```

#### Number <a name="entityPropertyTypeNumber"></a>
Defines a numerical value, there is no distinction betweeen integers and decimal.
##### Example Definition
```json
{ "age": "Number" ,"height": "Number" }
```

#### DateTime <a name="entityPropertyTypeDateTime"></a>
Defines a datetime value.
##### Example Definition
```json
{ "dob": "DateTime" }
```

#### Boolean <a name="entityPropertyTypeBoolean"></a>
Defines a boolean value.
##### Example Definition
```json
{ "hasMot": "Boolean" }
```

#### Entities <a name="entityPropertyTypeEntity"></a>
Defines an entity value.
##### Example Definition
```json
{ "name": "Text", "house": { "Number": "Number", "Street": "Text" }}
```

#### Arrays <a name="entityPropertyTypeArray"></a>
An array defines a collection of primitive types or entities, nested arrays are also supported.
##### Example Definition (primitive type, text)
```json
 { "names": { "dataType": "Array", "of": "Text"}}
```
##### Example Definition (entity)
```json
  { "children": { "dataType": "Array", "of": { "Name": "Text", "Age": "Number" }}}
```
##### Example Definition (nested array)
```json
  { "grandchildren": { "dataType": "Array", "of": { "dataType": "Array", "of":  { "dataType": "Array", "of": { "name": "Text" }} }}}
```

## Rules <a name="rules"></a>
A rule is a conditional statement, defined in JSON, that is used to run tests against one or more entities. When a rule is executed agaisnt an entity it will analyse its properties looking for matches. 

RuleBox supports a number of operators which can be used to build rules.

### Operators <a name="ruleOperators"></a>
#### Equals <a name="ruleOperatorEquals"></a>
Tests whether the value of an entities property is equal to the value specified in the rule.
##### Format 
```json
{ "<field name>": <rule_test_value> }
```
##### Example (text) 
```json
{ "@name": "Rick" }
```
##### Example (number) 
```json
{ "@age": 25 }
```
##### Example (datetime) 
```json
{ "@dob": "09/01/01" }
```
##### Example (boolean) 
```json
{ "@hasMot": true }
```
#### Less than <a name="ruleOperatorLT"></a>
Tests whether the value of an entities property is less than the value specified in the rule. Can be applied to numbers or dateTimes.
##### Format 
```json
{ "<field name>": { "$lt": <rule_test_value> } }
```
##### Example (number) 
```json
{ "@age": { "$lt": 25 } }
```
##### Example (datetime) 
```json
{ "@dob": { "$lt": "09/01/01" } }
```
#### Less than or equal to <a name="ruleOperatorLTE"></a>
Tests whether the value of an entities property is less than or equal to the value specified in the rule. Can be applied to numbers or dateTimes.
##### Format 
```json
{ "<field name>": { "$lte": <rule_test_value> } }
```
##### Example (number) 
```json
{ "@age": { "$lte": 25 } }
```
##### Example (datetime) 
```json
{ "@dob": { "$lte": "09/01/01" } }
```
#### Greater than <a name="ruleOperatorGT"></a>
Tests whether the value of an entities property is greater than the value specified in the rule. Can be applied to numbers or dateTimes.
##### Format 
```json
{ "<field name>": { "$gt": <rule_test_value> } }
```
##### Example (number) 
```json
{ "@age": { "$gt": 25 } }
```
##### Example (datetime) 
```json
{ "@dob": { "$gt": "09/01/01" } }
```
#### Greater than or equal to <a name="ruleOperatorGTE"></a>
Tests whether the value of an entities property is greater than or equal to the value specified in the rule. Can be applied to numbers or dateTimes.
##### Format 
```json
{ "<field name>": { "$gte": <rule_test_value> } }
```
##### Example (number) 
```json
{ "@age": { "$gte": 25 } }
```
##### Example (datetime) 
```json
{ "@dob": { "$gte": "09/01/01" } }
```

#### Not <a name="ruleOperatorNot"></a>
The 'not' expression returns the inverse of a boolean result.
##### Format
```json
{ "$not": <boolean_expression> }
```
##### Example
```json
{ "$not": { "@code": "E" } }
```

#### Some, all, none <a name="ruleOperatorAnyAllNone"></a>
These operators test whether some, or all, or none of the elements in a field array match a specified value.
##### Format
```json
{ "<field name>": { "$some|$all|$none": <predicate_object> } }
```
##### Examples
```json
{ "@tags": { "$some": { "@code": { "$in": ["New", "Used"] } } } }
{ "@tags": { "$all": { "@code": { "$in": ["New", "Used"] } } } }
{ "@tags": { "$none": { "@code": "Used" } } }
```

#### Is one of <a name="ruleOperatorIsOneOf"></a>
This expression tests whether a field value is one of the values in an array.
##### Format
```json
{ "<field name>": { "$in": [<primitive>, <primitive>] } }
```
##### Example
```json
{ "@tag": { "$in": ["New", "Used"] } }
```

#### Contains <a name="ruleOperatorContains"></a>
This expression is the inverse of 'is one of' - it tests whether a field's array value contains a specified value. The field value must be an array, the expression tests whether a primitive value is one of the values in a field's array.

##### Format
```json
{ "<field name>": { "$contains": <primitive> } }
```

##### Example
```json
{ "tags": { "$contains": "Sick" } }
```
#### Between <a name="ruleOperatorBetween"></a>
This expression tests whether a field value is between two specified values (inclusive). Can be applied to numbers or dateTimes.
##### Format
```json
{ "<field name>": { "$between": [<number>, <number>] } }
```
##### Example
```json
{ "@from": { "$between": [20, 22] } }
```


#### Logical and <a name="ruleOperatorAnd"></a>
##### Format
```json
{ "<field name>": <expression>, "<field name>": <expression> [, ...] }
```
##### Example
```json
{
    "@from": { "$gt": 7 },
    "@from": { "$lte": 22 },
}
```
#### Logical or <a name="ruleOperatorOr"></a>
##### Format
```json
{ "$or": [ <expression> [, <expression> ] ]}
```
##### Example
```json
{
    "$or": [
        { "@code": "E" },
        { "@code": "L" }
    ]    
}
```

### Functions <a name="functions"></a>
As well as the standard operators that can be used to build rules RuleBox also includes a number of pre-built functions that can be included in Rules. Functions accept parameters which can be entity properties or an expression.

#### Starts with <a name="ruleFunctionStartsWith"></a>
Tests whether a string value starts with the specified characters.

Returns: Boolean

Parameters:
1. String, the string instance
2. String, the characters

##### Format
```json
{ "$function": { "name": "startsWith", "arguments": [ <string>, <string> ] } }
```
##### Example
```json
{ "$function": { "name": "startsWith", "arguments": [ "@name", "D" ] } }
```

#### To uppercase <a name="ruleFunctionToUpperCase"></a>
Converts a given string to uppercase

Returns: String

Parameters:
1. String, the string to convert

##### Format
```json
{ "$function": { "name": "toUpperCase", "arguments": [ <string> ] } }
```
##### Example
```json
{ "$function": { "name": "toUpperCase", "arguments": [ "@name" ] } }
```

#### Substring <a name="ruleFunctionSubStr"></a>
Extracts a substring from a provided string.

Returns: String

Parameters:
1. String, the string to convert
2. Integer, the start index of the substring
3. Integer, the length of the substring

##### Format
```json
{ "$function": { "name": "subStr", "arguments": [ <string>, <integer>, <integer> ] } }
```
##### Example
```json
{ "$function": { "name": "subStr", "arguments": [ "@name", 5, 5 ] } }
```

#### Square Root <a name="ruleFunctionSqrt"></a>
Calculates the square root of a provided number.

Returns: Number

Parameters:
1. Number, the number for the calculation

##### Format
```json
{ "$function": { "name": "sqrt", "arguments": [ <number> ] } }
```
##### Example
```json
{ "$function": { "name": "sqrt", "arguments": [ 3 ] } }
```

#### Min <a name="ruleFunctionMin"></a>
Returns the minimum value from an array of numbers.

Returns: Number

Parameters:
1. Number Array, the array to query.

##### Format
```json
{ "$function": { "name": "min", "arguments": [ <number array> ] } }
```
##### Example
```json
{ "$function": { "name": "min", "arguments": [ @grades ] } }
```

#### Max <a name="ruleFunctionMax"></a>
Returns the maximum value from an array of numbers.

Returns: Number

Parameters:
1. Number Array, the array to query.

##### Format
```json
{ "$function": { "name": "max", "arguments": [ <number array> ] } }
```
##### Example
```json
{ "$function": { "name": "max", "arguments": [ @grades ] } }
```

#### Average <a name="ruleFunctionAvg"></a>
Returns the average value from an array of numbers.

Returns: Number

Parameters:
1. Number Array, the array to query.

##### Format
```json
{ "$function": { "name": "avg", "arguments": [ <number array> ] } }
```
##### Example
```json
{ "$function": { "name": "avg", "arguments": [ @grades ] } }
```

#### Years from now <a name="ruleFunctionYearsFromNow"></a>
Calculates the number of years between a provided date and the current date.

Returns: Number

Parameters:
1. Date, the date to query.

##### Format
```json
{ "$function": { "name": "getYearsFromNow", "arguments": [ <date> ] } }
```
##### Example
```json
{ "$function": { "name": "getYearsFromNow", "arguments": [ @dob ] } }
```

## RuleSet <a name="ruleSet"></a>
A RuleSet includes an entity definition and an associated list of rules, to run rules agaisnt your entities you must first define the entity definition and associated rules as a RuleSet, using your own unique RBxId and Version.

### RBxId <a name="ruleSetRbxId"></a>
The RBxId is an unique client identifier used to reference the RuleSet.

### Version <a name="ruleSetVersion"></a>
All RuleSets require a numerical version, specified by the client when it is created. When the client executes the rules they can specify a version number otherwise RuleBox will use the latest version.

### IsDraft <a name="ruleSetDraft"></a>
If the client creates a draft RuleSet it can only be used if the version number is specified during execution, it won 't be considered the latest version until IsDraft is set to false.

#### Example
```json
{
  "ruleset":
  {
      "entity": { "name": "Text" },
      "rules": [
          {
              "predicate":{ "$function": { "name": "startsWith", "arguments": [ "@name", "Dave" ] } } ,
              "outcome": true,
              "stop": true
          }
      ]
  }
}
```

## APIs <a name="apis"></a>
### Introduction <a name="apisIntroduction"></a>
The RBx API consists of a number of endpoints that allow client to create RuleSets and test entities agaisnt them.

For more information on the APIs you can view our [Swagger Specification](#https://app-execution-api-prod-uks-001.azurewebsites.net/swagger/index.html).

###  Compilation <a name="apisCompilation"></a>
```json
POST /compilation/{rbxId}/version/{version:int}
```

The Compilation API is used define your entity and rules ready for execution.

#### Example Request Body
```json
{
  "ruleset":
    {
      "entity": { "name": "Text", "age": "Number", "country": "Text"  },
      "rules": 
      [                          
          { 
              "predicate":{ "@age": { "$gte" : 21}, "@country" : "USA" },
              "outcome": true,
              "stop": true
          },
          { 
              "predicate":{ "@age": { "$gte" : 18}, "@country" : "UK" },
              "outcome": true,
              "stop": true
          }
      ]
    }
}
```

### Execution <a name="apisExecution"></a>

Once you've created your RuleSet with the Compilation API you can use the execution APIs to test entities agaist your rules.

#### Match <a name="apisExecutionMatch"></a>
```
POST /execution/{rbxId}/match
POST /execution/{rbxId}/version/{version}/match
```
The **Match API** accepts a single entity and returns a boolean value that indicates whether it matches a rule.

##### Example Request Body
```json
{
"testobj":  { "name": "Dave","age": 43  }
}
```
##### Example Response Body
```json
{
    "isMatch": true
}
```

#### All <a name="apisExecutionAll"></a>
```
POST /execution/{rbxId}/all
POST /execution/{rbxId}/version/{version}/all
```
The **All API** accepts an array of entites and returns a filtered array where rule matches are found.

##### Example Request Body
```json
{
"testobjs": [
    { "name": "John","age": 15, "country":"UK"  },
    { "name": "Frank","age": 19, "country":"UK"  },
    { "name": "Mike","age": 21, "country":"USA"  },
    { "name": "Andrew","age": 20, "country":"USA"  }]
}
```
##### Example Response Body
```json
[
    {
        "name": "Dave",
        "age": 21,
        "country": "USA",
    },
    {
        "name": "John",
        "age": 19,
        "country": "UK",
    },
]
```

#### First <a name="apisExecutionFirst"></a>
```
POST /execution/{rbxId}/first
POST /execution/{rbxId}/version/{version}/first
```
The **First API** accepts an array of entites and returns the first entity from the array that matches a rule.

##### Example Request Body
```json
{
"testobjs": [
    { "name": "John","age": 15, "country":"UK"  },
    { "name": "Frank","age": 19, "country":"UK"  },
    { "name": "Mike","age": 21, "country":"USA"  },
    { "name": "Andrew","age": 20, "country":"USA"  }]
}
```
##### Example Response Body
```json
{
    "name": "Dave",
    "age": 21,
    "country": "USA",
}
```
## Getting Started <a name="gettingStarted"></a>
### Define an Entity <a name="gettingStartedEntity"></a>
Define a person entity with 3 properties

- name (text)
- age (number)
- country (text)

```json
{ "name": "Text", "age": "Number", "country": "Text"  }
```

### Build some Rules <a name="gettingStartedRules"></a>
We're going to build two rules to check for peoples ages in different countries.

The first rule will test for people aged 18 and over in the UK
```json
{ "@age": { "$gte" : 18}, "@country" : "UK" }
```

The second will test for people aged 21 and over in the USA
```json
{ "@age": { "$gte" : 21}, "@country" : "USA" }
```

### Create a Ruleset <a name="gettingStartedRuleset"></a>
Compine the entity definition and rules into an RBx Ruleset.
```json
{
  "ruleset":
    {
      "entity": { "name": "Text", "age": "Number", "country": "Text"  },
      "rules": 
      [                          
          { 
              "predicate":{ "@age": { "$gte" : 21}, "@country" : "USA" },
              "outcome": true,
              "stop": true
          },
          { 
              "predicate":{ "@age": { "$gte" : 18}, "@country" : "UK" },
              "outcome": true,
              "stop": true
          }
      ]
    }
}
```

Then call the the RBx Compilation API with your Ruleset, you'll need to specify an RBxId and Version Number.
```
/compilation/{rbxId}/version/{version:int}
```
For more information on the APIs you can view our [Swagger Specification](#https://app-execution-api-prod-uks-001.azurewebsites.net/swagger/index.html).

### Test the Entity objects <a name="gettingStartedTest"></a>
Once you've created your RuleSet you can start testing entities. First we'll create an entity that matches your entity definition.
```json
{ "name": "Frank", "age": 21, "country":"USA"  }
```
Then create a request body for the execution match API.
```json
{
"testobj": 
    { "name": "Frank", "age": 21, "country":"USA"  }
}
```
Use the RBxId and Version from the execution API call to call the match API.
```
/execution/{rbxId}/version/{version}/match
```
For more information on the APIs you can view our [Swagger Specification](#https://app-execution-api-prod-uks-001.azurewebsites.net/swagger/index.html).

You should see the response below returned from the API.
```json
{
    "isMatch": true
}
```
If you give the age property of the entity a value of 10 and call the match API again you should see a different response.
```json
{
    "isMatch": false
}
```
Next lets create some more entities and add them to a request object for the execution all API.
```json
{
"testobjs": [
    { "name": "Dave", "age": 21, "country":"USA"  },
    { "name": "Frank", "age": 19, "country":"USA"  },
    { "name": "John", "age": 19, "country":"UK"  },
    { "name": "Eric", "age": 17, "country":"UK"  }
]
}
```
Use the RBxId and Version from the execution API call to call the execution all API.
```
/execution/{rbxId}/version/{version}/all
```
For more information on the APIs you can view our [Swagger Specification](#https://app-execution-api-prod-uks-001.azurewebsites.net/swagger/index.html).

You should see the response below returned from the API.
```json
[
    {
        "name": "Dave",
        "age": 21,
        "country": "USA",
    },
    {
        "name": "John",
        "age": 19,
        "country": "UK",
    },
]
```
