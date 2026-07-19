# Comparison Study: Custom LSTM vs Transformer for Time-Series Forecasting

## Prediction Quality

Both the Custom LSTM and Transformer models successfully learned temporal patterns from the hourly Jena Climate dataset. The LSTM demonstrated stable convergence throughout training and achieved good predictive performance by learning sequential dependencies. The Transformer also produced accurate forecasts and effectively captured the overall temperature trend using self-attention. While both models performed well, the Transformer showed greater capability in modeling global relationships within the sequence, whereas the LSTM relied on sequential memory to make predictions.

---

## Long-Range Dependency Handling

### Custom LSTM
The LSTM processes input sequences one time step at a time while maintaining hidden and cell states. The forget, input, and output gates help preserve important historical information, reducing the vanishing gradient problem. However, information from very early time steps may gradually weaken when processing long sequences.

### Transformer
The Transformer uses self-attention, allowing every input time step to directly interact with every other time step in the sequence. This enables efficient learning of long-range dependencies without relying on recurrent memory, making it particularly suitable for long-sequence forecasting tasks.

---

## Runtime

### Custom LSTM
- Sequential computation prevents parallel processing.
- Training time increases with sequence length.
- Generally slower for long input sequences.

### Transformer
- Processes the entire sequence simultaneously.
- Efficient GPU utilization through parallel computation.
- Faster training on modern hardware despite increased computational complexity.

---

## Memory Usage

### Custom LSTM
- Lower memory consumption.
- Suitable for systems with limited computational resources.
- Memory usage grows approximately linearly with sequence length.

### Transformer
- Higher memory consumption due to self-attention.
- Every time step attends to every other time step.
- Memory requirements increase rapidly as sequence length grows.

---

## Training Stability

### Custom LSTM
The training and validation losses decreased steadily throughout training, indicating stable optimization and good generalization. The small gap between training and validation losses suggests limited overfitting.

### Transformer
The Transformer converged rapidly during the initial epochs. However, after achieving the best validation performance, the validation loss gradually increased while the training loss continued to decrease, indicating mild overfitting. Early stopping or stronger regularization can improve generalization.

---

# Strengths and Limitations

## Custom LSTM

### Strengths
- Effective at modeling sequential data.
- Stable and consistent training.
- Lower memory requirements.
- Suitable for smaller datasets.
- Simpler architecture.

### Limitations
- Sequential computation limits parallelism.
- Long-range information may gradually fade.
- Slower training for long sequences.

---

## Transformer

### Strengths
- Excellent at capturing long-range dependencies.
- Fully parallelizable during training.
- Learns global relationships effectively using self-attention.
- Highly scalable for large datasets.

### Limitations
- Higher computational complexity.
- Greater memory requirements.
- Requires positional encoding.
- More sensitive to hyperparameter selection.

---

# Discussion

## Why Attention Helps Sequence Modeling

Self-attention enables the Transformer to compute relationships between all positions in an input sequence simultaneously. Rather than relying solely on previously processed information, the model can directly focus on the most relevant time steps when generating predictions. This improves its ability to capture long-range temporal dependencies and complex interactions within sequential data.

---

## Differences Between Recurrence and Attention

| Recurrent Networks (LSTM) | Attention-Based Networks (Transformer) |
|----------------------------|-----------------------------------------|
| Process one time step at a time | Process the entire sequence simultaneously |
| Store information in hidden and cell states | Learn relationships using attention weights |
| Sequential computation | Parallel computation |
| Long-range information may gradually weaken | Direct access to all positions regardless of distance |

---

## Situations Where LSTMs Are Still Useful

LSTMs remain a strong choice when:
- The dataset is relatively small.
- Computational resources are limited.
- Low memory usage is important.
- The sequence length is short or moderate.
- A lightweight model is preferred.

---

## Situations Where Transformers Perform Better

Transformers are generally preferred when:
- Modeling long sequences.
- Large-scale datasets are available.
- Parallel GPU training is possible.
- Long-range temporal dependencies are important.
- High forecasting accuracy is required for complex sequential data.

---

# Conclusion

Both the Custom LSTM and Transformer models successfully forecasted future temperatures using the hourly Jena Climate dataset. The LSTM provided stable learning, lower memory consumption, and a simpler architecture, making it suitable for resource-constrained applications. The Transformer leveraged self-attention to capture long-range dependencies more effectively and benefited from parallel computation, making it more suitable for large-scale and complex time-series forecasting tasks. Overall, the Transformer offers greater scalability and modeling capacity, while the LSTM remains an efficient and reliable solution for moderate-sized forecasting problems.
