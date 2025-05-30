---
layout: default
title: PROMPT CACHING
---

# How to structure OpenAI API prompts so you pay (and wait) less.

### Why prompt caching matters
| Metric | Without caching | With caching (≥ 1 024 identical tokens) |
| --- | --- | --- |
| Latency | 100 % | ↓ 40-80 % |
| Prompt-token cost | 100 % | ↓ 50-75 % |

### 1. Rule of thumb
Static first → Dynamic last
- To realize caching benefits, place static content like instructions and examples at the beginning of your prompt, and put variable content, such as user-specific information, at the end.
- Caching is enabled automatically for prompts that are 1024 tokens or longer.

### 2. Code patterns
❌ Anti-pattern – cache won't work because the user's data is at the beginning of the prompt and changes often. Static content (e.g. instructions) needs to be at the beginning of the prompt.
```js
messages = [
  { role: "user",   content: `My résumé: ${resume}` },
  { role: "user",   content: `Job description: ${jobDesc}` },
  { role: "system", content: SYSTEM_PROMPT }
];
```

✅ Basic pattern – static instructions first, dynamic user data at the end.
```js
messages = [
  { role: "system", content: SYSTEM_PROMPT },
  { role: "user",   content: `My résumé: ${resume} Job: ${jobDesc}` }
];
```

### 3. Using the `user` parameter

OpenAI uses the `user` parameter to boost cache hit rates by better bucketing similar requests.

Hash, e.g. the user's email, to create a stable and anonymous identifier that you can use to scope the cache.

```js
import crypto from "crypto";

const userHash = crypto.createHash("sha256")
                       .update(userEmail)
                       .digest("hex"); // stable & anonymous

const response = await openai.chat.completions.create({
  model: "gpt-4o",
  messages,
  temperature: 0.7,
  user: userHash // cache scoped per end-user
});
```

### 4. Full Example
```js
import crypto from "crypto";
import OpenAI from "openai";

const openai = new OpenAI();

const instructions = `you are a cover letter generator...`

function sha256(str: string) {
  return crypto.createHash("sha256").update(str).digest("hex");
}

const userHash = sha256(loggedInUserEmail); // anonymous

const response = await openai.chat.completions.create({
  model: gptModel,
  messages: [
    { role: "developer", content: instructions }, 
    { role: "user",
      content: `My Resume: ${resume} Job Title: ${title} Job Description: ${description}` }
  ],
  temperature,
  user: userHash  // per-user identifier helps improve caching
});
```