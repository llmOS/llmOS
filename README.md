# llmOS

llmOS is a free, blazing-fast LLM API running the [Mistral 7B Instruct model](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.1).

The API is a drop-in replacement for OpenAI's chat completion endpoints. To start using it, all you need to do is to set the OpenAI API base URL to `https://api.llmos.dev/v1` and grab your API key [here](https://llmos.dev).

The API will be open-sourced in the future under the [llmOS](https://github.com/llmOS) org.

During the test period, API usage is free.


### Using with `langchain`

```python
from langchain.chat_models import ChatOpenAI
from langchain.schema import AIMessage, HumanMessage, SystemMessage

chat = ChatOpenAI(temperature=0,
                    model="mistral-7b-instruct",
                    openai_api_base="https://api.llmos.dev/v1",
                    openai_api_key="YOUR_API_KEY_HERE"
                    )

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

openai.api_base = "https://api.llmos.dev/v1"
openai.api_key = "YOUR_API_KEY_HERE"

response = openai.ChatCompletion.create(
    model = "mistral-7b-instruct",
    messages = [{"role": "user", "content": "Hello!"}]
)

print(response)
```

### Using with `curl`

```bash
curl https://api.llmos.dev/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE" \
  -d '{
     "model": "mistral-7b-instruct",
     "messages": [{"role": "user", "content": "Say this is a test!"}],
     "temperature": 0.7
   }'
```


### Using with `autogen`

To enable this model in Autogen, add this model configuration entry into your `OAI_CONFIG_LIST`.

```json
{
    "model": "mistral-7b-instruct",
    "api_key": "YOUR_API_KEY_HERE",
    "api_base": "https://api.llmos.dev/v1",
}
```