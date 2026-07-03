# Chapter 4: Decoder

The **Decoder** is the second component of a Seq2Seq model. Its responsibility is to generate the translated sentence one token at a time using the contextual information learned by the encoder.

Unlike the encoder, which only understands the input sentence, the decoder is responsible for generating the target language.

---

## 4.1 What is a Decoder?

A Decoder is an LSTM network that receives the encoder's final hidden state and cell state as its initial memory.

Using this information, it generates the translated sentence one word at a time.

Example

```
Encoder

↓

state_h
state_c

↓

Decoder

↓

J'aime l'Inde
```

---

## 4.2 Why do We Need a Decoder?

Understanding a sentence and generating a sentence are two different tasks.

The encoder learns the meaning of the source sentence.

The decoder converts that learned representation into a sentence in the target language.

Without a decoder, the model would understand the input sentence but would never generate a translation.

---

## 4.3 Input to the Decoder

The decoder receives three important inputs.

### 1. Encoder Final Hidden State

```
state_h
```

This initializes the decoder's hidden state.

---

### 2. Encoder Final Cell State

```
state_c
```

This initializes the decoder's cell state.

---

### 3. Previous Target Token

During training

```
<SOS>

↓

J'aime

↓

l'Inde
```

During inference

```
<SOS>

↓

Previous Prediction
```

---

## 4.4 What Happens Inside the Decoder?

Suppose the encoder has already processed

```
I love India
```

The decoder starts with

```
Input

<SOS>

Hidden State

state_h

Cell State

state_c
```

The decoder LSTM computes

```
decoder_h1

decoder_c1
```

The hidden state is passed to

```
Dense Layer

↓

Softmax

↓

Predict First Word
```

The decoder then receives the next input token and repeats the same process until it predicts the `<EOS>` token.

---

## 4.5 What Does the Decoder Learn?

The decoder learns:

- Target language grammar.
- Word ordering.
- Sentence generation.
- When to stop generating (`<EOS>`).
- How to generate the next word based on previous words.

Unlike the encoder, the decoder learns to generate words in the target language.

---

## 4.6 Output of the Decoder

At every time step, the decoder produces:

```
Hidden State

decoder_h
```

```
Cell State

decoder_c
```

```
Prediction

Next Word
```

The hidden state is used to:

- Continue the next decoder step.
- Predict the next word.
- Compute attention scores (in Attention-based models).

The cell state is passed only to the next decoder step.

---

## 4.7 Decoder Workflow

```
Encoder

↓

state_h
state_c

↓

Decoder

↓

Hidden State

↓

Dense Layer

↓

Softmax

↓

Predicted Word

↓

Next Decoder Step
```

This process continues until the decoder predicts the `<EOS>` token.

---

## Interview Points

### Why doesn't the decoder start with an empty hidden state?

Because it needs information about the source sentence. The encoder's final hidden state and cell state provide this initial context.

---

### Does the decoder know the target language before training?

No.

Initially, the decoder's weights are randomly initialized. During training, it gradually learns the target language by minimizing prediction errors using backpropagation.

---

### Why does the decoder generate one word at a time?

Because language is sequential. Each predicted word depends on the previously generated words.

---

## Key Takeaways

✔ The decoder is an LSTM network.

✔ It starts with the encoder's final hidden state and cell state.

✔ It generates one word at a time.

✔ The Dense and Softmax layers convert the decoder output into word probabilities.

✔ Generation stops when the `<EOS>` token is predicted.
