# N8n YouTube/Reel Content Generation Agent

This N8n workflow automates the creation of various assets for short-form video content (like YouTube Shorts or Instagram Reels) based on a simple text prompt. It generates a script, converts it to speech, creates captions, generates relevant AI images and videos, and finds stock footage.

**Workflow Visualization:**

(Consider adding a screenshot of your N8n workflow here)

## Features

*   **Input:** Takes a simple text prompt describing the video idea via an N8n Form Trigger.
*   **Script Generation:** Uses an AI language model (OpenRouter - Qwen) to write a short, engaging script (~50-70 words).
*   **Text-to-Speech (TTS):** Converts the generated script into an audio file (`.wav`) using a local TTS service.
*   **Caption Generation:** Creates subtitle (`.srt`) files based on the script using a local captioning service.
*   **Image/Video Prompt Generation:** Uses an AI language model (OpenRouter - Qwen VL) to create concise prompts suitable for generating visuals based on the script.
*   **AI Image Generation:** Generates an AI image using the Google Gemini API based on the derived prompt.
*   **AI Video Generation:** Generates a short AI video clip using a Hugging Face Space API (ZeroScope v2) based on the derived prompt.
*   **Stock Video Search:** Searches Pexels for relevant stock videos based on the derived prompt.
*   **File Organization:** Creates a unique folder for each execution using the execution ID to store all generated assets.
*   **Outputs:** Saves the script (`.txt`), speech audio (`.wav`), captions (`.srt`), AI image (`.png`), AI video (`.mp4`), and downloaded stock videos (`.mp4`) locally where N8n has write access.


## Workflow Breakdown

1.  **Input & Setup:** Form Trigger receives the prompt, Execute Command creates a unique output folder.
2.  **Scripting:** OpenRouter LLM generates the script based on the prompt.
3.  **Local Asset Generation:**
    *   The script is saved as `.txt`.
    *   The script is sent to the local TTS service to create `.wav` audio.
    *   The script is sent to the local SRT service to create `.srt` captions.
4.  **Visual Prompting:** Another OpenRouter LLM (VL model) creates short prompts for visual generation from the script.
5.  **API Asset Generation:**
    *   **AI Image:** Google Gemini API is called to create a `.png` image.
    *   **AI Video:** Hugging Face API is called to create and download an `.mp4` video.
    *   **Stock Video:** Pexels API is searched, and the first relevant `.mp4` video is downloaded.
6.  **Saving:** All downloaded/generated binary files (audio, image, videos) are saved to the execution-specific folder.

