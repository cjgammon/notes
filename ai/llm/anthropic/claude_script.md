# Antrhopic script

Hey guys I thought i'd quick go through an walk through how to set up and use Anthropic's Claude Large Language Model for integration into your applications.

It is available with Python SDK, Typescript SDK, and REST API.
Also available through [Vertex AI API](https://docs.anthropic.com/claude/reference/claude-on-vertex-ai) and [Amazon Bedrock API](https://docs.anthropic.com/claude/reference/claude-on-amazon-bedrock).

We're going to focus on the typescript SDK for this walk through.

First we need to get the API Key which you can get from [console.anthropic.com](https://console.anthropic.com/dashboard). Just click create Key and be sure to store it in a safe place. We'll place this in our .env file. This will live on the server, be sure to never expose this key to the client side.

I've already created a simple web UI with a input field so we're just going to implement a simple node API which will use the SDK.

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
