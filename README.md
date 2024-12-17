# InstagramCrewAI: Your AI-Powered Instagram Marketing Assistant 

## **Mission: Revolutionizing Instagram Marketing with AI** 🌟

Think of InstagramCrewAI as your **personal AI-powered Instagram strategist**, ready to provide you with the tools and insights you need to succeed. This project uses state-of-the-art AI technologies to create engaging visuals, write impactful captions, and design data-backed strategies for your Instagram account. 📈📸

# Planning our crew

<img width="1206" alt="Screenshot 2024-12-17 at 2 13 32 PM" src="https://github.com/user-attachments/assets/f56d33ea-bce5-480f-b23a-17575b948da9" />

The diagram above looks all very pretty, but in order to get there, we needed to do some thinking. The good news, is that CrewAI has a GPT that can help you with that. Just describe your situation to their assistant and it will help you plan your crew. It may give you the full agents and tasks that you need to define, or it may give you some ideas to start with.

# CrewAI CLI

This time, we will be bootstrapping our project using the CrewAI CLI. The CLI is a powerful tool that allows you to create all the components of a CrewAI project in a single command. The CLI comes installed with the CrewAI package, so you don’t need to install it separately:

	$ pip install crewai
	$ crewai create my-crew
This will create a new directory called my-crew with the following structure:

	my-crew/
	├── src/
	│   ├── my_crew/
	│   │   ├── __init__.py
	│   │   ├── crew.py
	│   │   ├── main.py
	│   │   ├── tools/
	│   │   │   ├── __init__.py
	│   │   │   ├── my_tool.py
	│   │   ├── config
	│   │   │   ├── agents.yaml
	│   │   │   ├── tasks.yaml
	│   │   │   ├── tools.yaml
	│   ├── tests/
	│   │   ├── __init__.py
	│   │   ├── test_crew.py
	│   │   ├── test_tools.py
	│   ├── __init__.py
	├── .gitignore
	├── README.md
	├── pyproject.toml
	├── .env.example
 
### As you can see, the CLI creates everything you need for a new crew project. The most important things to consider here are:

- Your agents configuration is defined in **src/my_crew/config/agents.yaml**. Here is where you will write their backstories, goals and other params that you need to define your agents.

- Your tasks configuration is defined in **src/my_crew/config/tasks.yaml**. Here is where you define the tasks that your agents will perform.
 
- Your crew is defined in **src/my_crew/crew.py**. Here is where you define your crew’s agents and their tasks. It contains all the decorators and functions you need to define your crew.This file loads the configuration from the **config** folder and creates the agents and tasks.
 
Now you will have to install the dependencies and create a .env file with your Serper API key. You can get your Serper API key by signing up at Serper.

	$ cd my-crew
	$ poetry lock 
	$ poetry install
	$ cp .env.example .env

# Adding our agents and tasks

Now that we have our agents and tasks defined, we can add them to our crew. We will be using the **@agent** and **@task** decorators to define our agents and tasks. We can go to **src/my_crew/crew.py** and add our agents and tasks there.


# Creating Tools that work

The tools are the functions that your agents will use to perform their tasks. They are defined in the **src/my_crew/tools folder**. You can create as many tools as you want, but it is recommended to keep them simple and focused on a single task.

In our case, we will be using Serper API to search the internet for information about a given topic. That tool will be used by our **market_researcher** agent to perform its tasks. We will also define a tool to open a webpage and read its content. This tool will require the **WebBaseLoader** class from the **langchain_community** package (for which we have to install **beautifultsoup4** and **requests**):


# Testing our crew

Now that we have our crew defined, we can test it by running the following command:

	$ poetry run my_crew

# My testing results

After running my crew, I got the following results:

# Giving Agents Memory

Communication between agents was good, but we did not implement memory here. This means that the agents were not able to remember information from previous tasks.

To be precise, at some pointm the Copy Writer agent asked the Market Researcher agent for information about the latest hashtags, and the Market Researcher agent started a whole new search on the internet. This is not ideal because the Market Researcher agent had already done that search before and even produced a report about it. It just did not remember that information.

This could also be solved by manually assigning the output of specific previous tasks as context to the tasks that need them. But that does not seem to be very easily done when using the CrewAI setup provided by the CLI.


# Delegating Tasks

In earlier test, some agents over-delegated tasks to other agents. This is not ideal because it can lead to too many API calls and raise the cost of running the crew. That is why I set the allow_delegation parameter to false in the visual_creator and copywriter agents.

Try to do this for all your agents that do not need to delegate tasks. This will make your crew more efficient and cost-effective.

🌟 InstagramCrewAI – Your AI Marketing Crew on Instagram 🌟
