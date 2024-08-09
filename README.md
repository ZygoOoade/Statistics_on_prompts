We use the MATHS dataset of [Hendrycks & al. (2021)](https://arxiv.org/pdf/2103.03874).

In the file [Few_data_generation.ipynb](https://github.com/ZygoOoade/Statistics_on_prompts/blob/main/Few_data_generation.ipynb), we run the Gemini-Pro-1.5-exprimental-801 model on the first 10 dataset questions with a customized system prompt.
As it stands, this file is limited to the generation of 10 responses.
In the [Rating gemini's responses.ipynb](https://github.com/ZygoOoade/Statistics_on_prompts/blob/main/Rating%20gemini's%20responses.ipynb) file is simply used by Gemini-Pro to evaluate the quality of Gemini-Pro-Experiment-801 responses on the 10 maths problems.
As a result, Gemini-pro-express-801 got 9 out of 10 maths problems right.

But you can test the performance of other prompts and other models, such as those offered by [OpenAI](https://platform.openai.com/docs/overview) , [Google](https://console.cloud.google.com/vertex-ai/model-garden) or [Anthropic](https://console.anthropic.com) which currently offer the best models to solve mathematical problems according to [the LMSYS leaderboard](https://chat.lmsys.org/?leaderboard).



