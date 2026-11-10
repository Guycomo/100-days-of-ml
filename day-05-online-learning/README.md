# Day 05: Online Learning

## 1. Where this fits?

ML was first classified by the amount of supervision (supervised, unsupervised, semi-supervised, reinforcement). Then the discussion moved to a second basis: **how an ML model behaves in production.** That gives two categories:

1. **Batch learning** (previous video)
2. **Online learning** (this video)

---

## 2. What is online learning?

Many companies promote their product by saying: *"the more you use our product, the better its performance gets."* If you've heard a company say this, it means they're using online learning. Their ML model on the server keeps improving on the go by training on new data.

**Definition:** unlike batch learning, online learning is done **incrementally.**

- You feed data to the model in **small chunks (mini-batches), sequentially, one after another.**
- After each chunk, the model improves and keeps learning.
- Each chunk is small, so the training can be done **on the server, in production**, while the model is live. That's why it's called "online."

### Process flow

1. Start with some data and train the ML algorithm.
2. Test it to check that it works properly.
3. Put it on the server.
4. On the server, new data keeps coming in continuously. The model does **two things**: it predicts on the new data, and it also **trains on the new data.**

**The difference from batch learning:** in batch learning, once a model is trained and in production, retraining means taking it back, retraining it and deploying it again. In online learning, you train the model on the server itself, so as new data comes in, its performance keeps improving accordingly.

---

## 3. Examples

- **Chatbots / assistants** from famous companies (the video mentions Google Now and Siri, among others). They're deployed, predict on new data, and keep improving.
- **SwiftKey keyboard** on Android phones. As you type, its performance improves dynamically. The speaker says he noticed this himself and believes it uses online learning (he mentions reading about the company on its official blog).
- **YouTube.** When you click on a video and come back to the feed, the recommendations below change automatically based on what you just watched. YouTube knows that's what's on your mind, so it assumes you want related content. The data generated from your click is used to update the model and recommend new things.

Many companies still use batch learning, but the industry is moving towards online learning.

---

## 4. When should you use online learning?

**1. When the nature of the problem changes over time**

Sometimes the problem you're solving with ML keeps changing. E-commerce platforms are an example: customer behaviour and profiles keep changing. In situations where the concept itself keeps shifting, you should use online learning.

**2. To save cost**

If you work with a very large dataset, batch learning costs you a lot (compute and time). With online learning you work with small chunks, so the cost is much lower. Training is fast, so if you want your overall system to be fast, this is the solution.

The speaker says he'll share a research paper that explains how online learning is cost-effective compared to batch learning.

---

## 5. How to implement online learning

### 5.1 scikit-learn: `partial_fit`

The simple way is to use the scikit-learn module. Some of its algorithms let you train on data sequentially, in increments. Normally you use `fit`, but these algorithms also have a **`partial_fit`** method. An example is the SGD regressor, a linear model.

Demo in the video:

1. Train an SGD regressor on a very small dataset of a few data points. Training took almost no time.
2. Generate some more data, call `partial_fit`, and training **continues from the same point** where it left off.
3. You can keep repeating this whenever new training data shows up.

### 5.2 Dedicated libraries

- **River** is a very famous Python library for online machine learning. The video says it came from merging two earlier libraries. (The speaker is working on it and plans to do a project on it later.)
- **Vowpal Wabbit** is another famous one. It's also useful for reinforcement learning, and it has an option for online machine learning.

---

## 6. Learning rate

An important concept in online learning. The learning rate decides **how fast your model adapts to the new data.** Data comes in consistently, but how aggressively should the model update itself?

| Learning rate | What happens |
|---|---|
| **Too high** | The model changes very fast and **forgets old things**, learning only the new stuff |
| **Too low** | The model learns/adapts too slowly |

You have to set a rate so that the model **remembers old things and also learns new things.** Setting the right learning rate for your business is the most important part of online learning. If you get it wrong, the model may misbehave or not work properly. The speaker says this will come up again in later projects.

---

## 7. Out-of-core learning

Slightly different from the above, but related.

**Situation:** your dataset is so large that you can't train on it in one go on your machine. It's a technical limitation. Example: you have a 50 GB dataset and only 8 GB of RAM, so you can't load it. How do you train?

**What you do:** use the incremental learning concept.

1. Split the large dataset into small chunks.
2. Send the chunks to your model one by one, sequentially.
3. When done, take the trained model and put it on the server. After that you can update it either with batch learning or online learning, whichever you choose.

So using the online learning technique, you can process very large datasets. All of this work is done **offline**; only the technique being used is that of online learning. (The speaker admits there's some confusion in the naming here.)

---

## 8. Disadvantages of online learning

Everything sounds great, but there are big problems.

**1. It's hard to do and manage**

- Training a model isn't the hard part. Making it work properly **live on the server** is. The challenges are the learning rate, and handling the speed at which data arrives.
- When data is coming in real time, getting such a system to work perfectly is difficult.
- There aren't very reliable tools. The existing libraries were built by individuals working together, so you don't get **enterprise-grade assurance.** It's a newer approach and a bit unstable.

**2. It's risky**

You put the model on the server and its behaviour changes based on new data. Now imagine the data goes bad: a server gets hacked, or wrong or malicious requests keep coming in and you capture them all. Your model becomes **biased towards the wrong things**, and you'd have to take it off the server immediately. This is a big risk, because your model depends on the incoming data and you don't control that data.

**Solutions:**

- Build an **active monitoring system** that watches the whole system all the time.
- Use an **anomaly detection algorithm** that, as soon as it sees abnormal behaviour, takes the system offline or rejects that data.
- Always have a **second option** to roll back immediately: take the system down and put an **earlier version** of the model back online.

You need to know all these techniques and be careful with them.

---

## 9. Batch vs online learning

| | Batch (offline) learning | Online learning |
|---|---|---|
| **Complexity** | Simple: train on your machine, put it on the server, predict | More complex: continuous monitoring is needed on the server |
| **Computational power** | Heavy compute each time you retrain on the full data on your machine | Lighter, since you train on small chunks and don't retrain from scratch |
| **Ease of implementation** | Easier | Harder |
| **Best suited for** | Applications where the data and concept don't change over time. Example: classifying dogs and cats, since a dog will still be a dog 10 years later | Applications where data keeps changing |
| **Tools** | More mature tools in industry | Fewer, newer tools |

---

## 10. Why this matters

Beginners usually only focus on their model reaching, say, 90% accuracy and think the work is done. But when you work in industry as a professional, you have to think about more:

- If I put this on a server, how much will it cost?
- If the data changes on the server, how will my model react?

That's why these two videos on batch and online learning matter.
