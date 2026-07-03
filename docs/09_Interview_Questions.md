# Chapter 9: Interview Questions & FAQs

This chapter contains the most frequently asked interview questions related to Machine Translation using Seq2Seq LSTM and the Attention Mechanism.

---

## Encoder

### Q1. What is the role of the Encoder?

The encoder reads the complete source sentence one token at a time and converts it into a contextual representation using hidden states and cell states.

---

### Q2. Does the Encoder perform translation?

No.

The encoder only understands the source sentence.

The decoder generates the translated sentence.

---

### Q3. What does the Encoder learn?

- Context
- Grammar
- Word relationships
- Long-term dependencies

---

### Q4. What are the outputs of the Encoder?

- Hidden States
- Final Hidden State
- Final Cell State

---

### Q5. Why are Hidden States required?

They represent the contextual information learned after processing each input token.

In Attention-based models, all hidden states are used.

---

## Decoder

### Q6. What is the role of the Decoder?

The decoder generates the translated sentence one word at a time.

---

### Q7. Why does the Decoder need the Encoder states?

The decoder must know the meaning of the source sentence before generating the target sentence.

The encoder's final hidden state and cell state initialize the decoder.

---

### Q8. Does the Decoder know French before training?

No.

Initially, its weights are randomly initialized.

It learns the target language during training through backpropagation.

---

### Q9. Why does the Decoder generate one word at a time?

Because language is sequential.

Each predicted word depends on the previous words.

---

### Q10. What is the purpose of the Dense layer?

The Dense layer converts the decoder hidden state into scores for every word in the target vocabulary.

---

### Q11. Why is Softmax used?

Softmax converts the scores into probabilities.

The word with the highest probability becomes the prediction.

---

## Teacher Forcing

### Q12. What is Teacher Forcing?

Teacher Forcing is a training technique where the decoder receives the correct previous target word instead of its own prediction.

---

### Q13. Why is Teacher Forcing required?

It prevents error accumulation and speeds up learning.

---

### Q14. Is Teacher Forcing used during inference?

No.

During inference, the decoder uses its own predictions.

---

### Q15. Why do we create Decoder Input and Decoder Target?

The decoder input teaches the model what to read.

The decoder target tells the model what it should predict.

---

## Attention

### Q16. Why is Attention required?

The final hidden state alone may not contain enough information for long sentences.

Attention allows the decoder to access all encoder hidden states.

---

### Q17. Why are only Hidden States used in Attention?

Hidden states contain contextual information.

Cell states are internal LSTM memory and are not used by the Attention mechanism.

---

### Q18. What is a Context Vector?

The Context Vector is a weighted combination of all encoder hidden states based on attention scores.

---

### Q19. Does Attention replace the Encoder?

No.

Attention works together with the encoder.

The encoder still processes the input sentence.

---

## Training

### Q20. What learns during training?

- Encoder Embedding
- Encoder LSTM
- Decoder Embedding
- Decoder LSTM
- Dense Layer

---

### Q21. What is Backpropagation?

Backpropagation calculates gradients from the loss and updates all trainable weights.

---

### Q22. How are the Encoder and Decoder trained?

They are trained together as a single end-to-end model.

---

## Inference

### Q23. What happens during inference?

The encoder processes the source sentence once.

The decoder generates one target word at a time until it predicts `<EOS>`.

---

### Q24. When does the Decoder stop generating words?

When it predicts the `<EOS>` token or reaches the maximum sequence length.

---

### Q25. Difference between Training and Inference?

| Training | Inference |
|----------|-----------|
| Uses Teacher Forcing | Uses previous prediction |
| Target sentence available | Target sentence unavailable |
| Calculates Loss | No Loss Calculation |
| Updates Weights | No Weight Updates |

---

## Key Interview Takeaways

✔ Encoder understands the source sentence.

✔ Decoder generates the target sentence.

✔ Teacher Forcing is used only during training.

✔ Attention allows the decoder to access all encoder hidden states.

✔ During inference, the decoder depends on its own previous predictions.

✔ Encoder and Decoder are trained together using backpropagation.

✔ Translation ends when `<EOS>` is generated.

---
