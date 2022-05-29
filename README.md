# RuleBox

## Examples

### Automotive

#### 001 Basic Search
Defines a vehicle object. The rule tests the fuel type equals a value, the year is between two vales and the bodystyle is in a list of provided values.

##### Examples of
- In
- Between
- Equals

### People

[Test](examples/people/001_swimming_times.md)
#### 001 Swimming and Times
Defines a person object that represents a swimmer including competition entries and times. The rules check for ages, length and times in different strokes using a `startsWith` function.

##### Examples of
- startsWith function
- Less than or equal to
- Equals
- Some

#### 002 Name
Defines a person object, the rules look for a person with a last name of *Smith* where the first name is not *John*.

## Examples of
- Equals
- Not

### Business Process

#### 001 Max Execution Time
Defines a business process and array of historic execution times, the rule checks whether the execution time is greater than the maximum historic execution times.

## Examples of
- Min Function
- Greater than
- Number Array