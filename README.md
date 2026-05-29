# 🚀 AI LinkedIn Caption Generator

> Fully automated LinkedIn content pipeline — input an idea, get a professional post with a matching AI-generated image published to LinkedIn automatically.

## What It Does

1. You provide any topic idea (AI, business, food, tech...)
2. GPT-4o-mini generates a professional LinkedIn caption with emojis and hashtags
3. DALL-E generates a matching visual image
4. The post + image is **automatically published** to your LinkedIn profile

## Workflow Architecture

```
Manual Trigger
      │
      ▼
Set Idea (topic input)
      │
      ▼
GPT-4o-mini ──── System prompt: "You are a LinkedIn expert"
      │           Returns JSON: { caption, image_prompt }
      ▼
Parse JSON fields
      │
      ▼
DALL-E Image Generation ← uses image_prompt
      │
      ▼
LinkedIn API → Publish Post + Image ✅
```

## Nodes Used

| Node | Purpose |
|---|---|
| Manual Trigger | Start the workflow |
| Set Fields | Define the topic idea |
| OpenAI (GPT-4o-mini) | Generate caption + image prompt as JSON |
| Set Fields | Parse caption and image_prompt from response |
| OpenAI (DALL-E) | Generate image from prompt |
| LinkedIn | Publish post with image |

## Setup Instructions

1. Import `linkedin_caption_generator.json` into your n8n instance
2. Add your **OpenAI API key** under Credentials → OpenAI
3. Connect your **LinkedIn account** via OAuth2
4. Edit the `idea` field in the Set node with your topic
5. Click **Execute Workflow**

## Example Output

**Input idea:** `"The future of AI in personalized food recommendations"`

**Generated caption:**
```
🍽️ AI is transforming how we eat — and it's more personal than ever.

Imagine an app that knows you prefer low-carb on Mondays, spicy food when stressed...
That's not the future. It's happening now.

#ArtificialIntelligence #FoodTech #Personalization #AIInnovation
```

## What I Learned
- Chaining OpenAI calls: first for text generation, then for image generation
- Structured JSON output from LLMs for reliable downstream parsing
- LinkedIn OAuth2 integration and media upload flow in n8n
- Prompt engineering for consistent professional tone

## Tech Stack
`n8n` · `OpenAI GPT-4o-mini` · `DALL-E` · `LinkedIn API`
