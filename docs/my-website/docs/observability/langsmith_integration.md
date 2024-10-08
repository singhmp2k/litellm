import Image from '@theme/IdealImage';

# Langsmith - Logging LLM Input/Output


:::tip

This is community maintained, Please make an issue if you run into a bug
https://github.com/BerriAI/litellm

:::


An all-in-one developer platform for every step of the application lifecycle
https://smith.langchain.com/

<Image img={require('../../img/langsmith_new.png')} />

:::info
We want to learn how we can make the callbacks better! Meet the LiteLLM [founders](https://calendly.com/d/4mp-gd3-k5k/berriai-1-1-onboarding-litellm-hosted-version) or
join our [discord](https://discord.gg/wuPM9dRgDw)
::: 

## Pre-Requisites
```shell
pip install litellm
```

## Quick Start
Use just 2 lines of code, to instantly log your responses **across all providers** with Langsmith


```python
litellm.success_callback = ["langsmith"]
```
```python
import litellm
import os

os.environ["LANGSMITH_API_KEY"] = ""
os.environ["LANGSMITH_PROJECT"] = "" # defaults to litellm-completion
os.environ["LANGSMITH_DEFAULT_RUN_NAME"] = "" # defaults to LLMRun
# LLM API Keys
os.environ['OPENAI_API_KEY']=""

# set langsmith as a callback, litellm will send the data to langsmith
litellm.success_callback = ["langsmith"] 
 
# openai call
response = litellm.completion(
  model="gpt-3.5-turbo",
  messages=[
    {"role": "user", "content": "Hi 👋 - i'm openai"}
  ]
)
```

## Advanced
### Set Langsmith fields - Custom Projec, Run names, tags

```python
import litellm
import os

os.environ["LANGSMITH_API_KEY"] = ""
# LLM API Keys
os.environ['OPENAI_API_KEY']=""

# set langfuse as a callback, litellm will send the data to langfuse
litellm.success_callback = ["langsmith"] 
 
response = litellm.completion(
    model="gpt-3.5-turbo",
     messages=[
        {"role": "user", "content": "Hi 👋 - i'm openai"}
    ],
    metadata={
        "run_name": "litellmRUN",               # langsmith run name
        "project_name": "litellm-completion",   # langsmith project name
        "tags": ["model1", "prod-2"]            # tags to log on langsmith
    }
)
print(response)
```

### Make LiteLLM Proxy use Custom `LANGSMITH_BASE_URL`

If you're using a custom LangSmith instance, you can set the
`LANGSMITH_BASE_URL` environment variable to point to your instance.
For example, you can make LiteLLM Proxy log to a local LangSmith instance with
this config:

```yaml
litellm_settings:
  success_callback: ["langsmith"]

environment_variables:
  LANGSMITH_BASE_URL: "http://localhost:1984"
  LANGSMITH_PROJECT: "litellm-proxy"
```

## Support & Talk to Founders

- [Schedule Demo 👋](https://calendly.com/d/4mp-gd3-k5k/berriai-1-1-onboarding-litellm-hosted-version)
- [Community Discord 💭](https://discord.gg/wuPM9dRgDw)
- Our numbers 📞 +1 (770) 8783-106 / ‭+1 (412) 618-6238‬
- Our emails ✉️ ishaan@berri.ai / krrish@berri.ai
