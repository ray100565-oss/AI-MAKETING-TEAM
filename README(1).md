# 🤖 AI Marketing Team

An AI-powered marketing automation system built with **n8n**. A central AI agent orchestrates specialized workflows for content creation, image generation, image editing, image search, and faceless video production.

## ✨ Features

- 🧠 **AI Marketing Agent** — Central agent that understands requests and delegates tasks.
- 📝 **Blog Post Generation** — Create blog content based on a topic and target audience.
- 🎨 **AI Image Generation** — Generate images from natural-language prompts using OpenAI.
- ✏️ **AI Image Editing** — Edit existing images based on user instructions.
- 🔍 **Image Search** — Search an image database and retrieve existing assets.
- 🎬 **Faceless Video Generation** — Generate images, audio, and render video content.
- 💾 **Asset Management** — Store generated assets in Google Drive and log them in Google Sheets.
- 💬 **Telegram Integration** — Interact with the marketing agent through Telegram.

## 🏗️ Architecture

```text
                    ┌───────────────────┐
                    │   Telegram User   │
                    └─────────┬─────────┘
                              │
                              ▼
                  ┌───────────────────────┐
                  │   AI Marketing Team   │
                  │      Main Agent       │
                  └───────────┬───────────┘
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
        ┌─────────┐     ┌────────────┐   ┌────────────┐
        │  Blog   │     │Create Image│   │ Edit Image │
        │  Post   │     └──────┬─────┘   └─────┬──────┘
        └─────────┘            │               │
                               ▼               ▼
                         ┌────────────┐   ┌────────────┐
                         │Search Image│   │Google Drive│
                         └────────────┘   └────────────┘

                              │
                              ▼
                     ┌─────────────────┐
                     │ Faceless Video  │
                     └─────────────────┘
```

## 📂 Workflows

### AI Marketing Team

The main orchestration workflow uses an AI agent with conversational memory and specialized workflow tools.

The agent can call:

- `createImage`
- `editImage`
- `searchImages`
- `blogPost`

### Create Image

The image-generation workflow accepts:

- `imageTitle`
- `imagePrompt`
- `chatID`

It creates a detailed image prompt and generates an image using OpenAI's `gpt-image-1`. The generated image is then converted to a file, uploaded to Google Drive, and logged in Google Sheets.

### Edit Image

The image-editing workflow accepts:

- `image`
- `request`
- `chatID`
- `pictureID`

It downloads the selected image and sends it to OpenAI's image editing endpoint using `gpt-image-1`. The edited image is then stored and logged.

### Search Images

The image-search workflow searches an image database stored in Google Sheets.

Inputs:

- `intent`
- `image`
- `chatID`

The agent returns structured image information including the image name, ID, link, and status.

### Faceless Video

The faceless-video workflow combines multiple automated stages:

1. Generate image prompts
2. Generate images
3. Generate sound prompts
4. Generate audio
5. Merge media
6. Render the video
7. Download the rendered video

## 🧰 Tech Stack

| Technology | Purpose |
|---|---|
| **n8n** | Workflow automation |
| **OpenRouter** | AI language model access |
| **OpenAI** | Image generation & editing |
| **Telegram** | User interface |
| **Google Drive** | Asset storage |
| **Google Sheets** | Asset database/logging |
| **PiAPI** | Image generation |
| **ElevenLabs** | Audio generation |
| **Creatomate** | Video rendering |

## 🚀 Installation

### 1. Set up n8n

Set up an n8n instance using either self-hosting or an n8n-hosted environment.

### 2. Import Workflows

Import the workflow files from:

```text
workflows/
├── AI_Marketing_Team.json
├── Create_Image.json
├── Edit_Image.json
├── Search_Images.json
└── Faceless_Video.json
```

### 3. Configure Credentials

Configure your own credentials for:

- OpenAI
- OpenRouter
- Telegram
- Google Drive
- Google Sheets
- PiAPI
- ElevenLabs
- Creatomate

### 4. Configure Resources

Update Google Drive folders, Google Sheets, workflow references, and other environment-specific IDs for your own n8n environment.

### 5. Activate the Workflows

Test each workflow individually before activating the complete AI Marketing Team.

## 💬 Example Prompts

```text
Create an image of a futuristic city at night.
```

```text
Edit the futuristic city image and make the sky darker.
```

```text
Find the product hero image from the image database.
```

```text
Write a blog post about AI automation for marketers.
```

## 🔐 Security

**Never commit API keys, access tokens, passwords, or private credentials to GitHub.**

The workflow exports may contain environment-specific IDs and references. Replace these with your own n8n credentials and resources before deploying.

Use environment variables or n8n's credential manager for sensitive configuration.

## 📁 Repository Structure

```text
ai-marketing-team/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── workflows/
│   ├── AI_Marketing_Team.json
│   ├── Create_Image.json
│   ├── Edit_Image.json
│   ├── Search_Images.json
│   └── Faceless_Video.json
│
├── docs/
│   ├── architecture.md
│   ├── setup.md
│   └── workflows.md
│
└── .github/
    └── workflows/
        └── validate-json.yml
```

## ⚠️ Disclaimer

This project consists of **n8n workflow automations** and depends on external services and APIs. You are responsible for configuring the required services, credentials, storage resources, and API access.

## 📄 License

This project is released under the **MIT License**.

## ⭐ Contributing

Contributions and improvements are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Test your n8n workflow changes.
4. Update the documentation if necessary.
5. Submit a pull request.
