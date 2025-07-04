# AI Content Automation with n8n

---

## Project Overview

This repository contains the workflow for an end-to-end AI-powered automation system designed to generate social media content from idea to finished video. Built from scratch using **n8n**, this system automates the entire content pipeline, making it ready for platforms like YouTube Shorts and Instagram Reels.

The goal of this project was to understand the intricacies of AI content generation by building a custom, highly controllable, and cost-efficient solution, rather than relying solely on commercial tools.

## Features

This AI workflow automates the following steps:

* ✅ **Story/Script Generation:** Leverages **OpenAI** to create compelling narratives.
* ✅ **Text-to-Speech Narration:** Utilizes **ElevenLabs** for high-quality voiceovers.
* ✅ **Scene-Based Breakdown:** **OpenAI** intelligently segments the story into visual scenes.
* ✅ **Visual Generation:** Generates relevant images for each scene using **OpenAI (DALL·E or GPT-4V)**.
* ✅ **Local Media Storage:** Efficiently saves all generated text, audio, and image files to a configurable local directory.
* ✅ **Final Video Creation:** Assembles the media into a ready-to-publish video using **FFmpeg**.
* ✅ **Ready-to-Publish Content:** Outputs content optimized for social media platforms.

## Why Build This?

While powerful AI video tools like Pika, RunwayML, and Veo exist, this custom automation was built to achieve:

* **Custom Scene Control:** Granular control over each visual segment.
* **Voice Consistency:** Maintain a consistent narrative voice throughout.
* **Asset Storage:** Own and manage all generated media assets locally.
* **Cost Efficiency:** Significantly reduce per-content generation costs compared to credit-based models.
* **Full Automation:** Achieve a seamless, automated pipeline from initial input to final output.

## Workflow Breakdown (Built with n8n)

The core of this automation is an n8n workflow that orchestrates various AI APIs and shell commands.

![n8n Workflow Diagram](https://your-image-hosting-service.com/path-to-your-n8n-workflow-screenshot.png)
*Self-hosting your n8n workflow diagram image is recommended.*

**Workflow Steps:**

1.  **Trigger:** Manual execution or scheduled automation.
2.  **Generate Story:** OpenAI prompt for initial content generation.
3.  **Save & Format Story:** Disk write operation and text cleanup.
4.  **Narration:** ElevenLabs API call for voice generation.
5.  **Scene Breakdown:** OpenAI splits the story into visual segments.
6.  **Image Generation:** OpenAI (DALL·E or GPT-4V) creates visuals per scene.
7.  **File Storage:** Stores all generated text, images, and audio locally.
8.  **Final Video Creation:** FFmpeg joins images and narration into a video.
9.  **Acknowledgement/Notification:** Optional logging or alerts upon completion.

## Getting Started

### Prerequisites

* An active **n8n** instance (self-hosted or cloud).
* **OpenAI API Key**
* **ElevenLabs API Key**
* **FFmpeg** installed on the system where your n8n instance runs (and accessible in its PATH).
* **Environment Variable Configuration:** You **must** define an environment variable `N8N_OUTPUT_BASE_PATH` in your n8n instance's `.env` file (or other environment configuration) pointing to the root directory where you want to save all generated content (e.g., `/home/user/ai_generated_content` or `C:\ai_content`).

### Installation & Setup

1.  **Clone this repository:**
    ```bash
    git clone [https://github.com/your-username/ai-content-automation-n8n.git](https://github.com/your-username/ai-content-automation-n8n.git)
    cd ai-content-automation-n8n
    ```
2.  **Import the n8n Workflow:**
    * Open your n8n instance.
    * Go to "Workflows" and click "New" or "Import from file".
    * Import the workflow JSON file: `[Your n8n workflow file name here].json` (e.g., `social_media_content_automation.json`).
3.  **Configure API Credentials:**
    * In n8n, go to "Credentials".
    * **OpenAI:** Add or select an existing "OpenAI API" credential. The workflow uses a placeholder `YOUR_OPENAI_CREDENTIAL_ID` which will prompt you to link your actual credential upon import.
    * **ElevenLabs:** The "Story Narration" (HTTP Request) node requires your ElevenLabs API Key in its `Header Parameters` section (look for `xi-api-key`). Enter your key there.
4.  **Configure Output Paths (via Environment Variable):**
    * Edit your n8n instance's `.env` file (or equivalent).
    * Add the following line, replacing `/path/to/your/desired/output` with your actual desired root directory:
        ```
        N8N_OUTPUT_BASE_PATH=/path/to/your/desired/output
        ```
    * Restart your n8n instance for the environment variable to take effect.
    * The workflow will automatically save JSON files to `N8N_OUTPUT_BASE_PATH/JSON/`, audio to `N8N_OUTPUT_BASE_PATH/audio/`, and images to `N8N_OUTPUT_BASE_PATH/images/`.
5.  **FFmpeg Installation:**
    * Ensure FFmpeg is installed and added to your system's PATH variable on the machine running n8n. You can download it from [ffmpeg.org](https://ffmpeg.org/download.html).

### Usage

1.  **Activate the Workflow:** Set the n8n workflow to "Active" in your n8n instance.
2.  **Trigger the Workflow:** You can manually execute the workflow for testing, or rely on the `Schedule Trigger` node (currently set for 9 PM daily) to automate content generation.
3.  **Monitor Output:** Generated content (scripts, audio, images, and final videos) will be saved to the directories configured via `N8N_OUTPUT_BASE_PATH`.

## Challenges Faced

Building this system involved overcoming several hurdles:

* Navigating dynamic JSON and expression references within n8n.
* Dealing with API delays and failures, implementing robust error handling.
* Precise FFmpeg syntax and managing file paths, especially for diverse operating systems.
* Ensuring webhooks functioned correctly in active workflow states.

## Key Learnings

* **Modular Design:** Break down complex automations into smaller, manageable blocks.
* **Logging & Backups:** Essential for debugging and recovery.
* **Test Flows:** Build and test individual stages before integrating the entire chain.
* **Node Labeling:** Meticulous labeling saves significant debugging time.
* **Minimum Viable Automation:** Start simple and iterate to scale up.

## Potential Use Cases

This system can be adapted for various content creation needs:

* 🎬 AI-narrated children’s stories.
* 💬 Daily motivational video posts.
* 📈 Niche storytelling series (finance, health, productivity).
* ✍️ Repurposing blog posts into short video summaries.
* 🎞️ Building content banks for batch uploading to social platforms.

## Contributing

Feel free to fork this repository, suggest improvements, or open issues. Contributions are welcome!

## License

This project is open-sourced under the [e.g., MIT License].
