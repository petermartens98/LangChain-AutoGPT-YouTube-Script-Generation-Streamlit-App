# LangChain AutoGPT YouTube Script Generation Streamlit App
This is an app designed to generate YouTube video titles and scripts automatically using the GPT-3.5 language model. It utilizes Streamlit, a popular Python framework for building web applications, to create a user interface.

### Dependencies
The following dependencies are required to run the app:

os: Used for setting environment variables.

apikey (imported from apikey.py): Contains the API key required to access the GPT-3.5 model.

streamlit: The web framework used to build the user interface.

langchain.llms.OpenAI: A module that provides an interface to interact with the OpenAI language model.

langchain.prompts.PromptTemplate: Defines templates for generating prompts based on specific input variables.

langchain.chains.LLMChain: Represents a language model chain that generates outputs based on prompts and manages conversational memory.

langchain.memory.ConversationBufferMemory: A memory module that stores conversation history for specific input keys.

langchain.utilities.WikipediaAPIWrapper: A utility module that provides a wrapper for making API calls to Wikipedia.

### App Framework

The app's main interface is created using Streamlit. It consists of a title and a text input field where users can enter their desired prompt.

##### The following variables are initialized:

prompt: Stores the user's input prompt.

Prompt Templates

##### Two prompt templates are defined:

title_template: Takes a single input variable topic and generates a prompt for requesting a YouTube video title related to that topic.

script_template: Takes two input variables title and wikipedia_research and generates a prompt for requesting a YouTube video script based on the given title, while leveraging research from Wikipedia.

### Memory
##### Two conversation buffer memories are created:

title_memory: Stores conversation history based on the input key 'topic'. This memory is used to maintain context during the generation of video titles.

script_memory: Stores conversation history based on the input key 'title'. This memory is used to maintain context during the generation of video scripts.

### LLMs (Language Model Managers)
The app uses the GPT-3.5 model provided by OpenAI for generating titles and scripts.
##### The following LLMs are initialized:

llm: An instance of the OpenAI class, which provides an interface to interact with the GPT-3.5 model. The temperature is set to 0.9, which 
controls the randomness of the generated outputs.

title_chain: An LLMChain that utilizes the title_template prompt template. It is responsible for generating YouTube video titles based on user prompts. The generated title is stored in the output key 'title', and conversation history is stored in title_memory.

script_chain: An LLMChain that utilizes the script_template prompt template. It is responsible for generating YouTube video scripts based on user prompts, titles, and Wikipedia research. The generated script is stored in the output key 'script', and conversation history is stored in script_memory.

### Wikipedia API Wrapper
A wrapper class WikipediaAPIWrapper is used to make API calls to Wikipedia and retrieve research information based on the user's prompt. This information is utilized in the script_chain to generate more contextually relevant video scripts.

Displaying Results
If a prompt is provided by the user, the following steps are executed:

1. The title_chain generates a YouTube video title based on the prompt.
2. The wiki object retrieves research information from Wikipedia based on the prompt.
3. The script_chain generates a YouTube video script using the generated title and the retrieved Wikipedia research.
4. The generated title is displayed using st.write(title).
5. The generated script is displayed using st.write(script).
6. An expandable section titled "Title History" is created using st.expander('Title History').
7. Inside the "Title History" section, the conversation history stored in title_memory.buffer is displayed using st.info(title_memory.buffer).
8. An expandable section titled "Script History" is created using st.expander('Script History').
9. Inside the "Script History" section, the conversation history stored in script_memory.buffer is displayed using st.info(script_memory.buffer).
10. An expandable section titled "Wikipedia Research" is created using st.expander('Wikipedia Research').
11. Inside the "Wikipedia Research" section, the retrieved research information from Wikipedia (wiki_research) is displayed using st.info(wiki_research).

### Note
Uer will have to update apikey in apikey.py with their own OpenAI API key

### Example Outputs
#### Prompt: "Early Days of Apple Computing and Steve Jobs"
![image](https://github.com/petermartens98/AutoGPT-YouTube-Script-Generation-Streamlit-App/assets/87671757/3a468954-9925-4076-8c7a-ed77bf3626d9)
![image](https://github.com/petermartens98/AutoGPT-YouTube-Script-Generation-Streamlit-App/assets/87671757/cde2126c-f69e-4e11-9116-0af977ee0f51)

#### Prompt: "Michael Jordan's 1998 Season"
![image](https://github.com/petermartens98/AutoGPT-YouTube-Script-Generation-Streamlit-App/assets/87671757/62658104-9ad7-484e-abda-776902568639)
![image](https://github.com/petermartens98/AutoGPT-YouTube-Script-Generation-Streamlit-App/assets/87671757/38411898-6f58-45e1-b19c-cf4362927024)
