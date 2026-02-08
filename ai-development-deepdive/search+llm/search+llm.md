# AI Vector Search and Retrieval-Augmented Generation (RAG)

## Introduction

This lab guides you through the steps to retrieve database rows containing vectors, and the associated data chunks, that are close to the query/prompt in **vector space**. Then, we will use the most relevant text chunks to augment, or enhance, the query/prompt and present it to the LLM which will present a well-formed natural language response. This is the basic Retrieval-Augmented Generation (RAG) approach.

Estimated Time: 40 minutes

![overview](images/Station_05.png)

### Objectives
In this lab, you will:

- Examine for understanding, then execute the workshop python function "DB_AI_Vector_Search" that you defined in Lab 2, containing Python and SQL code to retrieve records from a vector database based on vector distance from a generalized query or prompt (the "prompt").
- Examine and execute previously defined workshop function "LLM_Search" which uses a Llama-3.2 multimodal large language model to retrieve a publicly available response to the prompt. This will be our baseline non-RAG response.
- Examine and execute previously defined workshop function "LLM_Search_using_RAG" which creates a new, enchanced prompt that uses the previous non-RAG response, the top chunks from the database vector search, and custom instructions.

## Task 1: AI Vector Search
In this step, we will take a text, supposedly a question the user is asking re: a relevant business issue, opportunity, etc. and transform it into a vector. We will then feed this vector to the database, where it will be used to retrieve **similar** vectors and associated metadata.
 
### Similarity Search
A similarity search looks for the relative order of vectors compared to a query vector.
The comparison is done using a particular **distance metric**, allowing us to return from the database a result set of the **top closest vectors** along with **the associated data Chunks most similar to the query** .

### Step 1: Executing the query
Below is an example of the similarity search process in SQL.

The similarity search guery returns the **vector\_data** , **doc\_id**, **chunk\_id** and **chunk\_data** columns from the USERINFO\_VECTOR table. It also returns the result of **VECTOR_DISTANCE** as **distance**
1. The SQL language function **VECTOR_DISTANCE** is used to calculate the distance between two vectors. Here, it takes **vector\_data** and **distance** as parameters.
2. **vector_data** contains the embedded vector data derived in Lab 3
3. SQL language function **VECTOR\_EMBEDDING** generates a single vector embedding for multiple data types using machine learning models. Here, we use the sentence transformer model **ALL\_MPNET\_BASE\_V2** used in Lab 3 to generate the embedding, using a plain text string.
4. The prompt from Lab3 is used as the VECTOR\_EMBEDDING 'USING' parameter. 
The similarity search guery returns the top ten rows from USERINFO\_VECTOR in ascending **distance** order.  The smallest vector distances between **vector_data** data and the prompt embedding indicates the most similar associated Chunks to the prompt text.

![overview](images/Station_06_large.png)
