#----------------------scm-assistant-bot---------------------------
A RAG chatbot in Flowise that answers questions about a supplier network using the two data files provided.
### Public Chatbot
[PUBLIC_URL] https://cloud.flowiseai.com/chatbot/4958d508-571e-4dc9-bf43-8e8b250ba984

### Tech Stack
- Flowise
- Pinecone
- Groq
- HuggingFace BGE Embeddings
- CSV Supplier Dataset
- Governance Policy PDF


##--------------------------Demo---------------

<img width="1600" height="772" alt="E" src="https://github.com/user-attachments/assets/c035e16c-e00b-43fc-baa9-55f11347459a" />

<img width="1600" height="824" alt="F" src="https://github.com/user-attachments/assets/28dacba0-0978-40f2-b0b0-da19004fe6bc" />

The chatbot allows users to query supplier performance, governance policies, risk classifications, disruption handling procedures, and compliance metrics using natural language.

##---------------------------Business Problem-------------

## Business Problem

Large organizations often maintain supplier information across spreadsheets, reports, and governance manuals.

Finding answers to questions such as:

- Which suppliers qualify for incentive programs?
- Which suppliers are under watch-list restrictions?
- Which suppliers require escalation?
- Which suppliers violate governance policies?

usually requires manual searching across multiple documents.

This project reduces that effort by combining structured supplier records with governance policies into a searchable knowledge base.


##---------------------------Architecture -------------------

<img width="1200" height="1600" alt="Architechture" src="https://github.com/user-attachments/assets/54f07e43-a12f-43ea-8b85-0781692e7b98" />

##-----------------------WorkFlow--------------------------------

1. Supplier records are loaded from CSV files.
2. Governance rules are loaded from a PDF policy document.
3. Documents are embedded using BAAI/bge-small-en-v1.5.
4. Embeddings are stored in Pinecone.
5. User questions trigger semantic retrieval.
6. Retrieved context is sent to Groq LLM.
7. Grounded responses are generated.

##-----------------------Document Processing--------------------------------

## Retrieval Strategy

Two chunking strategies were evaluated.

### Strategy 1

PDF:
- Recursive Character Splitter
- Chunk Size: 500
- Chunk Overlap: 100

### Strategy 2

PDF:
- Recursive Character Splitter
- Chunk Size: 1000
- Chunk Overlap: 200

Final selection:
Chunk Size 1000 and Overlap 200 provided more complete policy retrieval and fewer fragmented answers.

#--------------------Output-----------------------

## Question 1

<img width="1600" height="801" alt="Question_1_A" src="https://github.com/user-attachments/assets/b56d90ce-862a-4299-b076-88c4a40fbd2f" />

<img width="1600" height="761" alt="Question_1_B" src="https://github.com/user-attachments/assets/dbb4ac02-bdb5-4280-97d1-94e331a0c1fa" />

## Question 2

<img width="1600" height="628" alt="Question_2_A" src="https://github.com/user-attachments/assets/8c5fa9c8-0d9b-4b3b-bce2-47797507a37d" />

<img width="1600" height="628" alt="Question_2_B" src="https://github.com/user-attachments/assets/99ddc6a8-f52f-4589-97dd-a7da4b84f866" />

##  Question 3

<img width="1600" height="803" alt="Question_3_A" src="https://github.com/user-attachments/assets/a19de0c4-9ea8-4e30-b0c0-4ec89177fa21" />

<img width="1600" height="805" alt="Question_3_B" src="https://github.com/user-attachments/assets/c25567be-698c-4604-9f1b-625d18445123" />

<img width="1600" height="805" alt="Question_3_C" src="https://github.com/user-attachments/assets/e6c3af56-96fc-4362-9ec8-5eb64e2beb63" />

## Question 4

<img width="1600" height="805" alt="Question_4_A" src="https://github.com/user-attachments/assets/8ef23c5f-2a9d-4d8e-87dc-f1a6e75978b2" />

<img width="1600" height="812" alt="Question_4_B" src="https://github.com/user-attachments/assets/562055d1-b693-41ef-8839-7ccaf3509b1b" />

## Question 5

<img width="1600" height="815" alt="Question_5_A" src="https://github.com/user-attachments/assets/b231f838-3a8f-496c-9b6b-f5c43d14e2bd" />

<img width="1600" height="768" alt="Question_5_B" src="https://github.com/user-attachments/assets/5aef7a4c-a5f8-4933-85d5-9267f9f9ea77" />

<img width="1600" height="768" alt="Question_5_C" src="https://github.com/user-attachments/assets/a268f29d-a1e6-45e9-9bac-c3484d1fd532" />

##-------------------------------LLM & Embeddings Used----------------------

## Models Used

### LLM

meta-llama/llama-4-scout-17b-16e-instruct

### Embeddings

BAAI/bge-small-en-v1.5

##----------------------------Challenges--------------------

## Challenges Encountered

During development several retrieval issues were observed:

1. Policy chunks sometimes dominated retrieval results.
2. Supplier-specific questions occasionally returned policy sections.
3. Large chunk sizes reduced retrieval precision.
4. API rate limits were encountered while testing.

Mitigations:

- Created a dedicated namespace.
- Tuned Top-K retrieval.
- Reprocessed PDF chunks.
- Validated retrieval results before deployment.


##----------------Limitation----------------------------------
## Current Limitations

- No reranking layer
- No hybrid keyword search
- Limited evaluation dataset
- No supplier dashboard
- No structured SQL querying

##------------------------------Future Improvements--------------------
## Future Improvements

Potential enhancements:

- Hybrid Search (Vector + Keyword)
- Metadata Filtering
- Cross-Encoder Reranking
- LangGraph Agent Workflow
- Supplier Analytics Dashboard
- Feedback-based Answer Evaluation
- Automated Governance Alerts
- Multi-document reasoning

  
