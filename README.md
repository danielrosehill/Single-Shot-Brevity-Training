# Single-Shot Brevity Training

A framework for evaluating and training LLMs to provide concise, informative responses without excessive verbosity.

## The Problem

LLM responses often suffer from excessive verbosity - providing lengthy explanations when users want direct, actionable answers. While some context is useful, many models default to "professor mode" with unwanted educational content.

Finding the right balance is challenging: responses should be informative but not overwhelming, structured but not bloated.

## The Approach

This project implements a two-phase approach:

### Phase 1: Baseline Evaluation
Evaluate 10 diverse models (different providers, sizes, architectures) using a standardized test prompt to identify which model naturally provides the best balance of brevity and informativeness in vanilla configuration (no system prompting).

**Rationale**: Before implementing system prompts or fine-tuning, start with the model that's closest to the desired output style.

### Phase 2: Single-Shot Training
Use the best baseline model and implement "single-shot training" via system prompt - provide one example of the desired response style to guide future responses.

**Rationale**: Demonstrating the desired format with a concrete example is more effective than abstract instructions about "being concise."

## Repository Structure

```
Single-Shot-Brevity-Training/
├── prompts/                    # Test prompts
│   └── test-prompt.md         # Standard evaluation prompt
├── system-prompts/            # System prompts for single-shot training
├── data/                      # Reference responses
│   ├── chatgpt-verbose-response.md      # Example of too-verbose output
│   └── ideal-brevity-response.md        # Edited to ideal brevity
├── evaluation/                # Evaluation framework
│   ├── scripts/
│   │   └── evaluate_models.py    # Main evaluation script
│   ├── results/               # Timestamped evaluation results
│   ├── requirements.txt       # Python dependencies
│   └── README.md             # Evaluation documentation
├── docs/                      # Project documentation
│   ├── project-rationale.md   # Why this matters
│   └── model-selection.md     # 10 models chosen and why
└── README.md                  # This file
```

## Quick Start

### Prerequisites
- Python 3.8+
- OpenRouter API key

### Running an Evaluation

1. Clone the repository:
   ```bash
   git clone https://github.com/danielrosehill/Single-Shot-Brevity-Training.git
   cd Single-Shot-Brevity-Training
   ```

2. Set up your OpenRouter API key:
   ```bash
   export OPENROUTER_API_KEY='your-key-here'
   ```

3. Install dependencies:
   ```bash
   pip install -r evaluation/requirements.txt
   ```

4. Run the evaluation:
   ```bash
   python evaluation/scripts/evaluate_models.py
   ```

5. Review results in `evaluation/results/[timestamp]/`

## Models Evaluated

The framework tests 10 carefully selected models:

1. **Anthropic Claude 3.5 Sonnet** - Balanced, professional
2. **Anthropic Claude 3 Haiku** - Designed for speed/efficiency
3. **OpenAI GPT-4o** - Latest GPT-4 variant
4. **OpenAI GPT-4o Mini** - Faster, more concise
5. **Google Gemini 2.0 Flash** - Fast inference
6. **Meta Llama 3.3 70B Instruct** - Open source baseline
7. **Mistral Large** - Known for directness
8. **DeepSeek V3** - Efficient reasoning
9. **Qwen 2.5 72B Instruct** - Strong instruction following
10. **Cohere Command R+** - Business-focused

See [docs/model-selection.md](docs/model-selection.md) for detailed rationale.

## Test Prompt

The evaluation uses a real-world product recommendation prompt (power bank selection) that:
- Is genuinely useful when it works well
- Tends to trigger verbose "professor mode" in some models
- Requires web search for current products
- Has clear, specific questions that can be answered concisely

See [prompts/test-prompt.md](prompts/test-prompt.md) for the full prompt.

## Evaluation Metrics

Each response is analyzed for:
- **Word count** - Primary brevity metric
- **Character count** - Secondary length metric
- **Structure** - Use of headers, bullets, tables
- **Relevance** - Does it answer the specific questions?
- **Information density** - Key facts per 100 words
- **Unnecessary elaboration** - Educational content not requested

## Project Goals

1. **Identify** which model provides the best baseline brevity
2. **Document** the optimal approach for concise-yet-informative responses
3. **Create** reusable system prompts for single-shot training
4. **Share** findings with the community to help others avoid verbose AI responses

## Use Cases

This framework is useful for:
- Product recommendation prompts
- Technical support queries
- Quick research questions
- Any scenario where direct, actionable answers are preferred over lengthy explanations

## Contributing

Contributions welcome! Areas of interest:
- Additional test prompts for different use cases
- Analysis tools for evaluating response quality
- System prompt templates for different brevity levels
- Comparisons with fine-tuning approaches

## License

MIT License - see LICENSE file for details

## Author

Daniel Rosehill
- Website: [danielrosehill.com](https://danielrosehill.com)
- Email: public@danielrosehill.com

## Acknowledgments

Thanks to the OpenRouter team for providing unified access to multiple LLM providers, making this comparative evaluation possible.
