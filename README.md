# DevOps Lab 9 – Jenkins Multi-Stage Pipeline

## Objective
To create and execute a multi-stage Jenkins pipeline that builds, tests, deploys, and verifies a Python Flask application using Jenkins and GitHub.

## Technologies Used
- Jenkins
- Python 3
- Flask
- Git and GitHub
- Jenkins Pipeline (Jenkinsfile)
- Python unittest

## GitHub Repository
[View Lab 9 Repository](https://github.com/Khushicoder5/devops_lab9)

## Jenkins Dashboard
[Open Jenkins](http://localhost:8080)

**Pipeline Job:** `Python-MultiStage-Pipeline`

## Project Structure

```text
devops_lab9/
├── app.py
├── requirements.txt
├── test_app.py
├── Jenkinsfile
└── README.md
```

## Pipeline Stages

### 1. Build
- Creates a Python virtual environment.
- Installs dependencies from `requirements.txt`.
- Installs Flask and its required packages.

### 2. Test
- Runs automated unit tests using Python's `unittest` module.
- Verifies that the Flask application's home route returns HTTP 200 and the expected response.

### 3. Deploy
- Creates the `python-app-deploy` directory.
- Copies `app.py` and `requirements.txt` into the deployment directory.

### 4. Run Application
- Starts the deployed Flask application using `nohup`.
- Writes the application process ID to `app.pid`.
- Redirects application logs to `app.log`.

### 5. Test Application
- Runs the automated unit test again to verify the application.

## Execution Steps

1. Push the application files and `Jenkinsfile` to GitHub.
2. Create a Pipeline job in Jenkins.
3. Configure Jenkins to fetch the repository from GitHub.
4. Set the script path to `Jenkinsfile`.
5. Click **Build Now**.
6. Verify each stage in the Console Output.

## Successful Build Output

The Jenkins pipeline completed successfully.

```text
Build:
Successfully installed Flask-2.1.2
Jinja2-3.1.6
MarkupSafe-3.0.4
Werkzeug-2.1.2
click-8.5.0
itsdangerous-2.2.0

Test:
Ran 1 test in 0.016s
OK

Deploy:
Application files copied to python-app-deploy

Run Application:
Application started using nohup

Test Application:
Ran 1 test in 0.010s
OK

Pipeline completed successfully!
Finished: SUCCESS
```

## Final Result

The Jenkins multi-stage pipeline executed successfully. All five stages—Build, Test, Deploy, Run Application, and Test Application—completed, and both unit test executions passed.

**Build Status:** SUCCESS

