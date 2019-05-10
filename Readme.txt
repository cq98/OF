Unclear Steps from the OF tutorial
- For pushing function's image to Docker Hub,before faas-cli push -f ./hello-python.yml
	TO DO:
		- Open hello-python.yml file, and under IMAGE, edit to username/hello-python 
		- Also, tag hello-python by 
		docker tag hello-python username/hello-python [If this is not done, faas-cli push will state that image does not exist locally]
- hello-python failed to deploy with status code 401

