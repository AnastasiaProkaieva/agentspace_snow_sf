# Support Agent

## Setup

1. Run all the following commands from the support_agent folder:
```
cd support_agent
```

2. Ensure that you're in an environment that has all the required libraries in requirements.txt. You can, for example create your virtual enviroment with the required libraries:

```
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements.txt
```

3. Authenticate with the cloud CLI by runing run:
```
gcloud auth login
```
Follow the instructions in your browser

Login in the pop up window using your credentials

## (Optional) Test locally using ADK web
1. Update .env file with your own information
IMPORTANT: Ensure that the IS_ADK_WEB environment variable is set to TRUE

2. run:
```
adk web
```

3. go to http://localhost:8000/dev_ui/ to interact with the agent

## Deploying the Support Agent to Agentspace

1. Update .env file with your own information
IMPORTANT: Ensure that the IS_ADK_WEB environment variable is set to FALSE

2. run (only once): 
```
chmod +x toolkit/add_sf_authorization_to_agentspace.sh
chmod +x toolkit/add_snow_authorization_to_agentspace.sh
chmod +x toolkit/register_agent_to_agentspace.sh
```

3. Add a Salesforce Oauth2 authorization to Agentspace:
```
./toolkit/add_sf_authorization_to_agentspace.sh
```

4. Add a Servicenow Oauth2 authorization to Agentspace:
```
./toolkit/add_snow_authorization_to_agentspace.sh
```

5. Deploy your agent to Agent engine: Run:
```
python3 deploy.py
```

6. After running the deploy.py you'll see something like this in the execution logs:
```
INFO:vertexai.agent_engines:agent_engine = vertexai.agent_engines.get('projects/<your-project-number>/locations/<your-engine-location>/reasoningEngines/<your-reasoning-engine-id>')
```
Copy the reasoning engine id from the deploy.py response logs and use it to replace the .env REASONING_ENGINE_ID variable.


7. Finally register the agent to agentspace bu running:
```
./toolkit/register_agent_to_agentspace.sh
```


## Additional tools
### [DANGER] Delete all the agents registered in an agentspace app
1. Update .env file with your own information, particularly the ENGINE_ID with the ID of the Agentspace App you would like to delete agents from

2. run (only once): 
```
chmod +x toolkit/delete_ALL_agents_registered_in_agentspace_app.sh
```

3. [DANGER] By running the following script ALL of the agents registered to the provided ENGINE_ID will be deleted :
```
./toolkit/delete_ALL_agents_registered_in_agentspace_app.sh
```

### [DANGER] Delete all authorizations registered to agentspace
1. Update .env file with your own information, particularly the ENGINE_ID with the ID of the Agentspace App you would like to delete agents from

2. run (only once): 
```
chmod +x toolkit/delete_ALL_auths.sh.sh
```

3. [DANGER] By running the following script ALL of the Authorizations registered in Agentspace (as SF_AUTHORIZATION_ID and SNOW_AUTHORIZATION_ID) will be deleted. This action can only be performed if no resource is actively using this authorization:
```
./toolkit/delete_ALL_auths.sh
```
