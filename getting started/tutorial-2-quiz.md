# How to add a Quiz
A quiz is described using the following syntax in your markdown:

```markdown
?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love
```

The snippet above is interpreted by the platform as a Quiz.
- `?[What is the answer to Life, the Universe and Everything?]` is the first line of your quiz and allow you to ask a question to the user.
- `-[ ] There is no answer to that!` is one of the possible answers but it's invalid (no x inside the []).
- `-[x] Easy, this is 42` is a correct answer (x inside []),

This renders as:

?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love

You can learn more about quizzes [here](/markdown/markdown-quiz) and more about the answer to life [here](https://en.wikipedia.org/wiki/Phrases_from_The_Hitchhiker%27s_Guide_to_the_Galaxy#Answer_to_the_Ultimate_Question_of_Life.2C_the_Universe.2C_and_Everything_.2842.29).

# Test your playground
Once you have made all your local modifications, push them and test your playground.
