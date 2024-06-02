# Th3MayarBot
This is a custom bot, tested with the Gemini functionality, consuming the API.

## Installing Dependencies

  - **Prerequisites:** Ensure you have Python installed on your system. You can download it from the official website: https://www.python.org/

  - **Package Installation:** Open a terminal or command prompt and run the following command to install the required libraries using pip:

      ```
      pip install google-cloud-dialogflow
      ```

## Importing Libraries

  - **Import Statements:** In your Python script, include the necessary libraries using import statements:

      ```
        import os  # For interacting with the operating system
        from google.cloud import dialogflow_v2 as dialogflow  # For interacting with Dialogflow API
        import uuid  # For generating unique session IDs
      ```

## Setting Up Credentials

  API Key:
  
  + Obtain your API key from the Google Cloud Console's "APIs & Services" section. Create a Dialogflow project if you haven't already.
  + Set an environment variable named YourCredentialAPIKey to point to the path of your credentials file (usually a JSON file):

    ```
    os.environ["YourCredentialAPIKey"] = "/path/to/YourCredentialService.json"
    ```

## Project Configuration

  Project ID:
  
  + **Retrieve your project ID from the Google Cloud Console.** It's located in the top navigation bar of the project dashboard.

  Location and Session:
  
    project_id = "your_project_id"  # Replace with your actual project ID
    location = "global"  # This is the default location
    session_id = str(uuid.uuid4())  # Generate a unique session ID
    session_client = dialogflow.SessionsClient()
    session = session_client.session_path(project_id, session_id)


## Defining the Response Function

  Retrieving User Input:

    def get_response(query):
    text_input = dialogflow.TextInput(text=query, language_code="es")
    query_input = dialogflow.QueryInput(text=text_input)
    return session_client.detect_intent(session=session, query_input=query_input).query_result.fulfillment_text

## Example Usage

    Sample Query and Response:
    query = "Hello Th3MayarBot, How are you?"
    response_query = get_response(query)
    print("Th3MayarBot:", response_query)

## Continuous Interaction Loop

  Prompting for User Input:

    while True:
      query = input("You: ")
      if query.lower() in ["go out", "bye", "exit"]:
          print("Th3MayarBot: Bye!")
          break
      response_query = get_response(query)
      print("Th3MayarBot:", response_query)

