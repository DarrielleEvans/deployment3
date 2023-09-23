# Incident Report
### Date: 09/20/2023
### Time of Outage: 8:08 pm
### Time of Resolution: 8:12 pm

## Error/s
Internal Server Error
The server encountered an internal error and was unable to complete your request. Either the server is overloaded or there is an error in the application.

## Description of Incident
A new hire was tasked with updating the URL shortener. The new hire committed version 2 of the application to the main branch. Which automatically triggered a build, test, and deploy to the production server, replacing version 1 of the application running on the server.

## Steps to Resolution

### Step 1
* Accessed the URL Shortner Application code repository and rolledback to version 1 on a new branch called rollback-version1
    - command/s used: git branch version2Error
* Created a branch containing version 2 for future inspection after application is up and running
    - command/s used: git reset --hard 4707109
* Rolled the code back to the last commit containing version 1 of the application 
  - command/s git push --force
* Ran the force option to push the code and ignore commits that came after. The version2Error branch contains these commits.

### Step 2
* Accessed the Elastic Beanstalk environment and downloaded the last 100 logs

* The logs are reporting that Line 20 is not converting the JSON object into a str, byte, or bytearray.
* After examing line 20 in the code base, the error is that the intern is using loads instead of load to convert the Json. The correct line of code is urls = json.load(urls_file)

### Is the issue fully resolved? Yes

## Prevention Methods
* Restrict the ability for team members to push code to production without a code review from designated managers. 
* Create proper documentation that all developers will adhere to that includes instructions on creating individual branches when making changes to the main code.

