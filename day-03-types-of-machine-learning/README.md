# Day 03: Types of Machine Learning

## 1. How ML is classified?

Types of machine learning depend on different bases, and the video says there are three of them. Today's video covers only one: **how much supervision is needed to train an ML algorithm.**

Based on the amount of external supervision, ML algorithms fall into four categories:

1. Supervised machine learning
2. Unsupervised machine learning
3. Semi-supervised machine learning
4. Reinforcement learning

This is the most popular classification, and most videos and books use it. The other two bases will be covered in the next two days.

```mermaid
flowchart TB
    ML[Machine Learning] --> S[Supervised]
    ML --> U[Unsupervised]
    ML --> SS[Semi-supervised]
    ML --> R[Reinforcement learning]
    S --> S1[Regression]
    S --> S2[Classification]
    U --> U1[Clustering]
    U --> U2[Dimensionality reduction]
    U --> U3[Anomaly detection]
    U --> U4[Association rule learning]
```

---

## 2. Supervised machine learning

ML is learning from data. If your data has **both inputs and outputs**, and your job is to find the relationship between them so that you can predict the output for a new input, that is **supervised machine learning.**

### Example

Data of 5000 students with three columns: IQ, CGPA, and whether they got placed.

| IQ | CGPA | Placement |
|---|---|---|
| 87 | 7.1 | Yes |
| 111 | 8.9 | Yes |
| 75 | 6.3 | No |
| ... | ... | ... |

- **Input columns:** IQ and CGPA.
- **Output column:** placement (yes or no). It depends on the other two columns.
- The algorithm builds a mathematical relationship between input and output. Later, if you give it a new student (say CGPA 7.3 and IQ 73), it can say whether placement will happen, yes or no.

The video says that as you do more ML in the future, you'll mostly be working on supervised ML.

### Types of data (needed to understand the two sub-types)

| Type | Examples |
|---|---|
| **Numerical** | Age, weight, CGPA, IQ |
| **Categorical** | Gender, nationality, brand of phone you use |

### Regression

A supervised problem where the **output (target) column is numerical.**

Example: input is IQ and CGPA, output is the **package** (in lakhs) received after college, like 4.5, 3.0, 3.5, 6. Still supervised, but the type is regression because the target is numerical.

### Classification

A supervised problem where the **output column is categorical.**

Example: the first example above, placement yes or no.

### More examples

| Problem | Type |
|---|---|
| Predict a house's price from all its data | Regression |
| Predict whether an email is spam or not | Classification |
| Predict whether it will rain today from weather conditions | Classification |
| Look at a picture and say whether it has a dog | Classification |
| Look at different pictures and say how many dogs are in each | Regression |

### How to decide

1. Do you have both input and output? If yes, it's **supervised**.
2. Look at the output column. A number means **regression**, a category means **classification**.

That's the whole idea.

---

## 3. Unsupervised machine learning

The exact opposite of supervised. In supervised you have input and output. In unsupervised, **you only have inputs.**

Example: the same 5000 students, but only IQ and CGPA columns, no placement data.

Since there is only input and no output, there can be no prediction task, because you don't know what you're supposed to predict. So what do you do? Mainly four kinds of tasks:

1. Clustering
2. Dimensionality reduction
3. Anomaly detection
4. Association rule learning

The video says you'll end up working with unsupervised ML a lot too.

### 3.1 Clustering

Plot the student data on a 2D graph with IQ on the x-axis and CGPA on the y-axis. A clustering algorithm identifies which students should be in a group together. Say it finds three groups:

- High IQ and high CGPA
- High IQ and low CGPA
- High CGPA and low IQ

**What you get from this:**

- You can divide students into categories, and any new student can be put into a category and processed accordingly.
- You can label the groups yourself (0 means both high, 1 means high CGPA and low IQ, 2 means high IQ and low CGPA), and that way **create labelled data for supervised ML.**
- It helps your own analysis. For example, if you run an e-commerce website, you want to know what types of customers you have, how they behave, and which categories they fall into.

**Why clustering is powerful:** with two columns you can see the clusters by eye. A clustering algorithm can split data into clusters even in an n-dimensional hyperspace, very high-dimensional data that you can't look at yourself. It's widely used in industry.

**Hierarchical clustering** makes groups inside groups, so you can see everything group by group.

### 3.2 Dimensionality reduction

**Dimension means column** (an input column). Dimensionality reduction reduces the number of input columns.

**Why it's needed:** sometimes you have a huge number of input columns, for example 1000 columns when working with image or text data. Two problems:

1. The algorithm runs very slowly because it has to work on so much data.
2. After a certain point, adding more input columns gives no improvement in results. Some columns aren't needed.

**Example:** a house dataset with columns for the number of rooms and the number of washrooms, and you have to predict the house price. A dimensionality reduction algorithm takes related columns like these and converts them into one column, **square feet area.** Rooms and washrooms together make up the house, so the area is what's really increasing.

Creating one new column from the given columns is called **feature extraction.** Since the number of columns dropped, it's dimensionality reduction. A well-known algorithm for this is **PCA.**

**Visualization** is a related use. A graph can show at most three axes. If your data has 500, 1000 or 2000 columns, you can't plot it. You use a dimensionality reduction algorithm to bring it down to two or three dimensions, then plot the points there, while still capturing the relationships.

