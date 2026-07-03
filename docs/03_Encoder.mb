# Chapter 3: Encoder

The **Encoder** is the first component of a Seq2Seq model. Its primary responsibility is to read the entire source sentence one token at a time and convert it into a meaningful contextual representation that captures the information required for translation.

The encoder does **not** translate the sentence. Its job is only to **understand** the input sentence.

---

## 3.1 What is an Encoder?

An Encoder is an LSTM network that processes the input sentence sequentially.

For every input token, the encoder updates its **hidden state** and **cell state**, gradually building an understanding of the entire sentence.

Example:

```
Input Sentence

I love India
```

```
I      → h1,c1

love   → h2,c2

India  → h3,c3
```

After processing the final token, the encoder has learned a contextual representation of the complete sentence.

---

## 3.2 Why do We Need an Encoder?

Computers cannot understand the meaning of an entire sentence at once.

Instead, the sentence is processed one word at a time.

The encoder gradually combines the information from previous words with the current word, allowing it to understand the complete sentence before translation begins.

Without an encoder, the decoder would have no understanding of the source sentence.

---

## 3.3 Input to the Encoder

The encoder receives the preprocessed source sentence.

```
English Sentence

↓

Tokenizer

↓

Integer Sequence

↓

Embedding Layer

↓

Encoder LSTM
```

The embedding layer converts each token into a dense vector before it is processed by the LSTM.

---

## 3.4 What Happens Inside the Encoder?

Suppose the sentence is

```
I love India
```

The encoder processes one token at a time.

```
Time Step 1

Input

I

↓

Embedding

↓

LSTM

↓

h1,c1
```

```
Time Step 2

Input

love

Previous State

h1,c1

↓

LSTM

↓

h2,c2
```

```
Time Step 3

Input

India

Previous State

h2,c2

↓

LSTM

↓

h3,c3
```

Each hidden state contains more contextual information than the previous one.

---

## 3.5 What Does the Encoder Learn?

The encoder learns:

- Word relationships
- Sentence context
- Word order
- Grammatical information
- Long-term dependencies

It does **not** learn the translated sentence.

Its only responsibility is to understand the source sentence.

---

## 3.6 Output of the Encoder

The encoder produces:

```
Hidden States

h1

h2

h3
```

and

```
Final Hidden State

h3
```

```
Final Cell State

c3
```

In a basic Seq2Seq model,

```
h3

c3
```

are passed to the decoder.

In an Attention-based Seq2Seq model,

```
h1

h2

h3
```

are also passed to the Attention mechanism.

---

## Interview Points

### Why does the encoder not generate words?

Because its responsibility is to understand the source sentence, not generate the target sentence.

---

### Does the encoder know French?

No.

The encoder only learns a representation of the source sentence.

The decoder learns how to generate the target language.

---

### Why are hidden states generated for every time step?

Each hidden state represents the sentence after reading one more token.

These hidden states are later used by the Attention mechanism.

---

## Key Takeaways

✔ The encoder is an LSTM network.

✔ It processes one token at a time.

✔ It updates the hidden state and cell state at every time step.

✔ The final hidden state and cell state initialize the decoder.

✔ In Attention models, all encoder hidden states are used during decoding.
