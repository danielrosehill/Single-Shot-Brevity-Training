# Model Selection for Brevity Evaluation

## Selection Criteria

The goal is to identify which models naturally provide concise, informative responses without excessive verbosity. We're testing vanilla configurations (no system prompting) to find the best baseline before implementing single-shot training.

## Selected Models (10)

### 1. **Anthropic Claude 3.5 Sonnet** (`anthropic/claude-3.5-sonnet`)
- Known for balanced, professional responses
- Strong reasoning capabilities
- Generally concise without excessive elaboration

### 2. **Anthropic Claude 3 Haiku** (`anthropic/claude-3-haiku`)
- Designed for speed and efficiency
- Naturally more concise than larger Claude models
- Good baseline for brevity-first approach

### 3. **OpenAI GPT-4o** (`openai/gpt-4o`)
- Latest GPT-4 variant
- Known for being more direct than GPT-4
- Good general-purpose baseline

### 4. **OpenAI GPT-4o Mini** (`openai/gpt-4o-mini`)
- Smaller, faster variant
- Typically more concise due to size constraints
- Cost-effective option

### 5. **Google Gemini 2.0 Flash** (`google/gemini-2.0-flash`)
- Latest Gemini model
- Fast inference, typically concise
- Strong web search capabilities

### 6. **Meta Llama 3.3 70B Instruct** (`meta-llama/llama-3.3-70b-instruct`)
- Open source baseline
- Strong instruction following
- Good balance of capability and conciseness

### 7. **Mistral Large** (`mistral/mistral-large-latest`)
- European model with different training approach
- Known for direct, less verbose responses
- Strong technical capabilities

### 8. **DeepSeek V3** (`deepseek/deepseek-chat`)
- Chinese model with unique architecture
- Efficient reasoning approach
- Typically concise responses

### 9. **Qwen 2.5 72B Instruct** (`qwen/qwen-2.5-72b-instruct`)
- Strong open-source alternative
- Good instruction following
- Balanced output style

### 10. **Cohere Command R+** (`cohere/command-r-plus`)
- Designed for business use cases
- RAG-optimized
- Typically produces structured, concise outputs

## Rationale

This selection provides:
- **Size diversity**: From efficient small models (Haiku, GPT-4o Mini) to large capable models
- **Provider diversity**: Anthropic, OpenAI, Google, Meta, Mistral, DeepSeek, Qwen, Cohere
- **Architecture diversity**: Different training approaches and philosophies
- **Known characteristics**: Mix of models known for verbosity (to test worst case) and conciseness

## Expected Outcomes

Based on general characteristics:

**Most Likely to Be Concise:**
1. Claude 3 Haiku
2. GPT-4o Mini
3. Mistral Large
4. DeepSeek V3

**Most Likely to Be Verbose:**
1. GPT-4o (tends toward longer explanations)
2. Llama 3.3 70B (often provides detailed context)
3. Cohere Command R+ (comprehensive by design)

**Wild Cards:**
1. Gemini 2.0 Flash (variable depending on prompt)
2. Claude 3.5 Sonnet (balanced, context-dependent)
3. Qwen 2.5 72B (less predictable in English)

## Next Steps

1. Create evaluation script that tests each model with the test prompt
2. Capture full responses for qualitative analysis
3. Score responses on:
   - Length (word count, character count)
   - Information density (key facts per 100 words)
   - Relevance (does it answer the specific questions asked?)
   - Structure (is it organized clearly?)
   - Unnecessary elaboration (educational content not requested)
4. Identify the best baseline model
5. Test single-shot training approach on that model
