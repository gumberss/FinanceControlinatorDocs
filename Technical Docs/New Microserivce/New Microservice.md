# [[New Microservice]]
## What to do?
- Create API
	- Create dockerfile
- Create DB DockerFile
- Add them to dev docker-compose
- Add JWT Verification
- Register the api URL as audience in the gateway JWT audience
- Register API routes on Gateway (ocelot?) 
	- Downstream/Upstream
- Add Tests to Github actions
- Add the tests result to codacy code coverage
	- Need to add coverlet references
- Add API docker image push to Github actions
- Add Kubernetes files to db and api (helm)
- Add API/DB deploy #WhenCloud 
