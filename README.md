# LLM router

The LLM router is an API that reduces cost by dynamically switching between gpt-4 and gpt-3.5-turbo while retaining quality.

The API is a drop-in replacement for OpenAI's chat completion endpoints. To start using it, all you need to do is to set the OpenAI API base URL to `https://llm.sidekik.ai/v1`, no API key needed.

During the test period, API usage is free.


### Using with `autogen`

To enable this model in Autogen, add this model configuration entry into your `OAI_CONFIG_LIST`.

You do not need to fill in the API key.

```json
{
    "model": "gpt-4",
    "api_key": "",
    "api_base": "https://llm.sidekik.ai/v1",
}
```

### Using with `langchain`

```python
from langchain.chat_models import ChatOpenAI
from langchain.schema import AIMessage, HumanMessage, SystemMessage

chat = ChatOpenAI(temperature=0, openai_api_base="https://llm.sidekik.ai/v1", openai_api_key="-")

messages = [
    SystemMessage(
        content="You are a helpful assistant that translates English to French."
    ),
    HumanMessage(
        content="Translate this sentence from English to French. I love programming."
    ),
]

result = chat(messages)

print(result)
```


### Using with `openai`

```python
import openai

openai.api_base_url = "https://llm.sidekik.ai/v1"

response = openai.ChatCompletion.create(
    model = "gpt-3.5-turbo",
    messages = [{"role": "user", "content": "Hello!"}]
)

print(response)
```

### Using with `curl`

```bash
curl https://llm.sidekik.ai/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
     "model": "gpt-3.5-turbo",
     "messages": [{"role": "user", "content": "Say this is a test!"}],
     "temperature": 0.7
   }'
```
