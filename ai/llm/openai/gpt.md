# GPT

## Links

- [Quick Start](https://platform.openai.com/docs/quickstart?context=node)
- [API Reference](https://platform.openai.com/docs/api-reference/chat)

## Example

```typescript
import OpenAI from "openai";

const openai = new OpenAI();

async function main() {
  const completion = await openai.chat.completions.create({
    messages: [{ role: "system", content: "You are a helpful assistant." }],
    model: "gpt-3.5-turbo",
  });

  console.log(completion.choices[0]);
}

main();
```

## Parameters

#### model (required)

- gpt-4
  - highest quality
- gpt-4-turbo-preview
  - preview of faster model
- gpt-3.5-turbo
  - fastest

#### [messages](https://platform.openai.com/docs/api-reference/chat/create#chat-create-messages) (required)

- System
- User
- Assistant
- Tool

#### frequency_penalty (optional)

Value between -2.0 and 2.0. Higher value reduce the likelihood of repetition.

#### max_tokens (optional)

Maximum number of tokens to generate.

#### n (optional)

Number of completions to generate.

#### response_format (optional)

```json
{ "type": "json_object" }
```

#### seed (optional)

Attempt to create deterministic completions by setting seed.

#### stream (optional)

Uses server events to stream results.

#### temperature (optional)

Values between 0.0 and 2.0. Higher value makes the model more creative.

#### tools (optional)

Array of tools the model can use. Currently only functions are supported.

#### tool_choice (optional)

Determines whether the model can choose which tools to use. Takes values `none`, `auto`, or an object specifying the tool to use.

```json
{
  "type": "function",
  "function": { "name": "my_function" }
}
```
