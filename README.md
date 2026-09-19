# FAQ Chatbot

An NLP-based FAQ chatbot that answers user questions by finding the most similar question from a predefined FAQ dataset.

The chatbot uses **NLTK for text preprocessing** and **TF-IDF + Cosine Similarity** for question matching.

---

## Features

* Loads FAQs from a CSV file
* Automatically detects common question/answer column names
* Text preprocessing using NLTK
* Lowercasing and punctuation removal
* Tokenization
* Stopword removal
* POS-aware lemmatization
* TF-IDF vectorization
* Cosine similarity-based matching
* Similarity threshold for uncertain questions
* Interactive command-line chatbot
* Works with custom FAQ datasets

---

## How It Works

```text
                FAQ CSV
                   │
                   ▼
          Load Questions/Answers
                   │
                   ▼
          Text Preprocessing
                   │
          ┌────────┴────────┐
          │                 │
      Tokenization     Lemmatization
          │                 │
          └────────┬────────┘
                   ▼
             TF-IDF
             Vectorization
                   │
                   ▼
            User Question
                   │
                   ▼
             TF-IDF Vector
                   │
                   ▼
        Cosine Similarity
                   │
                   ▼
          Most Similar FAQ
                   │
             ┌─────┴─────┐
             │           │
        Above Threshold  Below
             │           │
             ▼           ▼
          Answer      Fallback
```

---

## Repository Structure

```text
FAQ_Chatbot_app/
│
├── faq_chatbot.py
├── sample_faqs.csv
├── requirements.txt
└── README.md
```

### Files

| File               | Description                         |
| ------------------ | ----------------------------------- |
| `faq_chatbot.py`   | Main chatbot and NLP matching logic |
| `sample_faqs.csv`  | Example FAQ dataset                 |
| `requirements.txt` | Python dependencies                 |
| `README.md`        | Project documentation               |

---

## Technologies Used

* **Python**
* **Pandas** — CSV and data handling
* **NLTK** — NLP preprocessing and lemmatization
* **Scikit-learn** — TF-IDF and cosine similarity

---

## Installation

Clone the repository:

```bash
git clone <your-repository-url>
cd FAQ_Chatbot_app
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Dataset Format

The chatbot expects a CSV containing question-answer pairs.

Example:

```csv
question,answer
"What is your refund policy?","You can request a refund within 30 days."
"How can I contact support?","You can contact support through our help center."
"How long does shipping take?","Standard shipping usually takes 3-5 business days."
```

The program can also work with datasets using columns such as:

```text
instruction,response
```

or other supported question/answer column names.

---

## Running the Chatbot

Using the sample dataset:

```bash
python faq_chatbot.py sample_faqs.csv
```

Using your own dataset:

```bash
python faq_chatbot.py your_faqs.csv
```

---

## Example

```text
FAQ Chatbot
Type 'quit' to exit.

You: How long will my delivery take?

Bot: Standard shipping usually takes 3-5 business days.

You: What is your refund policy?

Bot: You can request a refund within 30 days.

You: Tell me about quantum computing

Bot: I'm not confident about the answer. Please rephrase your question.
```

---

## NLP Preprocessing

Before matching questions, the chatbot performs several preprocessing steps:

1. Convert text to lowercase
2. Remove punctuation
3. Tokenize the text
4. Remove stopwords
5. Perform POS tagging
6. Apply POS-aware lemmatization

For example:

```text
"How long does shipping take?"
             ↓
"long shipping take"
```

Lemmatization helps normalize related words so that variations such as different grammatical forms can be matched more effectively.

---

## TF-IDF

The processed FAQ questions are converted into numerical vectors using **Term Frequency-Inverse Document Frequency (TF-IDF)**.

TF-IDF gives higher importance to words that are useful for distinguishing one FAQ from another.

For example:

```text
"refund policy"
"shipping policy"
"payment policy"
```

Words such as `refund`, `shipping`, and `payment` help distinguish the questions.

---

## Cosine Similarity

When a user asks a question, it is converted into a TF-IDF vector and compared with all FAQ vectors using cosine similarity.

The FAQ with the highest similarity score is selected.

```text
User Question
      ↓
TF-IDF Vector
      ↓
Compare with FAQ Vectors
      ↓
Cosine Similarity
      ↓
Highest Score
      ↓
Corresponding Answer
```

A similarity threshold prevents the chatbot from confidently returning an unrelated answer.

---

## Limitations

This chatbot is primarily **word-overlap based**.

For example:

```text
FAQ:
"What is your refund policy?"

User:
"How can I get my money back?"
```

These questions have similar meanings but may have limited vocabulary overlap, causing TF-IDF similarity to be low.

The chatbot also does not generate new answers. It retrieves the answer associated with the closest FAQ.

---

## Future Improvements

The project can be extended with:

* **Sentence Transformers** for semantic similarity
* FAISS for faster vector search
* Streamlit web interface
* Conversation history
* Top-3 FAQ suggestions
* Confidence scoring
* Multilingual FAQ support
* Database-backed FAQ storage
* Admin interface for adding/editing FAQs
* LLM-based fallback responses
* Retrieval-Augmented Generation (RAG)

A semantic embedding model such as `sentence-transformers` would significantly improve matching for paraphrased questions.

---

## Learning Concepts

This project demonstrates practical concepts in:

* Natural Language Processing
* Text preprocessing
* Tokenization
* Stopword removal
* Lemmatization
* TF-IDF
* Vector similarity
* Information retrieval
* Classification/matching
* Python file and CSV handling

---

## License

This project is intended for educational and portfolio purposes.
