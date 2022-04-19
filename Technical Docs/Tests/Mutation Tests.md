# [[Mutation Tests]]
 
I decided to use [**Stryker Mutator**](https://stryker-mutator.io/) as the mutators framework. I think that this project is a little limited, but it's ok so far.
 The biggest limitation is that each project can generate the mutators for only one project at the same time. One example is that I have the project `Expenses.Tests.csproj` that has tests for three projects (Expenses.Domain.csproj, Expenses.Application.csproj and Expenses.Handler.csproj) and I can generate mutators for only one of these three at the same time... ([Here is the Docs](https://stryker-mutator.io/docs/stryker-net/configuration#project-file-name))

## How to use
  1. Run the command `dotnet tool restore` in the solution folder
  2. Run the command `dotnet stryker -tp <test/project/path/1.csproj> -tp <test/project/path/2.csproj> -p Project.Name.Test.csproj`
	  Example: `dotnet stryker -tp ./Microservices/Expenses/Expenses.Tests/Expenses.Tests.csproj -p Expenses.Domain.csproj`
  
  4. After run the command, on the prompt you'll see the web site generated with the mutators results



 