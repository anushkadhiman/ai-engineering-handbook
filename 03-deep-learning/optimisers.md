## AdamW (Adam with Weight Decay)

AdamW (Adam with Weight Decay) is a modified version of the popular Adam optimizer, widely considered the de facto standard for training modern deep learning models like Transformers and Large Language Models (LLMs).

**The Core Difference: Decoupled Weight Decay**
While standard Adam combines L2 regularization directly with the gradient update, AdamW decouples them.
**Adam + L2:** Regularization is added to the gradient before the adaptive learning rate is applied. This means weights with large gradients get regularized less, and those with small gradients get regularized more, which weakens the regularization effect.
**AdamW:** Weight decay is applied directly to the weights after the adaptive update step. This ensures regularization remains consistent regardless of the gradient magnitude.

**Why Use AdamW?**

- **Superior Generalization:** By fixing the weight decay logic, AdamW typically achieves better validation performance and prevents overfitting more effectively than standard Adam.
- **Easier Hyperparameter Tuning:** Since weight decay is decoupled, you can tune the learning rate and weight decay coefficient more independently.
- **Stability for Large Models:** It is particularly robust for training complex architectures where parameters have vastly different gradient scales, such as in Vision Transformers or GPT models.

**How it Works (5-Step Algorithm)**
Compute Gradient: Calculate the unregularized loss gradient.

- **Update First Moment:** Track the moving average of gradients (momentum).
- **Update Second Moment:** Track the moving average of squared gradients (adaptive learning rate).
- **Bias Correction:** Adjust moments to account for their zero-initialization.
- **Decoupled Update:** Subtract the adaptive gradient step and the direct weight decay term from the current weight.

---

## Decoupled Weight Decay

Decoupled Weight Decay is a regularization technique that separates the process of shrinking model weights from the process of updating them based on loss gradients.
While traditional optimizers often lump these two together, decoupling them ensures that the "penalty" for having large weights remains consistent and predictable, regardless of how fast the model is learning.

**1. How It Differs from L2 Regularization**
In many textbooks, "L2 Regularization" and "Weight Decay" are used interchangeably, but in modern deep learning, they are implemented differently:

**L2 Regularization (Coupled):** You add a penalty term to the loss function. This modifies the gradient before it enters the optimizer. If you are using an adaptive optimizer like Adam, this regularization gradient gets scaled and "dampened" by the adaptive learning rate, meaning weights with large gradients get less regularization than they should.
**Decoupled Weight Decay:** You ignore the loss function for a moment and simply subtract a small fraction of the weight directly during the update step. This ensures the decay happens at a constant rate, independent of the gradients or adaptive moments.

**2. Why "Decoupling" Matters**

- **Consistent Regularization:** In models with varied gradient scales (like Transformers), decoupling ensures every parameter is regularized equally.
- **Easier Tuning:** Because weight decay and learning rate are separated, you can change your learning rate without unintentionally making your regularization stronger or weaker.
- **Better Generalization:** Research shows that decoupling allows adaptive optimizers (like AdamW) to perform as well as, or better than, standard SGD on complex tasks like image classification and language modeling.
