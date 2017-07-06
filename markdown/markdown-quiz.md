# Quiz extension
We added an extension to create multiple-choice quizzes. For any quiz, you can set up a question with a list of one or more possible answers. The default behaviours are:
- Display radio buttons to the user when the question can have only one correct answer.
- Display checkboxes to the user when the question can have multiple correct answers.

You can add a parameter on the quiz to force the type of quiz (radio buttons or checkbox).

# Simple example
```
?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love
```

will produce the following result:


?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love

The solution will be validated if the user checks the third item.

# Question label
The question label starts with the token `?[` and ends with the token `]`.

```
?[This is the label used for the question.]
```

# Choice items
Choice items are composed of 3 elements:
- The dash prefix: `-`
- The validity token of the item:
  - `[X]` token means a valid choice
  - `[ ]` token means a wrong choice
- The label of the item

Examples:
```
-[ ] This is an invalid choice
-[X] This is a valid choice
```

toto
# Force single or multiple choice answer style
Sometime, we need to force a single choice.
The choice answer style can be forced with the a parameter following the question label.
- Single answer: Radio button style, a single answer can be forced with the `single` parameter
- Multiple answers: Checkbox style can be forced with the `multiple` parameter

Example:
```
?[This is the label used for the question](single)
- [ ] Choice 1
- [X] Choice 2 which is a valid answer
- [ ] Choice 3
- [X] Choice 4 which is a valid answer
```
