# Chapter 7: Attention Mechanism

The basic Seq2Seq model uses only the encoder's final hidden state to initialize the decoder. While this works well for short sentences, it struggles with long sentences because important information from earlier words may be lost.

The **Attention Mechanism** solves this problem by allowing the decoder to access **all encoder hidden states** while generating each target word.

---

## 7.1 Why is Attention Required?

Consider the sentence:

```
The boy who is wearing a blue shirt is playing football.
```

In a basic Seq2Seq model, the encoder compresses the entire sentence into a single hidden state.

```
Sentence

↓

Encoder

↓

Final Hidden State
```

As the sentence becomes longer, it becomes difficult for a single hidden state to remember all the important information.

Attention removes this limitation.

---

## 7.2 Basic Seq2Seq vs Attention

### Basic Seq2Seq

```
Encoder

h1  h2  h3  h4  h5

↓

Only h5

↓

Decoder
```

The decoder receives only the final hidden state.

---

### Attention-Based Seq2Seq

```
Encoder

h1  h2  h3  h4  h5

↓

Attention

↓

Decoder
```

The decoder can access **all encoder hidden states**.

---

## 7.3 How Does Attention Work?

Suppose the encoder processes

```
I love India
```

Encoder outputs

```
h1

h2

h3
```

When generating the first French word,

the decoder compares its current hidden state with

```
h1

h2

h3
```

It calculates attention scores to determine which encoder hidden states are most relevant.

Example

```
Attention Scores

h1 → 0.20

h2 → 0.30

h3 → 0.50
```

These scores indicate how much attention should be given to each encoder hidden state.

---

## 7.4 Context Vector

The attention scores are used to create a **Context Vector**.

The Context Vector is a weighted combination of all encoder hidden states.

```
h1 × 0.20

+

h2 × 0.30

+

h3 × 0.50

↓

Context Vector
```

The decoder uses this Context Vector along with its own hidden state to predict the next target word.

---

## 7.5 Why Are Only Hidden States Used?

The hidden state contains the contextual representation required for prediction.

The cell state is internal memory used only by the LSTM itself.

Therefore,

```
Hidden States

↓

Attention
```

but

```
Cell States

×

Not used by Attention
```

---

## 7.6 Decoder Workflow with Attention

```
Encoder

↓

h1

h2

h3

↓

Decoder Hidden State

↓

Attention Scores

↓

Context Vector

↓

Context + Decoder Hidden State

↓

Dense Layer

↓

Softmax

↓

Predicted Word
```

This process repeats for every target word.

---

## 7.7 Advantages of Attention

- Better translation of long sentences.
- Preserves important contextual information.
- Reduces information bottleneck.
- Improves translation accuracy.
- Forms the foundation of Transformer models.

---

## Interview Points

### Why is the final hidden state not enough?

Because a single hidden state cannot effectively represent very long sentences.

---

### Why are all encoder hidden states required?

Different output words may depend on different parts of the input sentence.

Attention allows the decoder to focus on the most relevant hidden states for each prediction.

---

### Why are cell states not used?

Cell states are internal LSTM memory.

Attention requires contextual representations, which are stored in the hidden states.

---

### Does Attention replace the Encoder?

No.

The encoder still processes the source sentence.

Attention simply provides additional information to the decoder.

---
---

# Attention vs Bahdanau Attention

Many beginners think **Attention** and **Bahdanau Attention** are different concepts. They are not.

**Attention** is a general mechanism that allows the decoder to focus on the most relevant encoder hidden states while generating each target word.

**Bahdanau Attention** is one specific implementation of the Attention mechanism, proposed by Dzmitry Bahdanau in 2014. It is also called **Additive Attention**.

Later, other attention mechanisms were introduced.

| Attention Type | Description |
|---------------|-------------|
| Bahdanau Attention | Additive Attention (used in this project) |
| Luong Attention | Multiplicative (Dot-Product) Attention |
| Self-Attention | Used in Transformer models such as BERT and GPT |

In this repository, whenever we refer to **Attention**, we specifically mean **Bahdanau Attention**.

---
---

# Bahdanau Attention Workflow

```text
Encoder Hidden States (h1, h2, h3, ..., hT)
                 │
                 │
                 ▼
Current Decoder Hidden State
                 │
                 ▼
Bahdanau Attention
      │
      ├── Compute Attention Scores
      │
      ├── Convert Scores → Attention Weights (Softmax)
      │
      ├── Compute Weighted Sum of Encoder Outputs
      │
      ▼
Context Vector
      │
      ▼
Context Vector + Decoder Hidden State
      │
      ▼
Decoder predicts the next English word
```

### Quick Summary

1. Encoder processes the entire Telugu sentence.
2. Decoder generates one English word at a time.
3. Before generating each word, Bahdanau Attention compares the current decoder hidden state with all encoder hidden states.
4. It computes attention scores.
5. Softmax converts the scores into attention weights.
6. The attention weights create a Context Vector.
7. The Context Vector is sent to the decoder.
8. The decoder predicts the next English word.

---

## Key Takeaways

✔ Attention solves the information bottleneck problem.

✔ The decoder accesses all encoder hidden states.

✔ Attention computes scores to determine which input words are most relevant.

✔ A Context Vector is created using the attention scores.

✔ The Context Vector helps the decoder generate more accurate translations.
