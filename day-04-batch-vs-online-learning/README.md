# Day 04: Batch vs Online Learning

## 1. What this video is about

In the last video, ML was classified based on the **amount of supervision** (supervised, unsupervised, semi-supervised, reinforcement). Today is the same topic, types of ML, but on a **completely different basis**: **how the ML model is trained.**

This leads to two types:

1. **Batch learning** (also called offline learning)
2. **Online learning** (also called incremental learning)

This matters because in the real world you don't just build an ML model on your computer. You upload it to a server, and you need to know how batch and online learning differ.

---

## 2. First, what is "production"?

In simple terms, production means your code is going to run for real users.

- When you build software, it sits on your machine. To reach your customers it has to run on a **server**, which has an IP address your customers can reach to get answers to their requests.
- An ML model is the same. You deploy it to a server.
- The environment where your code runs for customers is called **production.**
- Your own machine, where you build and train, is the **development environment.**

ML software behaves and runs differently on a server compared to your machine, and that's the basis for the two types below.

---

## 3. Batch learning

**Batch learning** is the conventional way of training a model. You use the **entire data at once** to train the ML model.

The opposite is **incremental training**, where you train in small chunks.

### How it's usually done

- The data in real problems is generally very large. Loading it all and training on a server would be **costly and time-consuming.**
- So batch learning is generally done **offline**, on your own machine: a data scientist or ML engineer trains the model there.
- Once the model is trained, you take the learned model and put it on the server (production). This is why batch learning is also called **offline learning.**

### The flow

1. You have the data.
2. Train the model on your machine (offline).
3. Test it to check your claims are correct.
4. Put the model on the server.
5. The model keeps running, and whenever a user gives data, it gives an output.

**Example:** you want to build a movie recommendation engine for Netflix that suggests movies to users. You train the recommendation engine on your machine, put it on the server, and your system keeps suggesting movies automatically.

---

## 4. The problem with batch learning

The model is **static.** Once it has learned, it keeps working on old things.

But the business scenario keeps evolving.

- **Recommendation example:** you built the engine today using all the movies available today. Every week new movies come in. For the model to recommend new movies, it has to learn about them.
- **Spam example:** your email spam classifier is up to date today. But if you leave it for a year, spammers will have found new techniques. The model has had no training since, so it becomes useless.

**So the biggest problem with batch learning: you have to keep retraining your model.**

### The retraining cycle

1. New data keeps coming in, and the data keeps updating.
2. Combine the **new data and the old data**.
3. Train the model again.
4. Test it again.
5. Put it on the server again.

This is a **cycle** that repeats over a given period. How often depends on how fast things change and on the amount of data, since a large dataset takes time to train on. The video says people commonly do it weekly or every 24 hours.

---

## 5. Disadvantages of batch learning

**1. Large amounts of data**

- Data keeps growing over time, so each retraining has to deal with more and more of it.
- The data can become so large that your tools can't process it. You can't load the whole data in one go to train, because you're forced to use the **full data** every time.
- It's a hardware limitation. Computing power and memory are limited.

**2. No connectivity (hardware / deployment limitation)**

Sometimes your ML model runs in a place where you don't have instant connectivity. You can't just bring the model back, train it on new data and upload it again.

- **Example:** an app used in an extreme location like Ladakh, where there's no internet. The model is running on the phone, and until people return to a place with connectivity, you can't pull it back, retrain it and update it.
- **Similar example:** ML software sent on a satellite, or something running on a device in a train, where there's no internet connection or you don't know where it is.

In places like these you can't take frequent updates, so batch learning fails.

**3. Even frequent retraining can be too slow**

Say you work on a social networking site, and you built a model that decides which friends' stories to show you, based on your interests. It updates every 24 hours on new data.

- Suddenly a piece of news spreads on your network. The example in the video is news about demonetisation in India. Everyone becomes interested in it, including someone who normally only follows sports.
- But the system only updates your interests **after 24 hours.** By the time it does, the news is old and no longer important.
- The recommendation system can't respond to something that just happened.

For this kind of requirement, batch learning isn't helpful.

---

## 6. Online learning

Because of these problems, a **different approach** is used: **online learning**, also called **incremental learning.**

Instead of training on the full data again and again, the model learns in small chunks as new data comes.
