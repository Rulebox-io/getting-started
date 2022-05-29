# RuleBox - https://rulebox.io/

## Introduction <a name="introduction"></a>
RuleBox is a SaaS Solution that allows you to create and execute business rules agaisnt your own entities objects. Use the RBx APIs to describe your entities and author rules, creating an RBx RuleSet. When you're ready you can pass entity objects to our APIs and we'll run tests agaisnt them using your RuleSet.

This repo contains our **[User Guide](User_Guide.md)** and examples to help you get started creating your own rules.

You can also view our [Open API definition](https://app-execution-api-prod-uks-001.azurewebsites.net/swagger/index.html) or visit our [website](https://rulebox.io/) for more information or to register your interest and to get early access. Feel free to reach out to discuss your requirements and find out how RuleBox can help you.

## Examples

### Automotive

#### 001 Basic Search ([view](examples/automotive/001_basic_search.md))
Defines a vehicle object. The rule tests the fuel type equals a value, the year is between two vales and the bodystyle is in a list of provided values.

##### Examples of
- In
- Between
- Equals

### People
#### 001 Swimming and Times ([view](examples/people/001_swimming_times.md))
Defines a person object that represents a swimmer including competition entries and times. The rules check for ages, length and times in different strokes using a `startsWith` function.

##### Examples of
- startsWith function
- Less than or equal to
- Equals
- Some

#### 002 Name ([view](examples/people/002_name.md))
Defines a person object, the rules look for a person with a last name of *Smith* where the first name is not *John*.

## Examples of
- Equals
- Not

### Business Process

#### 001 Max Execution Time ([view](examples/business_process/001_execution_time_max.md))
Defines a business process and array of historic execution times, the rule checks whether the execution time is greater than the maximum historic execution times.

## Examples of
- Min Function
- Greater than
- Number Array