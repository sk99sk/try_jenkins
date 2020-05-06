# Automation with Jenkins

Jenkins provides automation for developers to make things very fast and easily scalable. It is the main component in CI/CD pipeline. Jenkins is based on JAVA, so you must have Java and its dependencies to enjoy Jenkins automation.

## System Requirements : 
1. RedHat Linux system
2. Jenkins 
3. Docker latest version

## Our Requirement : 

We want to deploy the code as soon as the developer team commits it to the system. Without any further manual tasks, the entire steps gets automated with the Jenkins integration.

### 1. Code Commit
Upon commiting the code, git **hooks** execute the scripts written in **post-commit** hook which pushes the code to github.

```
#!/bin/bash/
echo "This will automatically push the cod eto github after each commit
git push 
```

### 2. GitHub Hooks
From GitHub, GitHub hooks detects the code push and triggers the github hook to the jenkins system via post-request informing the local Jenkins of the latest code push to GitHub.
> The endpoint will be from ngrok

### 3. Jenkins Jobs
Upon receiving the information from github hooks, the jobs are triggered.
1. Job1 : this pulls the latest code and saves in the local workspace. After this, it copies the code to the one of the system folder (here /usr/local/apache2/htdocs)
```
git pull https://github.com/sk99sk/try_jenkins.git
```

2. Job2 : This runs a docker container (test server) to test the recent code base. Here testing is performed.

3. Job3 : This upon sucessful testing at test server, updates the document root to the new code base, so that the production system gets ready with lastest code changes.

