# final project documentation

This is the final project documentation by team 5.

Students are:
* Khiel Mantilla
* Martin Marwad
* Jose Ramos
* ok

Our topic problem is to implement a multiplayer game session. We decide to use unreal engine because it complements Amazon Web Service nicely.

Which tools are we using in amazon web services?
* Gamelift
* Lambda
* Cognito
* API Gateway

Our architecture is this.

We shall upload our game build to Gamelift. We will then create a fleet that will run the build in a server.

We will then create two lambda function, one to start a game session and one to authorize users using cognito.
* Our start-game-session function will find a game session to create a new player session or otherwise create a new game session on the fleet. Our team must grab the fleet ID from the fleet that is running our build in Gamelift so that we may be able to look in the fleet and either grab the existing game session or create a new game session.
* Our authorizer-user function will utilize AWS cognito to check if the credentials (username and password) are correct. Our team must grab the cognito ID which we will have once we create the cognito user pool and client in AWS. Once we have the id, we can check in the cognito with our lambda function.



