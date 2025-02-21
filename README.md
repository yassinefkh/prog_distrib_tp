# masterinfo

```
Put request : curl -X PUT -H "Content-Type: application/json" -d '{"begin" : "12/10/2023", "end" : "12/10/2023"}' "http://localhost:8080/cars/11AA22?rent=true"
```

### Docker

Build the Java file:
```
./gradlew build      
```

Check the Jar file in build/libs

Create a Dockerfile in the code folder: https://github.com/charroux/masterinfo/blob/main/rent/Dockerfile

Build a Docker image:
```
docker build -t rent .      
```
Run the container:
```
docker run -p 4000:8080 rent    
```
Then check in your browser:
```
http://localhost:4000/cars
```

### Publish the Docker image to the Docker Hub

Tager l'image :
```
docker tag 4da2332370c7 votreIdDocherHub/rent:1
```
où le numéro est l'identifiant de l'image donné par docker images, et 1 est un numéro de version

Se connecter au Docker Hub :
```
docker login
```

Publier l'image :
```
docker push votreIdDocherHub/rent:1      
```