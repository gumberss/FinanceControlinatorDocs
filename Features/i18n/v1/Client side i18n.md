## What we have so far
At this time, the back end return only the pt BR language, but it is prepared to return any other language because the class ptBr inherit the ILocalization interface.
Every time we need to return some data based no the language, we need to 'render' the language on the server side and return it to the client side.

## What we are thinking about
A way to share the language from server side to client side

## How?
1. Endpoint that return a file 'ptbr.json' that able client side to use the same filed usedin the server side
	1. How much endpoints? one for each microservice?
2. A microservice that handle each kind of localization features (hold the file and do format things)?
	1. Is it scalable?
3.  Keep it as it is
	1. Render on the server
	2. How to deal with error messages?
		1. Ex: "Error to comunicate to the server"
		2. Ex: "This value is not aceptable"
4.  Create a file in the client side to hold the client side texts
	1. It could be used with Keep it as it is

