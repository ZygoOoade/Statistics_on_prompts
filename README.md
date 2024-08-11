## Materials

This directory accounts for several notebooks aimed at measuring the performance of a prompt 𝒫 on exercises.
We use the MATHS dataset of [Hendrycks et al. (2021)](https://arxiv.org/pdf/2103.03874) which contains 12,500 mathematical problems, along with their level of difficulty, the branch to which they belong, and the solution to each problem. You can download it [from this link](https://huggingface.co/datasets/qwedsacf/competition_math).

## Procedure

### Load the data

First, we import the data we want to use. For the previous dataset :
```
!pip install datasets -q
```

```
from datasets import load_dataset
ds = load_dataset("qwedsacf/competition_math")
```
### Connect the LLM via an API key
We then use an API key to submit the exercises to an LLM. In this case, we use Gemini-1.5-Pro-exp or LIama 405B.


### Extracting an exercise from the data for input to the LLM

It's easy to extract exercises from loaded data :
```
ds['train'][i]
```
This makes it possible to give LLM an exercise from the data as input.

### Extract the LLM response and store it in a csv file
Then we retrieve the solution proposed by the model :

```
response = completion.choices[0].message.content
```
And we put it in a `csv` file
```
csv_writer.writerow([response])
```
### Iterate 
We then use a `for` loop to iterate this over as many exercises as desired. For example, we can serially give the LLM the first 100 exercises of the training data with 100 API calls, and, at the end of each loop, store the LLM's response in the same `csv` file.
<br>
Once the loop is complete, the result is a table containing one column and 100 rows, where each row $`i`$ contains the LLM's response to the $`i`$-th exercise.
<br>
We can now put three columns in parallel: firstly, the statements of the 100 exercises; secondly, the LLM's answers to each of these 100 exercises; and thirdly, the answers to these 100 exercises. This can be visualized as follows: 
| Exercise Statement | LLM's Solution | Correction |
|:-------------------|:---------------|:-----------|
| Exercise 1 statement | LLM's solution to exercise 1 | Correction to exercise 1 |
| Exercise 2 statement | LLM's solution to exercise 2 | Correction to exercise 2 |
| $`\hspace{1.6cm} ⋮`$ | $`\hspace{2.4cm} ⋮`$ | $`\hspace{2cm} ⋮`$ |
| Exercise *n* statement | LLM's solution to exercise *n* | Correction to exercise *n* |



### Building prompts for the verification model

We propose to "merge" together the statement of problem _i_, the LLM solution to this problem _i_ and the answer to this problem _i_ in a single message with a tagged format. This is achieved by the following code:
```
def concatenate_cells(cell0, cell1, cell2):
    return (f"<Start of problem statement> {cell0} <End of problem statement>."
            f"<Start of solution 1> {cell1} <End of solution 1>."
            f"<Start of solution 2> {cell2} <End of solution 2>")
```




You can also test the performance of other prompts and other models with this method, such as those offered by [OpenAI](https://platform.openai.com/docs/overview) , [Google](https://console.cloud.google.com/vertex-ai/model-garden) or [Anthropic](https://console.anthropic.com) which currently offer the best models to solve mathematical problems according to [the LMSYS leaderboard](https://chat.lmsys.org/?leaderboard).



