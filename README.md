# embedchain

embedchain is a framework to easily create bots over any dataset.

* If you want to create a Naval Ravikant bot which has 1 youtube video, 1 book as pdf and 2 of his blog posts, all you need to do is add the links to the videos, pdf and blog posts and embedchain will create a bot for you.

```python

from embedchain import App

app = app()

app.add("youtube_video", "https://www.youtube.com/watch?v=3qHkcs3kG44")
app.add("pdf_file", "https://navalmanack.s3.amazonaws.com/Eric-Jorgenson_The-Almanack-of-Naval-Ravikant_Final.pdf")
app.add("web_page", "https://nav.al/feedback")
app.add("web_page", "https://nav.al/agi")

app.query("How to do a startup?")
```

# How to use it?

## Installation

First make sure that you have the package installed. If not, then install it using `pip`

```bash
pip install embedchain
```

## Usage

* We use OpenAI's embedding model to create embeddings for chunks and ChatGPT API as LLM to get answer given the relevant docs. Make sure that you have an OpenAI account and an API key.

* Once you have the API key, set it in an environment variable called `OPENAI_API_KEY`

```bash
export OPENAI_API_KEY='sk-xxxxxxxx'
```

* Next import the `App` class from embedchain and use `.add` function to add any dataset.

```python

from embedchain import App

app = App()

app.add("youtube_video", "https://www.youtube.com/watch?v=3qHkcs3kG44")
app.add("pdf_file", "https://navalmanack.s3.amazonaws.com/Eric-Jorgenson_The-Almanack-of-Naval-Ravikant_Final.pdf")
app.add("web_page", "https://nav.al/agi")
```

* Now you app is created. You can use `.query` function to get the answer for any query.

```python
print(app.query("How to do a startup?"))
```

# What problem does it solve?

Creating a chat bot over any dataset needs the following steps to happen

* load the data
* create meaningful chunks
* create embeddigns for each chunk
* store the chunks in vector database

Whenever a user asks any query, following process happens to find the answer for the query

* create the embedding for query
* find similar documents for this query from vector database
* pass similar documents as context to LLM to get the final answer.

The process of loading the dataset and then querying involves multiple steps and each steps has nuances of it is own.

* How should I chunk the data? What is a meaningful chunk size?
* How should I create embeddings for each chunk? Which embedding model should I use?
* How should I store the chunks in vector database? Which vector database should I use?
* Should I store meta data along with the embeddings?
* How should I find similar documents for a query? Which ranking model should I use?

These questions may be trivial for some but for a lot of us, it needs research, experimentation and time to find out the accurate answers.

embedchain is a framework which takes care of all these nuances and provides a simple interface to create bots over any dataset.

In the first release, we are making it easier for anyone to get a chatbot over any dataset up and running in less than a minute. All you need to do is create an app instance, add the data sets using `.add` function and then use `.query` function to get the relevant answer.

# Tech Stack

embedchain is built on the following stack:

- [langchain](https://github.com/hwchase17/langchain) as an LLM framework to load, chunk and index data,
- [OpenAI's Ada embedding model](https://platform.openai.com/docs/guides/embeddings) to create embeddings
- [OpenAI's ChatGPT API](https://platform.openai.com/docs/guides/gpt/chat-completions-api) as LLM to get answers given the context
- [Chroma](https://github.com/chroma-core/chroma) as the vector database to store embeddings

# Author

* Taranjeet Singh ([@taranjeetio](https://twitter.com/taranjeetio))