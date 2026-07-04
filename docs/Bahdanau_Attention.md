# Understanding the Bahdanau Attention Neural Network

Before implementing Bahdanau Attention, it is important to understand **what kind of neural network it is** and **what it actually learns**.

---

## Is Bahdanau Attention an RNN?

**No.**

Bahdanau Attention is **not** an RNN because it has no recurrence and does not maintain hidden states across time steps.

---

## Is Bahdanau Attention an LSTM?

**No.**

It does not contain:

- Forget Gate
- Input Gate
- Output Gate
- Cell State

Therefore, it is not an LSTM.

---

## Then what is it?

Bahdanau Attention is a **small Feed Forward Neural Network (Artificial Neural Network - ANN)**.

It consists of **three Dense layers**.

```
Encoder Outputs ------► Dense (W1)
                             │
                             ▼
                     Learned Representation

Decoder Hidden State ► Dense (W2)
                             │
                             ▼
                     Learned Representation

               Add
                │
             tanh()
                │
             Dense(V)
                │
        Attention Scores
                │
            Softmax
                │
      Attention Weights
                │
        Weighted Sum
                │
          Context Vector
```

---

# Why do we use an ANN?

The decoder needs to answer one question before predicting every English word.

> **Which encoder hidden state is most relevant right now?**

Instead of manually designing this logic, Bahdanau proposed learning it using a small neural network.

The ANN learns how to compare:

- Current Decoder Hidden State
- Every Encoder Hidden State

and produces an **Attention Score** for each encoder hidden state.

---

# What does this ANN actually learn?

The Attention ANN does **not** learn Telugu.

It does **not** learn English.

It learns an **alignment function**.

Its job is to answer:

> **"How important is this encoder hidden state for predicting the current target word?"**

For every decoder time step, it learns attention scores such as:

```
Encoder Hidden State      Attention Score

h1 -----------------------> 0.92

h2 -----------------------> 0.05

h3 -----------------------> 0.03
```

Higher score means **more relevant**.

During training, backpropagation updates the ANN weights so that it learns to focus on the correct encoder hidden states.

---

# How is this similar to a normal ANN?

Exactly like a normal Dense Neural Network:

**We decide**

- Number of Dense layers
- Number of neurons in each layer

The network learns

- Layer weights
- Layer biases
- What each neuron represents

using Forward Propagation and Backpropagation.

Just like any ANN, we never manually define what each neuron should learn.

---

# How are the neurons decided?

The first two Dense layers are usually created with the same number of neurons as the LSTM hidden size.

Example:

```
LSTM Hidden Units = 256

↓

Dense(W1) = 256 neurons

Dense(W2) = 256 neurons
```

This allows the encoder hidden states and decoder hidden state to be projected into the same feature space before comparison.

This is a design choice (hyperparameter), not a mathematical requirement.

---

# Why only three Dense layers?

Each Dense layer has a different responsibility.

### Dense Layer W1

Processes the Encoder Hidden States.

```
Encoder Outputs

↓

Dense(W1)
```

---

### Dense Layer W2

Processes the Current Decoder Hidden State.

```
Decoder Hidden State

↓

Dense(W2)
```

---

### Dense Layer V

Produces a **single Attention Score** for every encoder hidden state.

```
Dense(V)

↓

One Attention Score
```

This score is later converted into an Attention Weight using Softmax.

---

# Working Process

```
Step 1

Encoder produces

h1 h2 h3 ... hT

↓

Step 2

Decoder produces current hidden state

d_t

↓

Step 3

Attention ANN compares

d_t

with

h1 h2 h3 ... hT

↓

Step 4

ANN computes Attention Scores

↓

Step 5

Softmax converts scores into Attention Weights

↓

Step 6

Weighted sum of encoder outputs creates the Context Vector

↓

Step 7

Context Vector is passed to the Decoder

↓

Step 8

Decoder predicts the next English word
```

---
# Example: What Does the Attention ANN Learn?

Consider the Telugu sentence:

```
నేను భారతదేశాన్ని ప్రేమిస్తున్నాను
```

The Encoder processes the sentence and produces three hidden states.

```
నేను ------------------> h1

భారతదేశాన్ని -----------> h2

ప్రేమిస్తున్నాను ---------> h3
```

The Decoder now starts generating the English translation one word at a time.

---

## Decoder wants to predict the first word

The current decoder hidden state is

```
d1
```

The Attention ANN receives two inputs:

```
Encoder Hidden States

h1
h2
h3

AND

Current Decoder Hidden State

d1
```

Initially, the Attention ANN has random weights.

It may produce the following Attention Scores.

```
h1 -----------> 0.30

h2 -----------> 0.20

h3 -----------> 0.50
```

After applying Softmax,

```
Attention Weights

h1 -----------> 0.30

h2 -----------> 0.25

h3 -----------> 0.45
```

The Context Vector is created using these weights.

The Decoder predicts

```
India
```

However, the correct first English word is

```
I
```

The prediction is incorrect.

---

## Backpropagation

The loss is calculated.

The gradients flow backward through

```
Decoder

↓

Attention ANN

↓

Encoder
```

The Attention ANN updates its weights.

It gradually learns:

> "For predicting the first English word, I should focus more on **h1** instead of **h3**."

---

## After Training

The same sentence now produces

```
Attention Scores

h1 -----------> 8.5

h2 -----------> 2.1

h3 -----------> 0.4
```

Softmax converts them into

```
Attention Weights

h1 -----------> 0.95

h2 -----------> 0.04

h3 -----------> 0.01
```

The Context Vector is now dominated by **h1**.

The Decoder correctly predicts

```
I
```

---

## Decoder predicts the second word

The Decoder hidden state changes.

```
d2
```

Again, the Attention ANN compares

```
d2

with

h1
h2
h3
```

This time it learns

```
h3 -----------> Highest Attention
```

because

```
ప్రేమిస్తున్నాను

↓

love
```

The Decoder predicts

```
love
```

---

## Decoder predicts the third word

The Decoder hidden state becomes

```
d3
```

Again, Attention computes new scores.

Now it learns

```
h2 -----------> Highest Attention
```

because

```
భారతదేశాన్ని

↓

India
```

The Decoder predicts

```
India
```

---

# Final Translation

```
నేను భారతదేశాన్ని ప్రేమిస్తున్నాను

↓

I love India
```

---

# Key Learning

Notice that the Attention ANN computes **new Attention Scores for every decoder time step.**

It continuously learns:

> **"Which encoder hidden state should I focus on for predicting the current target word?"**

This is why Attention is often described as **"learning where to look."**

# Key Idea

The Bahdanau Attention Network learns **where to look**.

It does **not** translate the sentence.

It learns which encoder hidden states are most important for generating the current target word.

This ability allows the decoder to dynamically focus on different parts of the input sentence during translation.
