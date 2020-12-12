# TacxAPIAssignment

##  Short descreption about the framework :


It was the second option to run API Collection framework. And it was more effective, fast and easy to maintain.


First I created the requests in **POSTMAN** using ```GET```, ```POST```, ```PUT```, ```DEL``` for the **CRUD** methods. I create a collection from these requests and save them as a single line of execution / end to end structure. I downloaded and used [Newman](https://www.npmjs.com/package/newman) to run that collection from my terminal. Then I push my collection to the **Github** account. And I used **Jenkins** with the help of the **Newman** to execute whole collection from the github and generate a fancy report.

### Tools used :

Tools | Purpose
------------ | -------------
POSTMAN | Manual and automated execution of requests and/or collections. 
Github | VCS
Newman | Command-line collection runner, supports to easly integrate with CI tools
Newman reporter htmlextra | Updated version of the standard HTML reporter containing a more in-depth data output

### Design and cration of framework in steps :

#### In POSTAN
I created **environment** to use in every request in POSTMAN as below. 

Environment name : Tacx
VARIABLE | INITIAL VALUE | CURRENT VALUE
------------ | ------------- | -------------
BaseURL | http://dummy.restapiexample.com/api/v1 | http://dummy.restapiexample.com/api/v1

* Than I created API requests by using end-points/methods that is given on [this](http://dummy.restapiexample.com/) website.  
* I created test scripts in POSTMAN using [Chai Library](https://www.chaijs.com/) snippets and JS.
* I created some global variables using ```Pre-request Script``` and I also created some variables in ```Tests``` and I created assertions inside ```Tests```.
* I run them and save one by one in a collection.
* After completed writing API requests, I run the collection easily
* I can share my collection via a link via POSTMAN.[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/333e72b19df0060d28fd)


**After completed the collection I exported my collection in local computer as ```json``` format in a folder. ```TacxAPI.postman_collection.json```**

**I downloaded my environment in Manage Environmet page as ```.json``` format in the same folder.```environment.json```.**

**I downloaded my global variables in Manage Environmet page as ```.json``` format in the same folder.```globals.json```.**


#### Newman
* I installed the newman -> ```npm install -g newman``` from terminal.
* I installed the newman-reporter-htmlextra -> ```npm install -g newman-reporter-htmlextra``` from terminal.
* Go that folder holding .json files and run the command -> ```newman run "TacxAPI.postman_collection.json" e "environment.json" -g "globals.json" -r htmlextra```

And It runs and gives a CLI result from terminal.

#### Jenkins
* I did the same setups above with the jenkins. 
* I open localhost:8080 which Jenkins run in. 
* Entered Manage Jenkins 
  * -> Manage Plugins and install NodeJS Plugin
  * -> Install Cucumber Reports
  * -> Install HTML Publisher Plugin
* I went to Global Tool Configuration and add a new NodeJS, made it's name ```NodeJS```, ```version``` is ```14.0.0``` and made the ```Global npm packages to install``` -> ```npm install -g newman``` to install newman in Jenkins and ```SAVE``` it.
* Create a freestyle job and save.
* Provide the Github link and branch name.
* In ```Build Environment```, ```Provide Node & npm bin/ folder to PATH``` is selected And :
  * ```NodeJS Installation``` is ```NodeJS```selected which I created in Global Tool
  
* In ```Build``` I selected ```Execute Shell``` plugin as a Build Step.
* I wrote a script to install htmlextra reporter and run the collection inside the Jenkins.  
  
```npm install -g newman-reporter-htmlextra```
```newman run "TacxAPI.postman_collection.json" -e "environment.json" -g "globals.json" -r htmlextra```

* I added ```Publish HTML Reporter``` as a ```Post-build Actions``` and configure the name, 
  * HTML directory to archive -> newman
  * Index page[s] -> TacxAPICollection.html
  * Report title -> TacxAPI HTML Report
  * - [x] Always link to last build	is checked 
  * 	Include files -> **/*.html
  
And ```SAVE``` the job.

Go to Dashboard, find the project and ```Build now```

I can see the HTML report by downloading Jenkins workspace as a zip file. Or I can also see these results inside my local folder. 
  

