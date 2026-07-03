# Chapter 2: Seq2Seq Architecture

Seq2Seq (Sequence-to-Sequence) is one of the earliest and most successful Neural Machine Translation architectures. It is designed to translate an input sequence (source language) into an output sequence (target language), even when both sequences have different lengths.

---

## 2.1 What is a Seq2Seq Model?

A Sequence-to-Sequence (Seq2Seq) model is a deep learning architecture that accepts one sequence as input and generates another sequence as output.

Unlike traditional neural networks that produce a single output, Seq2Seq models generate an entire sequence one token at a time.

Example:

Source Sequence (English)

```
I love India
```

↓

Target Sequence (French)

```
J'aime l'Inde
```

The input and output sequences can have different lengths.

---

## 2.2 Why can't a Single LSTM perform Machine Translation?

A single LSTM works well for problems like:

- Sentiment Analysis
- Spam Detection
- Text Classification

because these tasks require **one output**.

Example:

```
I love this movie.

↓

Positive
```

Machine Translation is different.

Here,

```
Input

I love India

↓

Output

J'aime l'Inde
```

The model first needs to **understand** the English sentence and then **generate** a completely new French sentence.

Trying to perform both tasks using a single LSTM makes learning very difficult.

Therefore, the problem is divided into two separate tasks:

- Understanding the source sentence.
- Generating the target sentence.

---

## 2.3 Why are Two LSTM Networks Required?

Seq2Seq uses two specialized LSTM networks.

### Encoder

Responsible for understanding the source sentence.

```
English Sentence

↓

Encoder LSTM

↓

Sentence Representation
```

### Decoder

Responsible for generating the translated sentence.

```
Sentence Representation

↓

Decoder LSTM

↓

French Sentence
```

This separation allows each network to specialize in its own task.

---

## 2.4 High-Level Architecture

```
          Source Language

          I love India

                │

                ▼

        +----------------+
        | Encoder LSTM   |
        +----------------+

        state_h , state_c

                │

                ▼

        +----------------+
        | Decoder LSTM   |
        +----------------+

                │

                ▼

         J'aime l'Inde
```

The encoder reads the complete input sentence.

The decoder generates the translated sentence one word at a time.

---

## 2.5 Components of a Seq2Seq Model

A Seq2Seq model consists of:

- Input Layer
- Embedding Layer
- Encoder LSTM
- Hidden State
- Cell State
- Decoder LSTM
- Dense Layer
- Softmax Layer

Each component performs a specific task, which will be discussed in the upcoming chapters.

---

## Interview Points

### Q1. Why is it called Sequence-to-Sequence?

Because the model converts one sequence into another sequence.

```
Input Sequence

↓

Output Sequence
```

---

### Q2. Why do we need two LSTMs?

One LSTM specializes in understanding the source sentence (Encoder), while the other specializes in generating the target sentence (Decoder).

---

### Q3. Can the input and output sequences have different lengths?

Yes.

Example

English

```
I love India
```

French

```
J'aime l'Inde
```

The number of words does not have to be the same.

---

## Key Takeaways

✔ Seq2Seq is designed for sequence generation tasks.

✔ Machine Translation is not a classification problem.

✔ The Encoder understands the input sentence.

✔ The Decoder generates the translated sentence.

✔ Encoder and Decoder are two independent LSTM networks that work together.
