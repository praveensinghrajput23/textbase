---
sidebar_position: 1
---

# Cohere Chat bot

This chat bot makes an API call to Cohere and processes the user input and also maintain the chat history of user and system. It uses command  model by default. More information added in Cohere Class itself.

```py
from textbase import bot, Message
from textbase.models import Cohere
from typing import List

# Load your Cohere API key
Cohere.api_key = ""

# Prompt for `command` (cohere's model)
MESSAGE = "Is messi better than ronaldo or ronaldo better than messi?"

@bot()
def on_message(message_history: List[Message], state: dict = None):

    # Generate `command` (cohere's model) response
    bot_response = Cohere.chat(
        system_prompt=MESSAGE,
        user_name="user",
        message_history=message_history, # Assuming history is the list of user messages
        model="command",
    )

    response = {
        "data": {
            "messages": [
                {
                    "data_type": "STRING",
                    "value": bot_response
                }
            ],
            "state": state
        },
        "errors": [
            {
                "message": ""
            }
        ]
    }

    return {
        "status_code": 200,
        "response": response
    }
```