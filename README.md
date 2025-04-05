# Book Recommendation System with LLaMA and Qdrant (RAG Practice)

This project implements a book recommendation system using a combination of the **Qdrant** vector database and **LLaMA** (Large Language Model) API. The system retrieves relevant books based on user input and suggests them using a chat-based interface.

## Project Overview

The system uses a **Qdrant** collection to store book data (such as genre) in vectorized form. It utilizes **Sentence Transformers** to generate sentence embeddings for each book's genre and stores the vectors in the Qdrant collection. When the user inputs a query (e.g., "Suggest me a good psychology book"), the system searches the Qdrant collection for the closest matching books, which are then passed to the **LLaMA model** for generating responses based on the user's query.

## Requirements

- **Python 3.8+**
- **Sentence-Transformers** (for generating embeddings)
- **Qdrant-Client** (for vector search)
- **Requests** (for interacting with the LLaMA API)

### Dependencies
Install the necessary packages via `pip`:
`pip install -r requirements.txt`

## Setup

### Download the Dataset

The dataset `goodreads_books_by_genre.csv` should contain columns such as book titles, authors, and genres. Ensure this CSV is available in the project folder.

### Set Up Qdrant and LLaMA API

1. **Install and set up your Qdrant server:**
   - You can run it in-memory for quick setup or install it on your system. Follow the [Qdrant installation guide](https://qdrant.tech/documentation/).

2. **Install and set up your LLaMA API server locally:**
   - Use models like `LLaMA-3.2-1B-Instruct.Q6_K.gguf`. Refer to the official [LLaMA documentation](https://github.com/facebook/llama) for installation and setup.

## Usage

### Load Data and Prepare Vectorized Search

- The data from `goodreads_books_by_genre.csv` is loaded and sampled for processing. The genre information of each book is then encoded into a vector using a **Sentence Transformer** model (`all-MiniLM-L6-v2`).

### Create Qdrant Collection

- A Qdrant collection is created in memory to store the books' embeddings and their associated metadata (payload). The vector size is based on the **Sentence Transformer** model's output dimension.

### Upload Books to Qdrant

- Each book in the sampled dataset is uploaded to the Qdrant collection. For each book, its genre is encoded into a vector, and metadata (such as book title, author, genre) is stored as a payload.

### User Query

- The user inputs a query (e.g., "Suggest me a good psychology book"). The query is encoded into a vector using the same **Sentence Transformer** model, and the Qdrant collection is searched for the top matching book genres.

### Interaction with LLaMA API

- The search results (books) are then passed to the **LLaMA model API**, which generates a chatbot-like response, suggesting books based on the query.

### Output

- The response from the **LLaMA model** is printed, including the recommended books based on the user's query.

## Troubleshooting

- Ensure the **Qdrant** server is running correctly and accessible at `http://127.0.0.1:8080`.
- Verify the **LLaMA model server** is running locally.
- Adjust the model name or other parameters based on your setup.

## Contributing

Feel free to fork this project, open issues, or submit pull requests if you have improvements or fixes!