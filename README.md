

## Procedure

This directory accounts for several notebooks aimed at measuring the performance of a prompt 𝒫 on data. As it is, these are mathematical exercises and the data used contain both exercises and their answer keys.

First, we import the data we want to use. For example, we use :
```
!pip install datasets -q
```

```
from datasets import load_dataset
ds = load_dataset("qwedsacf/competition_math")
```
We then use an API key to submit the exercises to an LLM. In this case, we use Gemini-1.5-Pro-exp or LIama 405B.

It's easy to extract exercises from loaded data, e.g. 
```
ds['train'][i]
```
This makes it possible to give LLM an exercise from the data as input.

Then we retrieve the solution proposed by the model :

```
response = completion.choices[0].message.content
```
And we put it in a `csv` file
```
csv_writer.writerow([response])
```

```
def concatenate_cells(cell0, cell1, cell2):
    return (f"<Start of problem statement> {cell0} <End of problem statement>."
            f"<Start of solution 1> {cell1} <End of solution 1>."
            f"<Start of solution 2> {cell2} <End of solution 2>")
```




We use the MATHS dataset of [Hendrycks et al. (2021)](https://arxiv.org/pdf/2103.03874) which contains 12,500 mathematical problems, along with their level of difficulty, the branch to which they belong, and the solution to each problem.




* In the file [Few_data_generation.ipynb](https://github.com/ZygoOoade/Statistics_on_prompts/blob/main/Few_data_generation.ipynb), we run the Gemini-Pro-1.5-exprimental-801 model on the first 10 dataset questions with a customized system prompt.
As it stands, this file is limited to the generation of 10 responses on 10 problems from the dataset.
* In the [Rating gemini's responses.ipynb](https://github.com/ZygoOoade/Statistics_on_prompts/blob/main/Rating%20gemini's%20responses.ipynb) file is simply used by Gemini-Pro to evaluate the quality of Gemini-Pro-Experiment-801 responses on the 10 maths problems.
* As a result, Gemini-pro-express-801 got 9 out of 10 maths problems right.

You can also test the performance of other prompts and other models with this method, such as those offered by [OpenAI](https://platform.openai.com/docs/overview) , [Google](https://console.cloud.google.com/vertex-ai/model-garden) or [Anthropic](https://console.anthropic.com) which currently offer the best models to solve mathematical problems according to [the LMSYS leaderboard](https://chat.lmsys.org/?leaderboard).



