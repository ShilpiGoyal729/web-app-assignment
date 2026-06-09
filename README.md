Task 10: Troubleshooting Scenarios

Application is not accessible
Root cause analysis
• Container might have some issue
• Wrong host port : container port mapping (while running container -p misconfigured)
• Application crashing in loop after start
• Application may be fine internally but not accessible outside due to network/firewall blocking the connection

Troubleshooting Steps:-
i. Check container status:
docker ps
docker ps -a
⁍ We can know if the container is up, exited or restarting (crash loop) and name of the container

ii. Check logs of container:
docker logs <container-name>
⁍ Exact reason of crash, what happened inside application, errors, crash reasons, missing DB issues, port binding issues

iii. Inspect container details
docker inspect <container-ID>
⁍ Detailed info about the container

iv. Check application access
curl http://localhost:8080
⁍ Check if application is accessible from outside or not

Fix
Restart the container, fix port mapping issues, check firewall/network settings and restart container

Docker container is continuously restarting
Root cause analysis
• Application failed while starting because required config or dependency is missing
• Missing environment variables
• Incorrect CMD / ENTRYPOINT

Troubleshooting Steps:-
i. Check container list and status
docker ps -a
⁍ Shows all containers (running + stopped + exited)

ii. Check logs of container
docker logs <container-name>
⁍ Helps find errors, crash reasons, missing DB issues, port binding issues, startup failures

iii. Inspect container details
docker inspect <container-id>
⁍ Detailed configuration of container

Fix
Add missing environment variables and ensure all dependencies and services are running properly

Nginx returns "502 Bad Gateway"
Root cause analysis
• Backend application is not running, so Nginx cannot forward request
• Wrong upstream/service name in Nginx config
• Incorrect port mapping between services
• Network issue between containers

Troubleshooting Steps:-
i. Check container status
docker ps -a
⁍ Shows running and stopped containers

ii. Check Nginx logs
docker logs nginx-proxy
⁍ Shows Nginx error details

iii. Check backend logs
docker logs webapp-container
⁍ Shows backend application errors and crash reasons

iv. Check network connection
docker network inspect docker-webapp_default
docker exec -it nginx-proxy sh
curl http://webapp-container:80
⁍ Confirms communication between Nginx and backend

Fix
Fix proxy_pass in Nginx config, restart backend container, and ensure both containers are in the same Docker network

SSL certificate is not working
Root cause analysis
• Wrong SSL certificate or key file path in Nginx configuration
• Certificate file missing or not mounted correctly
• Expired or invalid certificate
• Browser does not trust self-signed certificate
• Nginx not reloaded after SSL changes

Troubleshooting Steps:-
i. Check SSL files
ls ssl/
⁍ Verify certificate and key files exist

ii. Check Nginx logs
docker logs nginx-proxy
⁍ Identifies SSL loading or startup errors

iii. Test HTTPS connection
curl -k https://localhost
⁍ Checks HTTPS response and SSL working status

iv. Check Nginx configuration
docker exec -it nginx-proxy cat /etc/nginx/conf.d/default.conf
⁍ Verify correct ssl_certificate and ssl_certificate_key paths and port 443 setup

Fix
Fix SSL file paths in Nginx configuration, regenerate SSL certificate if needed, and restart Nginx container

Database connection fails
Root cause analysis
• MySQL container not running
• Wrong username or password
• Wrong hostname (should use service/container name)
• Network issue between containers

Troubleshooting Steps:-
i. Check containers
docker ps
⁍ Verify MySQL container is running

ii. Check MySQL logs
docker logs mysql-container
⁍ Shows DB errors, authentication failures, or startup issues

iii. Check network
docker network inspect docker-webapp_default
⁍ Ensures DB and app are in same network

iv. Test DB login
docker exec -it mysql-container mysql -u root -p
⁍ Manually verifies credentials and DB access

Fix
Fix username, password, and hostname (mysql-container), ensure correct network connection, and restart MySQL container

Port conflict occurs during deployment
Root cause analysis
• Port already used by another process
• Old container still running
• Same port used by multiple services

Troubleshooting Steps:-
i. Check port usage
lsof -i :8080
⁍ Checks which process is using the port

ii. Check container status
docker ps
⁍ Shows port mapping and running containers

Fix
Remove conflicting container using docker rm -f <container> or change port mapping to another free port and restart container

Server disk usage reaches 100%
Root cause analysis
• Unused Docker images
• Large container logs
• Unused volumes
• No cleanup policy

Troubleshooting Steps:-
i. Check disk space
df -h
⁍ Shows system disk usage and available space

ii. Check Docker usage
docker system df
⁍ Shows Docker images, containers, and volume usage

iii. Check containers
docker ps -a
⁍ Identifies stopped or unused containers consuming space

Fix
Free up space by removing unused containers, images, and volumes using Docker prune commands
docker system prune -a
docker volume prune
docker image prune -a
