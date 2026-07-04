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

# Key Idea

The Bahdanau Attention Network learns **where to look**.

It does **not** translate the sentence.

It learns which encoder hidden states are most important for generating the current target word.

This ability allows the decoder to dynamically focus on different parts of the input sentence during translation.
