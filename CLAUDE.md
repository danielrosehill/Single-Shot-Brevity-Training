Here's the idea with this repo:

In general, I find that LLM responses are too "loqacious".

I've been interested in ways to system prompt (or fine tune) a better balance.

The problem: it's a very fine balance. Monosyllabic responses are not usually desirable. Some level of explanation is often informative and useful. But too much is overwhelming. How can you drawl the line.

Here's my thinking here:

I used, as a test prompt, a "find me product recs" prompt that I run often. When it works, it works very well. But when I tried it with ChatGPT, I got a deluge of unwanted and confusing information.

The idea here is really two-fold:

- Firstly run a short evaluation on Open Router to see which model provides the closest experience to what I'm looking for in its vanilla config (without any system prompt). I'd like to limit the evaluation to a few carefully selected contenders. My logic is that before system prompting and tuning, it makes sense to start with the closest fit to the desired format. 

- After doing that, see how a "single shot" training might be implemented. My idea for this: provide an example in the system prompt. In the ChatGPT response captured, I've edited the response provided to model the type of brevity I'm looking for. 