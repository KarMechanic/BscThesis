# Retrieve Technical Debt analysis from GitHub repositories

## The script file ``sconar.sh``: 
- will be used to get multiple public GitHub repositories and run SonarQube analysis on them.
- The SonarQube instance is available locally, and running on port 9000 within a Docker container.
- The script will be run from the command line, and will take in a list of GitHub repositories as arguments, as well
 as the SonarQube token to use for the analysis.
- The script will then run the SonarQube analysis on each repository, and output all the classes that contain instances of Technical Debt and the number of Technical Debt items detected per project

## Prerequisites
- This script requires the following to be installed:
    - Docker
    - Git
    - Curl
    - jq
    - SonarQube Scanner

- The script also requires a SonarQube token to be generated and passed in as an argument. 
    - Before generating the token, make sure that your User has the 'Execute Analysis' permission.
    - 'Execute Analysis' permission can be granted by navigating to the Administration page, and then clicking on the Permissions tab.
    - The token can be generated by logging into SonarQube, and navigating to the My Account page. 
    - From there, click on the Security tab, and then click on the Generate Tokens button. 
    - Select 'User token'
    - Give the token a name, and click on the Generate button. 
    - The token will be displayed on the screen. 
    - Copy the token and save it somewhere safe. 
    - This token will be used as an argument when running the script.


- The script file is written for a linux image for zsh shell. 
    - If you are using a different shell, you will need to change the first line of the script to reflect the shell you are using.


## Usage
### SonarQube on Docker
First, make sure that SonarQube is running on port 9000. 
- You can pull the SonarQube image from Docker Hub and run it as follows:
- `` docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest``
- The SonarQube instance will be available at http://localhost:9000


### SonarScanner
- The SonarScanner needs to be installed and configured.
- The SonarScanner can be downloaded from https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/


### Running the script
The script needs the following arguments to be passed in:
    - ``sonar-token`` - SonarQube token
    - ``sonar-url`` - SonarQube url (e.g. http://localhost:9000)
    - ``github-repos-file`` - a file containing a list of GitHub repositories to be analysed. 
    - ``workdir`` - a directory where the script will create a temporary directory to clone the repositories into, and where the script will output the results of the analysis.

- The script can be run from the command line as follows: ``./sonar.sh --sonar-token={SONAR_TOKEN} --sonar-url={SONAR_URL} --github-repos-file={REPOS.json} --workdir=. 
  ``

### Output
- A folder with .csv files containing TD Java classes per project will be created in the workdir directory.
- A folder with .csv files containing the amount of TD per project will be created in the workdir directory.