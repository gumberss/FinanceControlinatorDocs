Type: #Feature
From: #Gateway
Status: #Discovery 

## Problem definition
Currently we use nginx as the gateway to the microservices and it is ok when we are testing the system in docker/kubernetes, but when we are testing local, we cant use (easily) it. Since we are starting calling many API from the app, and we want to separate cloud stuff from dev stuff (kubernetes and dev environment), Ocelot seems to be a good gateway.

## Goals / Motivations
[Ocelot](https://github.com/ThreeMammals/Ocelot) is a .net API Gateway, so, .NET means that we can run it with Visual Studio in one click, update packages in 1 click, and after it is in a container, It'll be as same as the other microservices in a container and everything we must do with a gateway, will be way easier because we already know .NET.

Obs: We used Ocelot in the [[Identity]] POC, you can see it [here](https://github.com/gumberss/Sandboxinator/tree/master/C%23/POCs/Authentication/Ocelot)

## Plan
- [Docs](https://ocelot.readthedocs.io/en/latest/)
- [Github](https://github.com/ThreeMammals/Ocelot)

### Steps

## Result