**Example: MNIST.** A famous dataset of handwritten digit images, each 28 by 28 pixels. It's converted into table form with each pixel value as a column, so 28 x 28 = **784 columns**, meaning the data sits in a 784-dimensional space. You can't visualise that. A technique called **t-SNE** (a dimensionality reduction technique) brings it down to three dimensions, and you can still see the relationship between points. In the blog shown, 10 colours represent the 10 digits (yellow for 1, blue for 6, red for 0, green for 4), and similar digits group together.

(The video says this is a more advanced topic, shown only to prove it exists in practice.)

### 3.3 Anomaly detection

Detecting something unusual or abnormal. It could be a defect in manufacturing, a problem during credit card processing, or a problem during loan approval. You identify the **outliers** and remove them from the system.

**Example:** you train your model on a set of points and tell it these normal points are fine. A new point that lands among them is okay, since it looks like the rest. If a point is far away and different from the others, you raise a flag that it's an anomaly.

It also works for things like share prices: if they were moving within a range and suddenly go well above it, the anomaly is flagged.

### 3.4 Association rule learning

**Example:** a supermarket (Spencer's or Big Bazaar, in the video) has around 5000 to 6000 products. How do you decide what goes next to what? That's a hard problem.

What you do:

1. Collect all shopping bills from the last one or two years.
2. Look for patterns. Say out of 100 bills, milk was bought in 80, and in 60 of those eggs were bought too.
3. That shows a strong association between milk and eggs, so you place them next to each other.

You collect information from data, do data mining, and then make the decision.

**Case study from the US (the video isn't sure if it was Walmart or another company):** an employee suggested placing baby diapers next to beer. It sounds strange, since the products look unrelated. But a study showed many customers who bought diapers also bought beer, so there was a correlation visible in the bills. When they put beer next to the diapers, sales went up.

The point: there are many hidden patterns in the real world, and ML brings them out, which helps businesses a lot.

---

## 4. Semi-supervised machine learning

Partly unsupervised and partly supervised, hence the name.

**The problem:** labels (the output column) are **expensive.**

- Who tells you whether a picture has a dog? A human.
- Who tells you whether a student with this IQ and CGPA got placed? A human.
- Creating labels takes human effort, which means paying salaries, which costs money.
- Input data is easy to get. If you need lots of images, you can scrape them from the internet. But to know what's inside each image, someone has to sit and label them manually, costing human hours and money.

**The idea:** what if you don't have to label all the data points? Label just one or two, and the rest get labelled automatically.

**Example: Google Photos.**

1. As you take photos, it automatically recognises that the same person appears in several pictures and groups them together. (That's clustering.)
2. It does the same for another person, and groups those photos separately.
3. Then it asks you who a person is. You say "Dad", and it labels every other photo of that person as Dad. Then it asks about the next person, you say "Mom", and all of her photos get labelled too.

As a user you only had to label one picture per person, and unsupervised ML did the rest in the background. You just copied the label onto the groups.

This technique has become popular in the last few years and is used in many places.

---

## 5. Reinforcement learning

- **Supervised:** input and output both present.
- **Unsupervised:** only input.
- **Reinforcement:** **no data at all.** The algorithm starts learning from zero and slowly improves itself.

It's like humans. When you go to college, you don't have data on how to behave or how to live there, but you learn by making mistakes. A good example is a **self-driving car.** It has no data beforehand, it goes on the road and slowly learns how to drive.

### How it works

| Term | Meaning |
|---|---|
| **Agent** | The algorithm |
| **Environment** | Where the agent has to live (a self-driving car's environment is the road, a chess agent's is the chessboard) |
| **Policy** | The agent's rule book, what it should do |
| **Reward / penalty** | Feedback for each action |

The loop:

1. The agent observes what's happening in the environment.
2. It acts based on its policy. Example: the environment has fire (danger) and water (good), and the policy says "go to the fire".
3. You defined fire as a negative reward (penalty), so when it goes near the fire, you cut some of its points.
4. The agent realises it shouldn't have gone there, and **updates its policy.**
5. It repeats the process with the updated policy. Now it avoids the fire (points get cut there) and goes to the water (it gets points there).

**Overall idea:** an agent in an environment gets a reward or a penalty for every action, and its goal is to maximise reward and minimise penalty. It's like training a dog: give a chocolate when it does something good, scold it when it does something wrong. The brain gets reinforced that this action helps and that one hurts.

### Examples

- **Self-driving cars.**
- **Game-playing agents.** DeepMind (acquired by Google) built **AlphaGo** for the game of Go, a very complex Chinese game, more complex than chess, which people thought was almost impossible for a machine to win. In 2016 or 2017, AlphaGo beat the champion in four out of five games. After this, reinforcement learning started getting a lot of attention in the industry.

It's a bit harder, since you have no data and the agent has to learn by itself, but people are using it more and more.

---

## 6. Summary

| Type | What you have | Typical tasks |
|---|---|---|
| Supervised | Input + output | Regression (numerical output), classification (categorical output) |
| Unsupervised | Only input | Clustering, dimensionality reduction, anomaly detection, association rule learning |
| Semi-supervised | A few labels + lots of unlabelled data | Auto-labelling the rest (like Google Photos) |
| Reinforcement | No data, an agent in an environment | Learning by reward and penalty (self-driving cars, game agents) |

The plan going forward: start with supervised, then unsupervised (3 to 4 techniques), sometimes semi-supervised, and reinforcement learning is a completely separate topic.

The video's advice for beginners: **this diagram should be memorised**, so that when you get a problem you know what type of problem it is.
