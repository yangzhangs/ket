# General info
MLOps-KET is designed to create knowledge graph from the unstructured data accumulated in our study and provide LLM-powered Q&A service. It is implemented based on the Langchain framework, Meta Llama 3 model, and Neo4j database. 

![image](https://github.com/user-attachments/assets/684fae8d-ceac-49f6-8ad1-293ded6b2012)

MLOps-KET supports interact with the MLOps knowledge data in a Neo4j database through conversational queries. Its workflow involves two steps: 
- Construct knowledge graph: MLOps-KET uses Llama 3 model to transform unstructured MLOps knowledge documents (our findings and posts&issues data) into a lexical graph of documents and chunks (with all-MiniLM embedding model) and an entity graph with nodes and their relationships, which are both stored in a Neo4j database.
- Explore knowledge: When developer ask a question, MLOps-KET semantically search for relevant data within the KG database, and rank results based on their relevance to the input query. Then, the query and retrieved data are combined and input to the Llama 3 model to generate enriched answers.

## Setup instructions
- Clone or download our repository
- Create a .env file with your Llama 3 configuration (i.e., service address)
  - Install and use Ollama framework to call Llama 3 model 
- Run Docker Compose to build and start all components: `docker-compose up --build`
- Connect to the Neo4j database (provide protocal, URI, database name, username, and password)
  - You can start a Neo4j container like this:
    `docker run \
    --publish=7474:7474 --publish=7687:7687 \
    --volume=$HOME/neo4j/data:/data \
    --volume=$HOME/neo4j/logs:/logs \
    neo4j:latest`
  - The Neo4j URI should be `neo4j://database:7687`
- Upload the MLOps knowledge documents (in the `documents` folder)
  - `findings.txt`: Our empirical study findings
  - `data.csv`: SO posts and GH issues related to MLOps
  - `online.docs`: Online documentation related to MLOps 
- Click `Generate Graph` to turn MLOps knowledge documents into structured knowledge graphs using Llama 3 model
- After prossing, the MLOps knowledge has been stored in the Neo4j database
- Ask any questions related to MLOps, the chatbot search the knowledge graph database, and combine the query and retrieved data as input
- Llama 3 model generate answer according to the input
- Support view graph and retrive metadata about the source of response to the queries

## Usage examples
