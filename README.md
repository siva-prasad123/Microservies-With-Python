To-Do Manager: A simple Microservices Example

To-Do Service: The ToDo service provides a RESTful endpoint to list all the lists as well as providing the list of projects filtered on the basis of usernames. 
This service runs on port 5001 of my server.


I Create a file named users.json under the database directory and add the following to the file:

{
    "Siva_Prasad": {
        "id":1,
        "name":"Siva Prasad",
        "verified":1
    },
    "kiran": {
        "id":2,
        "name":"Kiran kumar",
        "verified":1
    },
    "Manoj": {
        "id":4,
        "name":"Manoj Kumar",
        "verified":0
    }
}
The next thing I create another file named todo.json which contains the data of my lists.
 Create the file and add the following data to it:

{
    "Siva_prasad": {
        "home": [
            "Buy milk",
            "Look for pest control service",
            "Get a new carpet"
        ],
        "work": [
            "Complete the blogpost",
            "Create presentation for meeting"
        ]
    },
    "Kiran": {
        "school": [
            "Complete homework",
            "Prepare for test"
        ]
    }
}
So, now we are done with the database part for our application. Next, we have to build our services. So, 
let's start with writing our User service.

Under the services directory, I create a file named users.py and write the code for it:

So, let's start with the code, first we import the dependencies for the service


from flask import Flask, jsonify, make_response
import requests
import os
import simplejson as json



The next we do is to initialize our flask service


app = Flask(name)


Now, we import our users database in the service and parse it as a JSON file


with open("{}/database/users.json".format(database_path), "r") as f:
    usr = json.load(f)


The next step is to write our application endpoints, a simple hello world entrypoint can be created as:


@app.route("/", methods=['GET'])
def hello():
    ''' Greet the user '''

    return "Hey! The service is up, how about doing something useful"





The @app.route helps set the application route. The above example helps us setup a hello world application point. When a user visits our application at http://localhost:5000 the user will be greeted with the message we have specified.


The final step in writing the service will be to run the server as soon as the application is called. 
This can be achieved by the following set of code for our user microservice

if __name__ == '__main__':
    app.run(port=5000, debug=True)
