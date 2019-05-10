STEP 1:
- Install OpenFaas
- ./deploy_stack.sh
	- GOOD to keep track of Credentials
 username: admin 
 password: stringofpasswordgiven
 echo -n stringofpasswordgiven | faas-cli login --username=admin --password-stdin

STEP 2: 
-Install Cli

STEP 3:
- Rember to build before deploy
Unclear Steps from the OF tutorial
- For pushing function's image to Docker Hub,before faas-cli push -f ./hello-python.yml
	TO DO:
		- Open hello-python.yml file, and under IMAGE, edit to username/hello-python 
		- Also, tag hello-python by 
		docker tag hello-python username/hello-python [If this is not done, faas-cli push will state that image does not exist locally]
- faas-cli deploy -f ./hello-python.yml
	-SHOW: run faas-cli login 
		hello-python failed to deploy with status code 401
	- SOLUTION: Go back to the Credentials that we got when we downloaded OpenFaas and then copy and paste from the echo part onwards (e.g.)
	echo -n stringofpasswordgiven | faas-cli login --username=admin --password-stdin
- To test: (e.g.) curl http://127.0.0.1:8080/function/hello-python -d "HI"

STEP 4: 
- Add other modules through requirements.txt
- When changes, we need to build and deploy again
- To test: curl localhost:8080/function/hello-python --data-binary '{
 "url": "https://blog.alexellis.io/rss/",
 "term": "docker"
}'
- Logging and troubleshooting command:
	- Docker Swarm
		- All services: docker service ls
		- Check Specific function : docker service ps function_name
		- Check Specific function logs : docker service logs function_name
	- Metrics:
		- Use Prometheus UI at http://localhost:9090
	- Troubleshoot [can't reach service error]:
		- For multi-node cluster, push images into Docker Hub or similar registry before deploying
		- If it still fails, use docker service logs --no-trunc=true hello-python to get more information
		- in the event that it still fails, recreate Swarm services and rerun deploy


