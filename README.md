# Serve a Machine Learning Model as a Webservice
Serving a simple machine learning model as a webservice using [flask](http://flask.pocoo.org/) and [docker](https://www.docker.com/).

## Getting Started
1. Use Model_training.ipynb to train a logistic regression model on the [iris dataset](http://archive.ics.uci.edu/ml/datasets/iris) and generate a pickled model file (iris_trained_model.pkl)
2. Use app.py to wrap the inference logic in a flask server to serve the model as a REST webservice:
    * Execute the command `python app.py` to run the flask app.
    * Go to the browser and hit the url `0.0.0.0:80` to get a message `Hello World!` displayed. **NOTE**: A permission error may be received at this point. In this case, change the port number to 5000 in `app.run()` command in `app.py`. 
    (Port 80 is a privileged port, so change it to some port that isn't, eg: 5000)
    * Next, run the below command in terminal to query the flask server to get a reply ```2``` for the model file provided in this repo:
     ```
        curl -X POST \
        0.0.0.0:80/predict \
        -H 'Content-Type: application/json' \
        -d '[5.9,3.0,5.1,1.8]'
     ```
 3. Run ```docker build -t app-iris .``` to  build the docker image using ```Dockerfile```. (Pay attention to the period in the docker build command)
 4. Run ```docker run -p 80:80 app-iris``` to run the docker container that got generated using the `app-iris` docker image. (This assumes that the port in app.py is set to 80)
 5. Use the below command in terminal to query the flask server to get a reply ```2``` for the model file provided in this repo:
    ```
        curl -X POST \
        0.0.0.0:80/predict \
        -H 'Content-Type: application/json' \
        -d '[5.9,3.0,5.1,1.8]'
    ```
    
For details on floating the containerized app on [AWS ec2 instance](https://aws.amazon.com/ec2/), see the [blog](https://medium.com/@tanuj.jain.10/simple-way-to-deploy-machine-learning-models-to-cloud-fd58b771fdcf).

## LICENSE
See [LICENSE](LICENSE) for details.