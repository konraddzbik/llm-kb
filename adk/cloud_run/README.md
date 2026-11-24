## Google ADK Qucik start on your local machine 

## install python Python 3.9 or later
## pip 
### for a package installation 

## install google adk
bash
pip install google-adk
source ~/.zshrc # whats that for? 
## 

adk create my_agent 

## grab gemini API key from Google AI Studio- which has freemium

## edit .env file 
### You have to add your gemini api key, in case to work with gemini agent- we'll talk about gemini version later in this article
echo 'GOOGLE_API_KEY="YOUR_API_KEY"' > .env

## now you can run your agent in terminal 
adk run my_agent

## or you can use web browser with default localhost address
adk web 

## TIPS 
### You can specify the port if needed
adk web --port 6789

## now youre fully set to ejoy your localhost agent 


## how to add some advantages to the 
Second part of this artivcle will provide instructions, on how to use Google ADK witk ollama installed on your locall machine.

If you want ot use ollama with google adk, there's a need for additionall code and packages to wrap local models for interaction

first, add to 


# How to deploy you code to the cloud run with ADK and ollama from locall terminal and gcloud cli 
# go to google cloud conosle 
# create new project 

now in your terminal copy and run 

```bash
gcloud auth login
# not really, you can use gcloud config set project and TAB to list all of the prjects- like in terminal
gcloud projects list
gcloud config set project PROJECT_ID
```

### Ustal domyślne konto serwisowe dla wybranego projektu `default service account`

```bash
gcloud builds get-default-service-account
```

Activate python venv

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```


Tutaj mam zagadke, czy nie dodac tutaj lepiej w secret managerze tego gemini_ai_api_key klucza od AI 

nastepnie 
## What to do with default account to start
1. set COMPUTE_SA in .env or export COMPUTE_SA="your_service_account"
1. set GC_PROJECT_NAME in .env or export GC_PROJECT_NAME="GCP project name"
2. set this 
```bash
gcloud projects add-iam-policy-binding $GC_PROJECT_NAME \
  --member="serviceAccount:${COMPUTE_SA}" \
  --role="roles/storage.objectAdmin"
```
3. set this 
```bash
gcloud projects add-iam-policy-binding $GC_PROJECT_NAME \
  --member="serviceAccount:${COMPUTE_SA}" \
  --role="roles/artifactregistry.writer"
```

now you can deploy your ADK agents to the google cloud run 

*** be aware of the working directory, keep you chould be right "above" the agent directory for the reason of making it working on clouud run 

** your configuration wil work with google gemini 

comand to execute for a deployement 

   gcloud run deploy multi-tool-agent --source . --region europe-west1 --allow-unauthenticated --set-env-vars="GOOGLE_GENAI_USE_VERTEXAI=FALSE, GOOGLE_API_KEY="  --labels dev-tutorial=codelab-dos

** alllow unauthenticated- will not work 



### TIPS AND TRICKS

## logging 

gcloud builds log b8e53643-5dd3-4e4d-ae52-cec3de250867? \
 --region=europe-west1 \
 --project=kd-llm-cl-bielik