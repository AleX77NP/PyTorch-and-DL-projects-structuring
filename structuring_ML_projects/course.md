# 1. Orthogonalization 
is a system design property that ensures that modification of an instruction or an algorithm component does not create or propagate side effects to other system components.
Orthogonalization makes it easier to independently verify the algorithms, thus reducing the time required for testing and development.
One of the problems with developing machine learning systems is that there are so many things that you might try to change.
For instance, so many hyperparameters you might tune. One of the things I have noticed is about is that most people who is learning machine learning were really consistent about what to tune?
To try and achieve one result. This process is what we call orthogonalisation.

Chain of assumptions in ML:
 - Fit training set well on cost function
 - Fit dev set well on cost function
 - Fit test set well on cost function
 - Performs well in real world


# 2. Single Number Evaluation
Precision, Recall, F1 score, average error percentage

# 3. Satisficing and Optimizing metrics
A acc: 90% running_time: 80ms
B acc: 92% running_time: 95ms
C acc: 95% running_time: 1500ms

acc = optimizing metric ( max value )
other satisficing metrics ( < 100 ms )

Siri example: max acc, <= 1 false positive in the last 24 hours

# 4. Dev/Test sets
Should come from same distribution! These sets should reflect data
you except to get in the future and consider important to do well on.

Set sizes?
70-30? 60-20-20? thousands of records
98-1-1 millions of records

Test set big enough to give you confidence in the overall 
performance of the system

No test set? Sometimes only train, dev

When to change? If you prefer some set over other that performs better
when you look at dev + metrics, you should change.

Give much higher weight to problematic data. (1 possible evaluation metric)

- Define metrics to evaluate
- Think about how to do well on this metric

If dev/test works good, but real user examples fail to meet expectations,
try new metric

# 5. Human-level performance
Bayes optimal error - perfect level accuracy (can't be surpassed)

- Get labeled data from humans
- Question why human got it right
- Check Bias/variance

Doing bad on training set? Check Bias (Avoidable Bias)
Doing bad on dev set? Check Variance (Variance problem)

Compare to Human level
Human error ~ Bayes error

abs(HLE - TrainingErr) -> Bias reduction
abs(TrainingErr - DevErr) -> Work on variance

Surpassing HLP
training error < human error ? less clear what to do

Humans are quite good at perception tasks, hard to surpass

# 6. Improving Model Performance
- Fit training set well
- Training performance generalizes well on dev/test set

1. Check error difference between HLE and Training error (Bias)
2. Check error difference between Training error and dev error (Variance)

Bias error -> train bigger NN, train longer, try other 
optimization methods, better hyperparams, try other architectures for NN

Variance error -> more data, data augmentation,
regularization, NN architecture/hyperparams search

# 7. Carrying Out Error Analysis
Get mislabeled data - check it.
Create table, analyze where model fails

# 8. Cleaning Up Incorrectly Labelled Data
Sometimes small amount of error doesn't matter

If error number plays significant difference, fix it!
(Or it plays a big part in total error)

# 9. Training and Testing on Different Distributions
option 1: Shuffle 2 different sets? Will optimize for the set
that has more data (web, mobile for example)

option2: train = web + mobile, dev/test = mobile
(different distributions) - Better option!

# 10. Bias & Variance with mismatched data
Introduce Training-dev set = shuffle training, take small part,
call it training-dev.
Do not train on it

Same distribution: training & training-dev , dev & test

- if training-dev error is much bigger than training error - Variance
problem

- if training-dev error is similar to training error, but much larger
on dev, that's distribution problem = mismatched data

- if large error (~10%) on all 3 sets - Avoidable Bias error, much 
larger error than HLE

- if large error (~10%) on all training, training-dev sets,
and even larger (~20%) on dev = Avoidable Bias error, much 
larger error than HLE AND Variance error

- Large difference on error between dev and test sets? Overfitting
on dev (find bigger dev set)

# 11. Addressing Data mismatch
- Different distributions
1. Carry out manual error analysis to try to understand
difference between training and dev/test sets
2. Make training daya more similar, collect more data similar
to dev/test sets
3. Artificial Data Synthesis (Example: "The quick brown fox jumps
over the lazy dog" + Car noise)
Problem of overfitting to specific set of data (1 hour car noise,
20 different cars ...)

# 12. Transfer Learning
Transfer learning (TL) is a research problem in machine learning (ML) that focuses on storing knowledge gained
while solving one problem and applying it to a different but related problem.
For example, knowledge gained while learning to recognize cars could apply when trying to recognize trucks. 
This area of research bears some relation to the long history of psychological literature on transfer of learning, 
although practical ties between the two fields are limited. From the practical standpoint, 
reusing or transferring information from previously learned tasks for the learning of new tasks has the potential to 
significantly improve the sample efficiency of a reinforcement learning agent.

# 13. Multitask Learning
Multi-task learning (MTL) is a subfield of machine learning in which multiple learning tasks are solved
at the same time, while exploiting commonalities and differences across tasks. This can result in improved learning
efficiency and prediction accuracy for the task-specific models, when compared to training the models separately.

Example: 1 NN to check if image contains traffic lights, cars, stop signs etc.

Use cases: Benefit from shared low-level features, big enough NN, similar 
amount of data for each task

# 14. End-to-end deep learning
End-to-end (E2E) learning refers to training a possibly complex learning system represented by a single model
(specifically a Deep Neural Network) that represents the complete target system, bypassing the intermediate layers
usually present in traditional pipeline designs.

Whether to use it? Ask yourself if you have sufficient data to learn
a function of the complexity needed to map X to Y.
