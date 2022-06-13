We should change DateTime.Now to DateTime.UtcNow, because DateTime.Now can change depending where the microservice is deployed and it can cause some problems.

One thing to think about is when we validate the user input, if we user Datetime.UtcNow, we can get in trouble sometimes, because we do not know where the user is, and then, reject to store some new information like PiggyBank, because PiggyBank could be in the past. One example is for Brazilians,  because they that live in UTC -3