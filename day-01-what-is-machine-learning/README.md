# Day 01: What is Machine Learning?

> Series: 100 Days of Machine Learning (CampusX)
> Day: 1 / 100
> Topics: What ML is, explicit programming vs ML, when to use ML, history, job market

---

## TL;DR

Machine learning means giving a computer **data** (inputs and outputs) and letting an algorithm find the rule itself, instead of you writing the rule by hand. It wins in places where hand-written rules break: things that keep changing, things with too many cases, and hidden patterns in data.

---

## About This Series

- One video every day for 100 days.
- It is **not** an algorithms playlist (those already exist on the channel). It covers the flow around the algorithms: the ML life cycle, imputation, preprocessing, analysis, model selection, feature selection, bias-variance trade-off, deployment.
- Level: beginner to intermediate.
- Core idea from the intro: knowing algorithms is mandatory, but knowing how to build an end-to-end project is what most beginners skip.

---

## Key Concepts

### What is Machine Learning?
A field of computer science that uses statistical techniques to give computers the ability to "learn" from data without being explicitly programmed. In simple words: **learning from data**.

### Explicit programming vs ML

| | Traditional programming | Machine learning |
|---|---|---|
| You give | Input + the logic you wrote | Input + output (data) |
| You get | Output | The logic (the model) |
| Who writes the rules | You | The algorithm |
| New scenario | You edit the code | Data changes, logic updates |

**Why this matters:** in normal code, every case needs a rule you wrote. In ML, the rules are the *result* of training, not the input.

### The addition example (from the video)
- A program that adds two numbers only works for two numbers. Give it four and it breaks.
- In ML you give a sheet of numbers and their sums. The model figures out the pattern is "addition" and extends it.
- Caveat: the video uses this as intuition. In practice a model has a fixed number of input features, so "2, 4 or 10 numbers" won't work out of the box with a simple model.

---

## When ML Beats Traditional Software

**1. You can't keep up writing rules (spam filter)**
- A hand-written spam filter is a long if-else ladder: "if 'huge' appears more than 3 times, it's spam."
- Spammers just switch to "big" or "massive" and you rewrite the rules, forever.
- With ML, you retrain on new data and the logic updates itself.

**2. You can't even list the cases (image classification)**
- "Is there a dog in this picture?" Hundreds of breeds, sizes, colours.
- Impossible to hand-code. We learn to spot dogs as kids by seeing examples, and ML does the same.

**3. Hidden patterns in data (data mining)**
- Data analysis = finding patterns by plotting graphs.
- Data mining = when patterns are too hidden for graphs, so you train an ML model and inspect what it learned (e.g. which words made it call an email spam).
- ML is the main tool for data mining.

---

## Why ML Took Off After 2010

The speaker compares it to Nawazuddin Siddiqui: he was around for years in small roles, then a shift in the industry made him a star. ML was the same, the theory and maths existed for 40-50 years.

What was missing back then, and what changed:

| Problem earlier | What fixed it |
|---|---|
| Not enough data, and labelling it was tedious | Internet + smartphones, huge data generation |
| Weak hardware (128MB RAM was a big deal) | Cheap powerful hardware, GPUs, phones with 12GB RAM |

He also claims that all the digital data created from the start of mankind till 2015 was generated again in 2016 alone, showing how fast data is growing.

---

## The Job Market Point

His argument is plain economics:
- A new in-demand skill has few people, so companies compete and salaries are high (Java earlier, ML now).
- High salaries pull more people in, supply grows, and salaries normalise (like Java today).
- His take: we're still on the upward part of the curve, so learning it properly now is a good time.

(This is his opinion and a simple model, not a guarantee.)

---

## Key Takeaways

- ML = data in, rules out. Programming = rules in, output out.
- Use ML when rules keep changing, cases are countless, or patterns are hidden.
- ML isn't new, what changed after 2010 was data + hardware.
- Algorithms alone aren't enough, you need the whole project flow.

---

## Questions to Think About

1. If ML learns the rules from data, what happens when the data is bad or biased?
2. For which problems would plain if-else code still be the better choice?
3. Why does the spam example get easier with ML when spammers change their words?
4. If the model learned "addition", how would you actually check it didn't just memorise the training rows?

---

## My Notes

<!-- Add your own thoughts, confusions, and anything you want to revisit -->

---

## Code

No code in the video. Small demo of the "learn addition from data" idea (my own, not from the video):

```python
from sklearn.linear_model import LinearRegression
import numpy as np

# data: pairs of numbers and their sum
X = np.array([[1, 2], [3, 4], [5, 6], [7, 8], [2, 9]])
y = X.sum(axis=1)

model = LinearRegression().fit(X, y)

print(model.predict([[10, 20]]))  # ~30
print(model.coef_)                # ~[1, 1], the "rule" it found
```

Compare with explicit programming: `def add(a, b): return a + b`. Here we never wrote the plus sign, the model found weights close to 1 on its own.
