# Claude

## Notes

Available with Python SDK, Typescript SDK, and REST API.
Also available through [Vertex AI API](https://docs.anthropic.com/claude/reference/claude-on-vertex-ai) and [Amazon Bedrock API](https://docs.anthropic.com/claude/reference/claude-on-amazon-bedrock).

## Links

- [Client SDKs](https://docs.anthropic.com/claude/reference/client-sdks)
- [Typescript SDK Github](https://github.com/anthropics/anthropic-sdk-typescript)
- [API References](https://docs.anthropic.com/claude/reference/messages_post)

## Example

```typescript
import Anthropic from "@anthropic-ai/sdk";

const anthropic = new Anthropic({
  apiKey: "my_api_key", // defaults to process.env["ANTHROPIC_API_KEY"]
});

const msg = await anthropic.messages.create({
  model: "claude-3-opus-20240229",
  max_tokens: 1024,
  messages: [{ role: "user", content: "Hello, Claude" }],
});
console.log(msg);
```

## Parameters

#### model (required)

- claude-3-opus-20240229
  - highest quality
- claude-3-sonnet-20240229
  - balance between quality and speed
- claude-3-haiku-20240307
  - fastest

#### messages (required)

```typescript
[
  { role: "user", content: "Hello there." },
  { role: "assistant", content: "Hi, I'm Claude. How can I help you?" },
  { role: "user", content: "Can you explain LLMs in plain English?" },
];
```

**Image Example**

```typescript
{"role": "user", "content": [
  {
    "type": "image",
    "source": {
      "type": "base64",
      "media_type": "image/jpeg",
      "data": "/9j/4AAQSkZJRg...",
    }
  },
  {"type": "text", "text": "What is in this image?"}
]}
```

#### max_tokens (required)

Max number of tokens to generate. Caps at 4096.

#### system (optional)

The system prompt is a message that Claude will see before generating a response. It can be used to provide context or additional information to Claude.

#### metadata (optional)

```typescript
{
  "user_id": "1234",
}
```

`user_id` A uuid to track a user

#### stop sequences (optional)

Optional array of strings that Claude should stop generating after.

#### stream (optional)

Enable streaming mode. This is useful for long running requests.

```typescript
import Anthropic from "@anthropic-ai/sdk";

const anthropic = new Anthropic();

const stream = await anthropic.messages.create({
  max_tokens: 1024,
  messages: [{ role: "user", content: "Hello, Claude" }],
  model: "claude-3-opus-20240229",
  stream: true,
});
for await (const messageStreamEvent of stream) {
  console.log(messageStreamEvent.type);
}
```

#### temperature (optional)

Amount of randomness in the output. 0.0 is deterministic, 1.0 is maximum randomness.
