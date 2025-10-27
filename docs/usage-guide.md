# Usage Guide

## Running Your First Evaluation

### Step 1: Set Up Environment

Create a Python virtual environment (recommended):

```bash
cd Single-Shot-Brevity-Training
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r evaluation/requirements.txt
```

### Step 2: Configure API Access

Get an OpenRouter API key:
1. Sign up at [OpenRouter](https://openrouter.ai/)
2. Add credits to your account ($5-10 is sufficient)
3. Generate an API key

Set the environment variable:

```bash
export OPENROUTER_API_KEY='sk-or-v1-...'
```

Or add to your `.env` file:

```bash
echo "OPENROUTER_API_KEY=sk-or-v1-..." > .env
```

### Step 3: Run Evaluation

```bash
python evaluation/scripts/evaluate_models.py
```

The script will:
- Load the test prompt from `prompts/test-prompt.md`
- Call each of the 10 models via OpenRouter
- Save individual responses and analysis
- Generate a summary with brevity rankings

### Step 4: Review Results

Results are saved in `evaluation/results/YYYYMMDD_HHMMSS/`:

**Quick review:**
```bash
# View the summary
cat evaluation/results/[timestamp]/summary.json | jq

# Read individual responses
ls evaluation/results/[timestamp]/*.md
```

**Check brevity ranking:**
The summary.json shows models ranked by word count.

**Read responses:**
Each model's response is saved as both:
- `.json` - Full structured data
- `.md` - Human-readable text

## Interpreting Results

### What to Look For

**Good brevity indicators:**
- Answers all 3 questions directly
- Uses structured format (headers, bullets, tables)
- No lengthy explanations of basic concepts
- No "let me explain..." preambles
- Gets straight to the answers

**Red flags (too verbose):**
- Long introductions before answering
- Explanations of concepts not requested
- Repeated information
- "Here's what you need to know" sections
- Academic/professorial tone

### Comparing Responses

Create a comparison document:

```bash
# Extract just the response texts
for f in evaluation/results/[timestamp]/*.md; do
    echo "=== $(basename $f) ===" >> comparison.txt
    cat $f >> comparison.txt
    echo -e "\n\n" >> comparison.txt
done
```

### Quantitative Analysis

The script provides:
- **Word count**: Lower is generally better (but not at the cost of missing info)
- **Character count**: Secondary metric
- **Structure indicators**: Shows if bullets/tables/headers were used

### Qualitative Analysis

For each response, ask:
1. Did it answer all 3 questions?
2. Were the answers accurate?
3. Was additional context helpful or distracting?
4. Would you prefer this response over others?

## Customizing the Evaluation

### Test Different Prompts

Edit `prompts/test-prompt.md` with your own prompt. The script automatically loads this file.

**Tips for good test prompts:**
- Have specific questions
- Represent real use cases
- Trigger varying response styles across models

### Test Different Models

Edit the `MODELS` list in `evaluation/scripts/evaluate_models.py`:

```python
MODELS = [
    "anthropic/claude-3.5-sonnet",
    # Add more models from OpenRouter
]
```

Find available models at [OpenRouter Models](https://openrouter.ai/models)

### Adjust Analysis Metrics

Modify the `analyze_response()` function in `evaluate_models.py` to add custom metrics:

```python
def analyze_response(response_text: str) -> Dict[str, Any]:
    # Add your own analysis here
    return {
        "word_count": len(words),
        "custom_metric": your_calculation()
    }
```

## Phase 2: Single-Shot Training

After identifying the best baseline model:

### 1. Create System Prompt

Create a file in `system-prompts/` with your ideal example:

```markdown
# System Prompt for [Model Name]

When answering questions, provide concise, structured responses.

## Example

User: [Your test prompt]