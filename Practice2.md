# Pratice 2 - Using Docker Compose

##### Step 1: Install Docker Conpose

After Install Success, show version docker-compose
```console
$ docker-compose -v
```






##### Step 2: Download docker-compose.yml

```console
$ curl -sSL https://raw.githubusercontent.com/bitnami/bitnami-docker-wordpress/master/docker-compose.yml > docker-compose.yml
```
View docker-compose.yml
```console
$ cat docker-compose.yml
```
#### Step 3: Run 2 Images with docker-compose
Run
```console 
$ docker-compose up -d
```


# Result
Go to *http://localhost:8080* or *https://localhost:8443* to test
![image](https://user-images.githubusercontent.com/43313369/117467889-50b96700-af7e-11eb-98ae-98468c31f484.png)
