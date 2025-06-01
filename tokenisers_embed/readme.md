---

# Understanding Language Models: Key Concepts

---

## 1. Tokenization

**Q: What is a token in language models?**
A token is a unit of text that the model processes. It can be a whole word, a subword piece, a character, or a byte-pair encoding. Models break down input text into these tokens before understanding or generating language.

**Q: How do different tokenizers like BPE, WordPiece, and SentencePiece work?**

* **BPE (Byte Pair Encoding):** Iteratively merges frequent pairs of characters or subwords into tokens.
* **WordPiece:** Similar to BPE but optimized for handling rare words and out-of-vocabulary tokens.
* **SentencePiece:** Treats text as a raw byte stream and tokenizes without pre-tokenizing on spaces, useful for languages without clear word boundaries.

**Q: Why do token counts matter in LLMs?**
Token counts determine how much text the model can process or generate at once. Limits like `max_new_tokens` control output length. More tokens mean higher compute cost and latency.

**Q: How does tokenization affect text generation?**
Proper tokenization helps maintain sentence meaning and fluency. Poor tokenization can cause incomplete sentences, hallucinations, or abrupt cutoffs if token limits are reached.

---

## 2. Token Embeddings

**Q: What are token embeddings?**
Token embeddings are numerical vector representations of tokens. They capture semantic and syntactic information that the model uses to understand and generate language.

**Q: How do token IDs map to embeddings?**
Each token has a unique ID in the vocabulary. The model uses this ID to fetch the corresponding vector from the embedding matrix.

**Q: Why is embedding dimensionality important?**
The dimensionality (e.g., 768, 1024) determines how much information each token vector can hold. Higher dimensions can capture more nuanced meanings but require more computation.

**Q: How do embeddings capture similarity between words?**
Similar tokens have embeddings close to each other in vector space, allowing the model to generalize and understand related concepts.

---

## 3. Positional Embeddings

**Q: Why do models need positional embeddings?**
Transformers don’t inherently know token order. Positional embeddings add sequence order information so the model understands context and syntax.

**Q: What types of positional embeddings exist?**

* **Absolute positional embeddings:** Assign fixed position vectors to each token position.
* **Relative positional embeddings:** Encode token positions relative to each other, allowing better generalization to longer sequences.

**Q: How are positional embeddings combined with token embeddings?**
They are usually added together element-wise before being passed into the transformer layers.

---

## 4. End-to-End Flow (Text → Tokens → Embeddings → Model → Output)

**Q: What is the typical data flow in an LLM during inference?**
Text input → tokenized into IDs → mapped to embeddings → passed through transformer layers → model outputs logits → logits converted to token probabilities → tokens sampled/generated → decoded back to text.

**Q: What are `input_ids` and `attention_mask`?**

* `input_ids`: Token IDs representing the input text.
* `attention_mask`: A mask indicating which tokens should be attended to (1) or ignored/padded (0).

---

## 5. Vocabulary and Indexing

**Q: What is a vocabulary in LLMs?**
Vocabulary is the set of all tokens the model knows, each assigned a unique ID.

**Q: What are special tokens like `<pad>`, `<eos>`, and `<bos>`?**

* `<pad>`: Padding token used to fill sequences to the same length.
* `<eos>`: End of sequence token indicating text completion.
* `<bos>`: Beginning of sequence token indicating start of text.

**Q: How do token IDs relate to tokens?**
Token IDs are numerical representations of tokens, used internally by the model for efficient processing.

---

## 6. Attention Basics (High-Level)

**Q: What is attention in transformers?**
Attention allows the model to weigh the importance of different tokens in the input when generating each token, enabling context-aware processing.

**Q: Why is attention important?**
It lets the model focus on relevant parts of the input, helping with tasks like translation, summarization, and answering questions.

---

## 7. Word2Vec and GloVe Embeddings

**Q: What is Word2Vec?**
Word2Vec is a method to create word embeddings by training a neural network to predict words given their context (Skip-gram) or predict context from words (CBOW). It captures semantic relationships by placing similar words closer in vector space.

**Q: What is GloVe?**
GloVe (Global Vectors for Word Representation) creates embeddings by factorizing a word co-occurrence matrix, capturing global statistics of word usage. It combines the benefits of count-based and predictive models.

**Q: How do Word2Vec and GloVe differ from transformer embeddings?**
Word2Vec and GloVe produce static embeddings where each word has a fixed vector. Transformer embeddings are contextual, meaning the same word can have different vectors depending on its sentence context.

---
