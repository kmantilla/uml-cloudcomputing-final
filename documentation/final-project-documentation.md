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

What is our infrastructure? Our game is uploaded to Gamelift and a fleet is created to run a server build. Two lambda functions will be created, one to check for game sessions in the Gamelift fleet and one to check users by AWS Cognito. Our API Gateway instance will set up our API with `GET` and `POST` methods utilizing our lambda functions that way our player can send a request of which our API Gateway will receive and initialize the needed functions.

With a `POST` request sent to the API, if the username and password are correct, our API Gateway will return an *idToken* and a `success` flag. If username or password is entered incorrectly, the API will return a `fail` flag.

With a `GET` request sent to the API, if the idToken is correct and valid and authorized, our API Gateway will return json of the player session ID with `IpAddress` and `Port`. This ip address will be used to connect player and game session in the fleet.

A player can sign up as a user in our Cognito sign up page, and will be able to connect to a game server upon request via game client. Our game client will send a request to our API, set up in by AWS API Gateway, which uses two lambda functions which we will create, one to check for game sessions and one to authorize user login.



## Our architecture is this.

We shall upload our game build to Gamelift. We will then create a fleet that will run the build in a server.

We will then create two lambda function, one to start a game session and one to authorize users using cognito.

Start game session lambda function:
* file name: `Gamelift-StartGameSession.py`
* Our start-game-session function will find a game session to create a new player session or otherwise create a new game session on the fleet. Our team must grab the fleet ID from the fleet that is running our build in Gamelift so that we may be able to look in the fleet and either grab the existing game session or create a new game session.
* Our team must also add an IAM policy.

Cognito login authorizer lambda function:
* file name: `GameLiftUnreal-CognitoLogin.py`
* Our authorizer-user function will utilize AWS cognito to check if the credentials (username and password) are correct. Our team must grab the cognito ID which we will have once we create the cognito user pool and client in AWS. Once we have the id, we can check in the cognito with our lambda function.
* Our team must also add an IAM policy.

Once our lambda functions are written, deployed and tested, our team can start creating a user pool in AWS Cognito and the api in AWS API Gateway.



Creating our Cognito user pool.

This is easily done. We do so in the AWS Cognito console. Our team enables username, email, and password to sign up and sign in to the user pool. When we create our user pool, we then must provide a domain name and callback and sign out URLS. For our URLs we shall just use `https://aws.amazon.com` as our URL. For our domain name, AWS let's us use an Amazon Cognito domain with a domain prefix which we can enter.

Now our user pool is prepared, and it has a hosted UI which we can use to sign up. The hosted UI is a simple login form with a sign up option. We can create a user here. Once the user is created, we can check that the user is created in the user pool settings.



Creating our API in the API Gateway.

This is easily done, and we can do so in the AWS API Gateway console.

We must enter a name, of which AWS will start to create our API instance.

We must enter two resources, a `/login` and a `/startsession` resource.

The `/login` resource will have a `POST` method that can utilize our `GameLiftUnreal-CognitoLogin.py` lambda function.

The `/startsession` resource will have a `GET` method that can utilize our `Gamelift-StartGameSession.py` lambda function.

Once our resources are prepared and set, there is one thing we must do. We must create an authorizer within the API Gateway instance. We must enter a name and a Token Source value of `Authorization`. Next, we must go in to our `/startsession` `GET` Method Request and enter our authorizer in the settings. This shall be the end of preparing our API Gateway instance.


