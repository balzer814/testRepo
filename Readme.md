## Repository Structure
To open a custom project in Eclipse Chea factory Json must be created in a designated folder of the repo
 e.g.: ArtifactType_War/.factory.json
The created factory can used to create a new workspace will be created in a user space(you have to login with OAuth) on codenvy


## creating the .factory.json
* see http://www.eclipse.org/che/docs/factory/json-reference/index.html
* To create/test a factorie it's best to use the codenvy IDE https://codenvy.io/dashboard/#/factories and than copying the resulting factory.json 
* To prevent creating new workspaces every time the user clicks on the link insert:
		
		'"policies": {
			"create" : "perUser"
		}'
	  in the .factory.json
* To provide custom commands use 
		
		'"commands": [
		  {
			"commandLine": "mvn clean package -f ${explorer.current.file.path}",
			"name": "package",
			"attributes": {
			  "goal": "Run",
			  "previewUrl": ""
			},
			"type": "mvn"
		  }
		]'
	* and typing in the command needed (Maven, git, jdk8.. can be included in the runtime using the codenvy IDE/Stacks)
	* The goal defines where the command is located in the IDE (Build, Test, Run, Debug, Deploy, Common are available)
	* To makros ${..} best make a random che workspace in codenvy open the workspace-> Manage Commands->Run->(create new)+
		There you find a link 'macros' 
	  
	* all factories must contain a unique id
	* the workspace name/id/namespace must be the same for all factories in order 
	to use only one workspace and not create a new one every time the user clicks on a different link 

## Issues
* Eclipse che seems to lack the ability to handle Folders containing '%' #2337
* Finding a way to use multiple Factorys scince the codenvy always trys to find a factory in the root folder 
