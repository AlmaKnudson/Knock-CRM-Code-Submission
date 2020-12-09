# Getting started
A simple [Knock Full Stack Screening - Core](https://gist.github.com/marvincolgin/b348800b942d4d56e51e173b099b1e49#file-knock-screening-fullstack-md) implementation.

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install all dependencies.

```bash
pip install -r requirements.txt
```

## Tests
Navigate to the project directory "flaskProject" and run pytest
```bash
pytest 
```

## Database
Currently, configured to point to an instance of MongoDb running on MS Azure. The temporary username and password will expire in a week, but should be sufficient to play around with a bit.

## Postman
The provided postman collection to make calls to the messaging API. Feel free to let loose and have some fun sending messages! 

## Limitations & Potential enhancements
Threads are restricted to contain between [2-100] users and messages in the thread are restricted to be as long as a Tweet (280 characters).
FYI, a thread can currently contain duplicate usernames in a given thread. This is a clear area for improvement.

# Architectural Considerations & Design Decisions
## Database
### Why MongoDB instead of DynamoDB, Sqlite, MySQL, Redis etc? 
##### Here it is really a matter of taste. I wanted persistence that would be quick to integrate with and was decoupled from the API application. Since I already had a MongoDB cluster setup; that fit the bill.

## Framework 
### Why Flask instead of FastAPI, Django etc?
##### I chose Flask because I have used it before for simple API applications. With that said, I think that FastAPI is the preferred choice here. It is more performant than Flask. It also provides DI, data validation and documentation generation (SwaggerUI and ReDoc) out of the box. All of which Flask is lacking. If I were to continue this messaging project, I would quickly replace Flask with FastAPI. However, I was able to make use of some of Flask's features. Like serialization and modularity using Blueprints. I guess it is also worth noting that Django could handle all of my needs here, but I was preferential to a micro-framework instead.

## Configuration
### What is going on with configuration?
##### I chose to hard code configuration and secrets in the .env file. The correct approach would be to leverage Secrets Manager (AWS) or Key Vault (Azure) paired with a more robust configuration module.

## Error Handling Concept
### What is the current state of error handling?
##### Honestly, I did not really get around to defining a robust error handling strategy even though this is a must-have in a production level application.

## Logging
### What is logged and when? 
##### I have logs that rotate after 10mb. While the logging is not really useful with such a tiny application, it provides a great foundation for a production level application. It would also be important to consider anonymization of logs since they contain usernames.

## Pipeline (CI/CD)
### This would be nice to setup with more time...
##### To be added (due by 01.01.2050)
