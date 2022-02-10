[![SamuelNavarro](https://circleci.com/gh/SamuelNavarro/project-ml-microservice-kubernetes.svg?style=svg)](https://github.com/SamuelNavarro/project-ml-microservice-kubernetes)

## Summary of project
We have a pre-trained `sklearn` model and we provided the project ability to serve out the predictions via API calls. The project is containerized and we need to be able to run it either standalone, in docker or in a kubernetes cluster. Also, we've provided CI to the project via CircleCI.


## Steps
To run the app you first need to run the server with whatever of the following choices inside your virtual environment:
1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

To make predictions, with the application running, open another terminal and run the `./make_prediction.sh` script.


## Structure of the project

We have provided the server configuration in the `app.py` file. The app accepts a `POST` request (which is given in `./make_prediction.sh`), converts this payload to a DataFrame and then in predicts the value given this input. 

The `Dockerfile` run in the official python 3.7 image and copies the app.py file into the app working directory. It then install the dependencies and exposes the correct ports. Also, we run the app at container lunch.


The `Makefile` let us create the environment and test our commands. We have provided linting and some test to check if circle ci will pass.


- `run_docker.sh` builds the image and runs the app in the specified port: `80`
- `run_kubernetes.sh`: In order to run the app in a kubernetes cluster you have to have installed `minikube`. We run the app in the port `80` and we forward the container port (`8000`) to the host port (`80`) with `kubectl`.
- `upload_docker.sh`: Uploads our image to Docker Hub.



