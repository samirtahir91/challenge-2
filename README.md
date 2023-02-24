# Challenge

Hello fellow applicant, we have a very exciting challenge for you to solve, it will be broken down into stages to make it easier to understand and to score you as well.
There is an application called "addtime" that contains two API endpoints: / and /time. The endpoint / will just return "Welcome to the HomePage!" and a GET request to the endpoint /time will add the current time to a mysql database. The application runs by default on port 8082 and it was compiled in go for linux x86. Here are the suggested stages that you need to complete in order to reach the end goal, which is to deploy the application on kubernetes.

1) Create a docker image with the application binary that will run when you start the container and expose it on port 8082.

2) You also need a database. For that, you can use the mysql official image "mysql:5.6". You also need to create the database and table. For that, I have included for you an initdb.sql, so you can run that to create your database schema. The default root password to access the database inside the application is "password". To get help from the application and see the defaults, just run from a shell: addtime -h

3) Once you have both containers up and running on your docker environment you can test the application and check if it's working as expected, this is a sample response of what you should expect when making a GET request to the API endpoint / :

```
curl -v http://192.168.50.10:8082/

- Trying 192.168.50.10...
- TCP_NODELAY set
- Connected to 192.168.50.10 (192.168.50.10) port 8082 (#0)
> GET / HTTP/1.1
> Host: 192.168.50.10:8082
> User-Agent: curl/7.54.0
> Accept: /
> < HTTP/1.1 200 OK
> < Date: Fri, 18 May 2018 13:04:26 GMT
> < Content-Length: 24
> < Content-Type: text/plain; charset=utf-8
> <
  - Connection #0 to host 192.168.50.10 left intact
  - Welcome to the HomePage!
```

4) This is what expect When doing a GET request to the API endpoint /time :

```
curl -v http://192.168.50.10:8082/time

- Trying 192.168.50.10...
- TCP_NODELAY set
- Connected to 192.168.50.10 (192.168.50.10) port 8082 (#0)
> GET /time HTTP/1.1
> Host: 192.168.50.10:8082
> User-Agent: curl/7.54.0
> Accept: /
> < HTTP/1.1 200 OK
> < Date: Fri, 18 May 2018 13:05:00 GMT
> < Content-Length: 21
> < Content-Type: text/plain; charset=utf-8
> <
  - Connection #0 to host 192.168.50.10 left intact
  - Welcome to the TIME endpoint!
```

5) Check the results on your mysql if when you hit /time it’s adding an entry for the current time. This is what you should expect to find on the database:

```
MYSQL> use challenge;
Database changed
MySQL [challenge]> select * from addtime;
+----+----------------------------------------------------------+
| id | time                                                     |
+----+----------------------------------------------------------+
| 13 | 2018-05-22 13:37:04.187953449 +0000 UTC m=+320.084343109 |
| 14 | 2018-05-22 13:42:45.534329594 +0000 UTC m=+661.430719238 |
| 15 | 2018-05-22 13:42:46.411702338 +0000 UTC m=+662.308091984 |
| 16 | 2018-05-22 13:42:47.029824738 +0000 UTC m=+662.926214381 |
| 17 | 2018-05-22 13:42:47.549798625 +0000 UTC m=+663.446188269 |
+----+----------------------------------------------------------+
```

6) Great, now that you have seen the application running, it's time to deploy on kubernetes. Please use minikube since it's quick and easy to setup. Also we can make sure that you are running on the same environment as us, so it’s consistent. Please create the necessary yaml files to deploy the application and the database.

  **Please deploy the application as if it's going to be on a production environment****:** that means it needs to be secure, reliable and fault tolerant in case one of the pod dies (Keep in mind that you have only one node with minikube).

7) Please change the default port for the application to run on port 9090 and the mysql password should be set to “challenge”
If you think that any changes need to be made in the source code for the application, feel free to do so and make note of why.
Once completed, please commit all yaml files, the Dockerfile and the source code for the application (if you changed anything). Also, please provide documentation on how to deploy the application.
