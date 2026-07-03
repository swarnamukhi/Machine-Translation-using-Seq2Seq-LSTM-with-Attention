# Chapter 8: Inference (Prediction)

Inference is the process of using a trained Seq2Seq model to translate a new sentence that it has never seen before.

Unlike training, the correct target sentence is **not available** during inference. Therefore, the decoder must generate the translation one word at a time using its own previous predictions.

---

## 8.1 Training vs Inference

### Training

During training, the decoder receives the **correct previous target word** (Teacher Forcing).

```
Input

<SOS>

↓

Predict

J'aime

↓

Next Input

J'aime

↓

Predict

l'Inde

↓

Next Input

l'Inde
```

---

### Inference

During inference, the correct target sentence is unknown.

The decoder must use its **own previous prediction** as the next input.

```
<SOS>

↓

Predict

J'aime

↓

Input

J'aime

↓

Predict

l'Inde

↓

Input

l'Inde

↓

Predict

<EOS>
```

---

## 8.2 Complete Inference Workflow

```
English Sentence

↓

Tokenizer

↓

Embedding

↓

Encoder

↓

Encoder Hidden State

↓

Initialize Decoder

↓

Input <SOS>

↓

Predict First Word

↓

Use Prediction as Next Input

↓

Predict Next Word

↓

Repeat Until <EOS>
```

---

## 8.3 Step-by-Step Example

Suppose we want to translate

```
English

I love India
```

### Step 1

The encoder reads the complete sentence.

```
I

↓

love

↓

India
```

The encoder generates

```
state_h

state_c
```

and all hidden states (for Attention models).

---

### Step 2

The decoder starts with

```
<SOS>
```

Initial state

```
state_h

state_c
```

The decoder predicts

```
J'aime
```

---

### Step 3

Now the decoder uses

```
J'aime
```

as the next input.

It predicts

```
l'Inde
```

---

### Step 4

The decoder uses

```
l'Inde
```

as the next input.

It predicts

```
<EOS>
```

The translation process stops.

---

## 8.4 When Does the Decoder Stop?

The decoder continues generating words until one of the following conditions is met:

- The `<EOS>` (End of Sentence) token is predicted.
- The maximum sequence length is reached.

---

## 8.5 Greedy Search

The simplest decoding strategy is **Greedy Search**.

At each decoding step, the model selects the word with the highest probability.

Example

```
Word Probabilities

Bonjour   0.10

Merci     0.05

J'aime    0.80

Paris     0.05
```

Prediction

```
J'aime
```

Greedy Search is fast but may not always produce the best overall translation.

---

## 8.6 Beam Search (Interview Overview)

Beam Search is an improved decoding strategy.

Instead of keeping only one prediction, Beam Search keeps multiple candidate sequences and chooses the one with the highest overall probability.

Advantages:

- Better translation quality.
- More accurate than Greedy Search.

Disadvantage:

- Slower than Greedy Search.

---

## Interview Points

### Is Teacher Forcing used during inference?

No.

Teacher Forcing is used only during training.

---

### Why does the decoder use its own prediction?

Because the correct target sentence is not available during inference.

---

### When does translation stop?

Translation stops when the decoder predicts the `<EOS>` token or reaches the maximum sequence length.

---

### Which decoding strategy is commonly used?

Greedy Search for simplicity and speed.

Beam Search for higher translation quality.

---

## Key Takeaways

✔ Inference is the prediction phase.

✔ Teacher Forcing is not used during inference.

✔ The decoder uses its own previous prediction as the next input.

✔ Translation stops when `<EOS>` is generated.

✔ Greedy Search and Beam Search are common decoding strategies.
