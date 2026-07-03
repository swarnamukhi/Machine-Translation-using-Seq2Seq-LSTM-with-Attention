# Chapter 5: Teacher Forcing

Teacher Forcing is a training technique used in Seq2Seq models where the decoder receives the **correct previous target word** instead of its own predicted word while learning.

This helps the decoder learn the target language faster and more accurately.

---

## 5.1 Why is Teacher Forcing Required?

Suppose we want to translate

```
English

I love India
```

to

```
French

J'aime l'Inde
```

During training, the decoder does not know French.

Its weights are randomly initialized, so its first predictions are usually incorrect.

If these incorrect predictions were continuously fed back into the decoder, the errors would accumulate, making learning very slow.

Teacher Forcing solves this problem by providing the correct previous target word during training.

---

## 5.2 Decoder Input and Decoder Target

Before training, the target sentence is modified by adding special tokens.

Original Sentence

```
J'aime l'Inde
```

↓

After preprocessing

```
<SOS> J'aime l'Inde <EOS>
```

Now two sequences are created.

### Decoder Input

```
<SOS> J'aime l'Inde
```

### Decoder Target

```
J'aime l'Inde <EOS>
```

These sequences are created during preprocessing before training starts.

---

## 5.3 How Does Teacher Forcing Work?

Suppose the decoder starts with

```
<SOS>
```

The decoder predicts

```
J'aime
```

Whether the prediction is correct or incorrect, during training the next input is the **correct word** from the dataset.

```
Input

<SOS>

↓

Predict

J'aime

↓

Next Input

J'aime
```

Next

```
Input

J'aime

↓

Predict

l'Inde

↓

Next Input

l'Inde
```

Finally

```
Input

l'Inde

↓

Predict

<EOS>
```

This process continues until the complete sentence is generated.

---

## 5.4 Why Not Use the Predicted Word During Training?

Suppose the decoder predicts

```
Bonjour
```

instead of

```
J'aime
```

If we use

```
Bonjour
```

as the next input,

all future predictions become less accurate.

This causes error accumulation.

Teacher Forcing avoids this by always providing the correct previous word during training.

As a result, the decoder learns faster and converges more efficiently.

---

## 5.5 What Happens During Inference?

Teacher Forcing is used **only during training**.

During inference (prediction), the correct target sentence is not available.

Therefore, the decoder uses its own previous prediction as the next input.

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

The decoder continues until it predicts the `<EOS>` token.

---

## 5.6 Teacher Forcing Workflow

```
Target Sentence

<SOS> J'aime l'Inde <EOS>

↓

Create

Decoder Input

<SOS> J'aime l'Inde

↓

Create

Decoder Target

J'aime l'Inde <EOS>

↓

Training

Decoder Input

↓

Prediction

↓

Compare with

Decoder Target

↓

Loss

↓

Backpropagation

↓

Update Weights
```

---

## Interview Points

### Why do we use Teacher Forcing?

Teacher Forcing speeds up training by feeding the correct previous target word to the decoder instead of its own prediction.

---

### Is Teacher Forcing used during inference?

No.

Teacher Forcing is only used during training.

During inference, the decoder uses its own predicted word as the next input.

---

### Why are `<SOS>` and `<EOS>` required?

`<SOS>` tells the decoder where to begin generating the sentence.

`<EOS>` tells the decoder where to stop generating the sentence.

---

## Key Takeaways

✔ Teacher Forcing is used only during training.

✔ The decoder receives the correct previous target word.

✔ Decoder Input and Decoder Target are created during preprocessing.

✔ Teacher Forcing reduces error accumulation.

✔ During inference, the decoder uses its own previous prediction.
