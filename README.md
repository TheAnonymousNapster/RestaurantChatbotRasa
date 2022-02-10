# RestaurantChatbotRasa

# Restaurant ChatBot CCNLP Mini Project :
##  Members: 
- Nachiket Dunbray
- Jayesh Katade
- Sakshi Lad
- Sparsh Nimje

A restaurant chatbot using open source chat framework RASA : https://rasa.com/. Integrates with Zomato : https://developers.zomato.com/?lang=tr API to fetch restaurant information.

Here Interpreter is part of NLU and Tracker, policy and action are part of Core.

* The message is passed to an Interpreter, which converts it into a dictionary including the original text, the intent, and any entities that were found.

* The Tracker is the object which keeps track of the conversation state. It receives the info that a new message has come in. Know more about it here: https://rasa.com/docs/rasa/api/tracker-stores/

* The policy receives the current state of the tracker, chooses the next action which is logged by the tracker and response is sent to the user. There are different policies to choose from.
You will get more information here: https://rasa.com/docs/rasa/core/policies/#policies
Along with policy “slots” which act as bot’s memory(context). It also influences how the dialogue progresses. Read more about slots here: https://rasa.com/docs/rasa/core/slots/



# Library Installation :

## Pre-requisites :
* python 3.6.2
* rasa 2.1.0
* spacy 2.1.4
* en_core_web_md 2.1.0

### Create New Environment Variable :
- check no of env : conda env list or conda info --envs
- create : conda create -n RasaEnv python=3.7 anaconda
- conda activate RasaEnv
- conda deactivate
- conda env remove --name ENVIRONMENT

### Required Libraries :
- pip install rasa 
- pip install spacy
- python -m spacy download en_core_web_md

##### OR
- python -m spacy link en_core_web_md en

# RASA
- Refer to official installation guide : https://rasa.com/docs/rasa/user-guide/installation/ to install RASA

### NLU : 

##### Rasa NLU Run :
- rasa train nlu # train nlu model
- rasa shell nlu # test nlu model
- rasa test nlu # Evaluate nlu model
- rasa run actions # expose the nlu model 

##### Rasa Core Run :
- rasa train core # train core model
##### OR
- rasa train -vv -dump-stories --force 

#### Equivalent RASA CLI command: 
- rasa run actions # expose the core model
##### OR
#### Run RASA action server ( mandatory step to interact with chatbot) on port 5055
- python actions.py
- rasa run actions --actions actions -vv

#### Train RASA NLU and Core model
- python rasa_train.py

#### Equivalent RASA CLI command
- rasa train

#### Equivalent RASA CLI command
- rasa shell  # test core model
- rasa test core # Evaluate core model

#### Run RASA server to connect slack channel
- rasa run -m models -p 5005 --connector slack --credentials credentials.yml


# Run Chatbot :
### Terminal 1 :

### Start directly from here :
- rasa run -m models --enable-api --cors "*"

### Terminal 2 :
- ngrok http 5005 

 
# Project Information:

### Data Files :
* data/nlu.md : contains training examples for the NLU model
* data/stories.md : contains training stories for the Core model

## Script Files :
* zomato : contains Zomato API integration code
* zomato.py : contains functions to consume common Zomato APIs like fetch location details, type of cuisines, search for restaurants, etc
* actions.py : contains the following custom actions (insert ZOMATO API key in this script file before starting RASA server)

- search restaurant
- action_restart
- action_search_restaurants
- action_send_mail
- action_slot_reset
- action_validate_email
- validate location
- validate cuisine
- restart conversation
- reset slots

## Config Files : 
* config.yml contains model configuration and custom policy

* credentials.yml contains authentication token to connect with channels like slack

* domain.yml defines chatbot domain like entities, actions, templates, slots

* endpoints.yml contains the webhook configuration for custom action
 
 

### Slack Configuration :
* End url : /webhooks/slack/webhook

* Link 1: https://api.slack.com/

* Link 2: https://app.slack.com/client/T016GCA0T5K/D016XJ4Q75X

