# Deploy spring boot in docker and orchestrate by kubernetes

## Create cluster
Open the termincal. You can open it from winscp if you have installed. Type below command:-
```
minikube start --vm-driver=none
```
**Note:** Here ```--vm-driver=none ``` is specified. It means it doen;t need any hypervisor. If you have installed the virtualbox than, you need to specify ``` --vm-driver=virtualbox ```.

## Open dashboard
```
minikube dashboard
```
It will open the dashboard in the browser.

## Create image
Dockerfile
```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
ADD ${JAR_FILE} app.jar
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/app.jar"]
```
- Run below command from the location where *Dockerfile* is listed to create image in local host
```
docker build . -t sample-name:tag
```
- Login to docker hub
```
docker login --username=<ajaytiwari52> --password=password
```
- Push image
```
docker tag 7b76fe31970b ajaytiwari52/test:<tage-name-to-be-shown-in-repository>
```
***7b76fe31970b*** is the image id. You can get image id by running ``` docker images ``` command.
***ajaytiwari52*** is your private account in docker repository.
***test*** is your repository
Run the below command to push the above image
```
docker push ajaytiwari52/test
```
- Create deployment
```
kubectl run sample-spring --image= ajaytiwari52/test:first --port=8080
```
Always sprcify ``` --port=8080 ``` as per minukube document.

- Expose service
You need to expose the deployment as service otherwise you will not be able to access it. Run bellow command
```
kubectl expose deployment sample-spring --type=NodePort --port=8084 --target-port=8080
```
Here *type* is *NodePort*. If you have deployed from dashboard you need to change this in service yaml file after deployment. *target-port* should be 8080. *port* can be from range 30k to 32k.

- Access the service
Run below command to get the service url
```
minikube service angular-app --url
```
Copy the url in browser.
