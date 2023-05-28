Type: #TechnicalDebit
From: #DbContext
Status: #OnlyIdea 
## Overview 
Since I don't want to persist on database in AppServices (flow) and Service (logic), the handler has this responsibility and it is correctly on my point of view.

The main problem so far is that almost every handler has the same responsibility:
1. Call AppService
2. Check if result is an exception
3. if it is not, try to save
4. Check if the result of save is an exception
5. If it is, build a business exception (because the controller know how to deal with this)
6. return the exception
7. Otherwise, return the data result

## Exemple of the problem
![image](https://user-images.githubusercontent.com/38296002/163622229-4cbc079a-d31b-47fb-9c80-6dbd345dd2c6.png)


The main idea of this document is, that the handler responsibility should be only call the correct App Service (flow) and be a bridge between the business rules and the doors (controllers and integration handlers).

## Possible solutions
So, the correct responsibility should be 1. 2. 3.
and the other responsibilities be from others like:
1. An interceptor that get the data result or save error result and build the internal server error exception (will I be able to know the result type?)
2. The Commit from IDbContext return the exception already built
3. A static method in BusinessExpetion that build the internal server error from a message and a custom logger that log based on the result (exception or data)



## Solved as:
- [this pull request](https://github.com/gumberss/FinanceControlinator/pull/128)
