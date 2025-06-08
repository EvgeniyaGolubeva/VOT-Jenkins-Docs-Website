# VOT-Jenkins-Docs-Website
A simple static website built with HTML & CSS and deployed using **Jenkins**, **Docker**, **Apache**, and **GitHub Webhooks** that is fully automated with CI/CD!

## What’s inside?
- `index.html` – Homepage
- `docs.html` – A little "documentation" section
- `style.css` – Simple responsive styles
- `Jenkinsfile` – Defines the CI/CD pipeline
- `Dockerfile` – Docker image with Apache to serve the website

## How it works
Every time you push to the `main` branch on GitHub:
1. GitHub sends a **webhook** to Jenkins (via ngrok)
2. Jenkins pulls the latest code
3. Jenkins builds a Docker container that:
   - Copies the HTML/CSS files
   - Serves them using Apache
4. Jenkins deploys the site on port `8081` locally

## URLs
| What             | Where                                                        |
|------------------|--------------------------------------------------------------|
| Jenkins UI       | `http://localhost:8080`                                      |
| Site (local)     | `http://localhost:8081`                                      |
| Site (ngrok)     | `https://superb-pika-cunning.ngrok-free.app`                 |
| Jenkins Webhook  | `https://superb-pika-cunning.ngrok-free.app/github-webhook/` |

---

##How to Setup
1. Install a Linux Virtual Machine - Iused Ubuntu, but any Debian-based distro should work.
2. Install Jenkins. I followed the official guide here: https://www.jenkins.io/doc/book/installing/
As Jenkins needs Java and Git to work properly, make sure to also install:
```sudo apt install git openjdk-17-jdk```
3. Install Apache and Docker
```sudo apt install apache2```
```sudo apt install docker.io```
  Apache serves the site through the default /var/www/html folder.
  Docker is used to package and run the site as a container.
4. Give Jenkins Access to Docker
Jenkins runs as its own user, and by default it can’t use Docker. To fix that:
```sudo usermod -aG docker jenkins``` This adds Jenkins to the Docker group and gives it permission to run containers.
```sudo reboot```
5. Test Everything
Follow the steps for after reboot first.
6. Set Up Jenkins Job
Create a new Pipeline project. Point it to the GitHub repo: ```https://github.com/EvgeniyaGolubeva/VOT-Jenkins-Docs-Website```.
It will automatically use the Jenkinsfile inside the repo
7. Set Up Webhook (Automatic Builds). Install ngrok (if you want GitHub to auto-trigger builds)
Get a URL like: https://abc123.ngrok-free.app
Go to your GitHub repo → Settings → Webhooks
Add this URL with /github-webhook/ at the end:
https://abc123.ngrok-free.app/github-webhook/
This makes Jenkins build the site automatically on every push.
8. Push Your Code

---

## After Reboot
1. Start Jenkins
```sudo systemctl start jenkins```
2. Start Docker
```sudo systemctl start docker```
If Jenkins can’t access Docker, run:
```sudo usermod -aG docker jenkins```
```sudo systemctl restart jenkins```
3. Start ngrok
Start the reserved ngrok tunnel:
```ngrok http --domain=superb-pika-cunning.ngrok-free.app 8080```
Leave the terminal open, as it keeps the tunnel active!
4. Trigger the Webhook by pushing to GitHub:
```git add .```
```git commit --allow-empty -m "testing webhook"```
```git push```
5. Open Everything
Jenkins: ```http://localhost:8080```
Site: ```http://localhost:8081```
Public Si`te: https://superb-pika-cunning.ngrok-free.app
