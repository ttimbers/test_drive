---
title       : Classification
description : The classification problem; applications to data; neighbourhood methods and majority vote.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

---
## A really bad movie

```yaml
type: MultipleChoiceExercise
lang: r
xp: 50
skills: 1
key: ddbdafacdf
```

Suppose, you have the following data where happiness score and puppy count (how many puppies you have) are the 2 input variables and cat ownership (yes or no) is the dependent variable. Use the plot on the right, can you predict the cat ownership status of a new person who scored a happiness score of 2 when there were 4 puppies in the room using eucludian distance in 3-NN. Choose from the list below:

`@instructions`
- this person owns a cat
- this person does not own a cat
- cannot say whether or not this person owns a cat 


`@hint`
Have a look at the plot. Which group will this new point be closest to?

`@pre_exercise_code`
```{r}
# load libraries
library(readr)
library(ggplot2)

# load data
happiness_data <- read_csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_6643/datasets/k-nn_simple_data.csv")

# plot data
ggplot(data = happiness_data, aes(x = puppy_count, y = happiness_score, colour = cat_owner)) +
  geom_point(size = 2) +
  xlab("Number of puppies in room") +
  ylab("Happiness score (1-5)") +
  scale_colour_discrete(name="Cat owner")
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! 3-NN using eucludian distance would have us predict that this person likely owns a cat!."
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad, msg_bad))
```

---
## More movies

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 3a60a11144
```

In the previous exercise, you saw a dataset about movies. In this exercise, we'll have a look at yet another dataset about movies!

A dataset with a selection of movies, `movie_selection`, is available in the workspace.

`@instructions`
- Check out the structure of `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`.

`@hint`
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

`@pre_exercise_code`
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
load(url("https://s3.amazonaws.com/assets.datacamp.com/course/teach/movies.RData"))
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"), c("Genre", "Rating", "Run")]

# Clean up the environment
rm(Movies)
```

`@sample_code`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

`@solution`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```
