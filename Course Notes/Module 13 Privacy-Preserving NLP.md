# Module 13: Privacy-Preserving NLP

# Differential Privacy

## What is it?

- The intuition behind differential privacy is that “***we limit how much the output can change if we change the data of a single individual in the database***”

## Definition

- Differential privacy (DP) ensures that adversaries cannot **identify an individual** within a protected dataset by comparing it with other datasets
- It achieves this by making **small, arbitrary changes to individual data** without altering the overall statistics of interest
- Let's first define privacy in the context of differential privacy:
    - Suppose we have a dataset $D_1$ that is input to an algo $M_1$ and results in $R_1$
    - Pluck some random datapoint from $D_1$, and remove it
    - Now we have $D_2 = D_2 - {x}$ and we will pass this into our Algo $M_1$ to get $R_2$
    - Now we compare $R_1$ and $R_2$
    - If they are similar then we may say that the privacy of $x$ is preserved
- What do we mean by similar?
    - It means that the output doesn't meaningfully change irrespective of whether your data was looked at or not
- This is the mathematical formulation
    - $∀ \space \text{adjacent}(D_1,D_2); ∀ \space x,Pr(M(D_1)=x) \leq e^ϵ \space Pr(M(D_2)=x)$
        - Represents the ratio between the two probability distributions is smaller than some epsilon
        - This mechanism is called Epsilon **Differentially Private**
    - Note that privacy comes from the mechanism not the dataset, since we haven't changed the dataset at all

## How does it work in practice?

- Add some noise to gradients

```python
for epoch in range(epochs):
    for x,y in dataloader(train,batch=20):
        y_hat = model(x)
        loss = criterion(y_hat,y)
        loss.backwards()

        gradients = (p.grad for p in model.parameters())

        # add some noise to implement a DP mechanism
        for p in model.parameters():
            p.grad += torch.normal(mean=0.0,std=args.sigma,size=p.grad.shape)

            optimizer.step()
            optimizer.zero_grad()
```