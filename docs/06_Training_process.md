# Chapter 6: Complete Training Process

Training a Seq2Seq model involves teaching the encoder and decoder to work together so that the model can translate a sentence from the source language to the target language.

During training, both the encoder and decoder learn simultaneously through forward propagation, loss calculation, and backpropagation.

---

## 6.1 Complete Training Pipeline

```
Parallel Dataset

English                French

I love India      →    J'aime l'Inde
```

↓

```
Tokenization
```

↓

```
Vocabulary Creation
```

↓

```
Integer Encoding
```

↓

```
Padding
```

↓

```
Create

Encoder Input

Decoder Input

Decoder Target
```

↓

```
Embedding Layer
```

↓

```
Encoder
```

↓

```
Hidden State

Cell State
```

↓

```
Decoder
```

↓

```
Dense Layer
```

↓

```
Softmax
```

↓

```
Prediction
```

↓

```
Loss Calculation
```

↓

```
Backpropagation
```

↓

```
Update Encoder Weights

Update Decoder Weights
```

---

## 6.2 Forward Propagation

During forward propagation,

the English sentence is given to the encoder.

Example

```
Input

I love India
```

The encoder processes one token at a time and produces

```
state_h

state_c
```

These states initialize the decoder.

The decoder starts with

```
<SOS>
```

and predicts one target word at a time.

---

## 6.3 Loss Calculation

Suppose the decoder predicts

```
Prediction

Bonjour
```

but the correct word is

```
J'aime
```

The prediction is compared with the correct target word.

The difference between the predicted probability and the correct word is called the **Loss**.

A smaller loss means better predictions.

---

## 6.4 Backpropagation

The calculated loss is propagated backward through the entire Seq2Seq model.

The gradients update:

- Encoder Embedding
- Encoder LSTM
- Decoder Embedding
- Decoder LSTM
- Dense Layer

As training continues, the model gradually learns better translations.

---

## 6.5 What Does Each Component Learn?

### Encoder

Learns to understand the source sentence.

---

### Decoder

Learns to generate the target language.

---

### Embedding Layer

Learns meaningful vector representations of words.

---

### Dense Layer

Learns how to convert decoder outputs into vocabulary probabilities.

---

## 6.6 Training Workflow

```
English Sentence

↓

Encoder

↓

state_h
state_c

↓

Decoder

↓

Prediction

↓

Compare with

Correct Word

↓

Loss

↓

Backpropagation

↓

Weight Update

↓

Next Epoch
```

This process repeats for every sentence in the training dataset across multiple epochs.

---

## Interview Points

### Which layers learn during training?

All trainable layers learn:

- Embedding Layer
- Encoder LSTM
- Decoder LSTM
- Dense Layer

---

### Does the encoder learn separately?

No.

The encoder and decoder are trained together as one end-to-end model.

---

### What is updated during backpropagation?

The weights of every trainable layer are updated to reduce the prediction error.

---

## Key Takeaways

✔ Encoder and Decoder are trained together.

✔ Loss is calculated using the decoder prediction and the correct target word.

✔ Backpropagation updates the entire network.

✔ Training repeats for every sentence and every epoch until the model learns accurate translations.
