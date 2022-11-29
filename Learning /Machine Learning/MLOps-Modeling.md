## Baselines
[[Baseline Model]] are simple benchmarks for iterative development.
### Process
1. Start with simplest possible baseline to compare subsequent development with. This is often a random model.
2. Slowly add complexity by addressing limitations and motivating representations and model architectures
3. Weight tradeoffs (performance, latency, size, etc) between performant baselines
4. Revisit and iterate on baselines as your dataset grows.

> When choosing what model architectures to proceed with, what are important tradeoffs to consider? And how can we prioritize them?

- Prioritization of these tradeoffs depends on your context.
	-   `performance`: consider coarse-grained and fine-grained (ex. per-class) performance.
	-   `latency`: how quickly does your model respond for inference.
	-   `size`: how large is your model and can you support it's storage.
	-   `compute`: how much will it cost ($, carbon footprint, etc.) to train your model?
	-   `interpretability`: does your model need to explain its predictions?
	-   `bias checks`: does your model pass key bias checks?
	-   `time to develop`: how long do you have to develop the first version?
	-   `time to retrain`: how long does it take to retrain your model? This is very important to consider if you need to retrain often.
	-   `maintenance overhead`: who and what will be required to maintain your model versions because the real work with ML begins after deploying v1. You can't just hand it off to your site reliability team to maintain it like many teams do with traditional software.

### Iterate on the data
Instead of using a fixed dataset and iterating on the models, choose a good baseline and iterate on the dataset:
-   remove or fix data samples (false positives & negatives)
-   prepare and transform features
-   expand or consolidate classes
-   incorporate auxiliary datasets
-   identify unique slices to boost

