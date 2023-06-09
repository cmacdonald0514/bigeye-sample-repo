# Airflow Codebase Template

### Running Airflow locally

This project uses a Makefile to consolidate common commands and make it easy for anyone to get started. To run Airflow locally, simply:

        make start-airflow

This command will build your local Airflow image and start Airflow automatically!

Navigate to http://localhost:8080/ and start writing & testing your DAGs! Login with the user-password combo: `admin:admin` (you can change this in `docker-compose.yaml`).

You'll notice in `docker-compose.yaml` that both DAGs and plugins are mounted as volumes. This means once Airflow is started, any changes to your code will be quickly synced to the webserver and scheduler. You shouldn't have to restart the Airflow instance during a period of development! 

When you're done, simply:

        make stop-airflow

### Testing & Linting

Instantiating a local virtual environment is now entirely optional. You can develop entirely through Docker, as Airflow runs inside of docker-compose and `test-docker` and `lint-docker` provide avenues for running those steps without a virtual environment. 

However, not using a virtual environment also means sacrificing any linting/language-server functionality provided by your IDE. To setup your virtual environment:

        make  venv

This project is also fully linted with black and pylint, even using a cool pylint plugin called [pylint-airflow](https://pypi.org/project/pylint-airflow/). To run linting:

With your virtual environment: 

        make lint

With Docker:

        make lint-docker

Any tests can be placed under `tests`, we've already included a few unit tests for validating all of your DAGs and plugins to make sure they're valid to install in Airflow. To run tests:

With your virtual environment:

        make test

Inside Docker:
        
        make test-docker

### Cleaning up your local environment

If at any point you simply want to clean up or reset your local environment, you can run the following commands:

Reset your local docker-compose:

        make reset-airflow

Rebuild the local Airflow image for docker-compose (useful if you make changes to the Dockerfile):
        
        make rebuild-airflow

Clean up Pytest artifacts:
        
        make clean-pytest

Reset your virtual environment:

        make clean-venv

Start completely from scratch:

        make clean-all