# 🎨 RWC-AI-STUDIO

### Advanced AI Image Generation & Editing Studio for Google Colab

RWC-AI-STUDIO is a powerful and versatile tool built on Google Colab, designed for advanced AI image generation and editing. It provides a web-based interface for easy interaction and leverages popular diffusion models to create and modify images based on text prompts.

## ✨ Features

- **Text-to-Image Generation:** Create images from detailed text descriptions.
- **Image-to-Image Editing & Enhancement:** Transform existing images based on prompts and control the strength of the transformation.
- **Image Regeneration with Specific Modifications:** Modify specific aspects of previously generated or uploaded images.
- **Multiple AI Models:**
    - **DreamShaper:** Versatile model for artistic and realistic images.
    - **Dreamlike:** Ethereal and artistic image generation.
    - **RunwayML:** Standard Stable Diffusion model.
    - **Realistic Vision:** Photorealistic image generation.
- **Style Presets:** Apply predefined styles like Photorealistic, Digital Art, Anime, Fantasy, and Cyberpunk.
- **Advanced Settings:** Fine-tune generation with control over steps, guidance scale, and seed.
- **Google Drive Integration:** Automatically save generated images and their metadata to your Google Drive.
- **Public Access via ngrok:** Expose your Colab environment to the internet for easy access from any device.
- **Web Interface:** A user-friendly web interface for interacting with the studio.

## 🚀 Quick Start

1. **Open the notebook in Google Colab.**
2. **Run all the cells in sequential order.**
    - The first cell installs the necessary packages.
    - The subsequent cells define the core functions, Flask API, web interface, and launch the server.
3. **Access the web interface:** Once the server launch cell finishes execution, it will provide a public URL via ngrok. Click on this URL to open the RWC-AI-STUDIO web interface in your browser.
4. **Start Generating/Editing:** Use the web interface to select a generation mode (Text → Image, Image → Image, or Regenerate), enter your prompts and settings, and generate images.

## 🔧 Advanced Usage

### API Endpoints

The RWC-AI-STUDIO provides a RESTful API for programmatic access. All API endpoints require an `X-API-Key` header or `api_key` query parameter with the value `rwc-ai-studio-2025` (or the value you set in the `main_code` cell).

- `POST /generate/text2img`: Generate image from text prompt.
    - **Request Body (JSON):** `prompt`, `negative_prompt` (optional), `model` (optional, default: `dreamshaper`), `style` (optional), `width` (optional, default: 512), `height` (optional, default: 512), `steps` (optional, default: 20), `guidance_scale` (optional, default: 7.5), `seed` (optional).
- `POST /generate/img2img`: Transform existing image.
    - **Request Body (Multipart Form Data or JSON):** `image` (file upload or `image_url`), `prompt`, `negative_prompt` (optional), `model` (optional, default: `dreamshaper`), `style` (optional), `strength` (optional, default: 0.7), `steps` (optional, default: 20), `guidance_scale` (optional, default: 7.5), `seed` (optional).
- `POST /regenerate`: Regenerate image with modifications.
    - **Request Body (Multipart Form Data or JSON):** `image` (file upload or `image_url` or `image_id`), `modification_prompt`, `model` (optional, default: `dreamshaper`), `strength` (optional, default: 0.5), `steps` (optional, default: 15), `guidance_scale` (optional, default: 7.0), `seed` (optional).
- `GET /gallery`: List all generated images.
- `GET /models`: Get information about available models and settings.
- `GET /health`: Health check endpoint.
- `GET /image/<image_id>`: Serve a specific generated image.
- `GET /metadata/<image_id>`: Get metadata for a specific image.

### Configuration

You can modify the `main_code` cell to change various configurations, including:

- `BASE_DIR`: Change the base directory for saving files in Google Drive.
- `DEFAULT_MODEL`: Set a different default AI model.
- `API_KEY`: Change the API key for accessing the API endpoints.
- `HF_TOKEN`: Update your Hugging Face token for accessing gated models.
- `NGROK_TOKEN`: Provide your ngrok authentication token for stable public URLs.
- `MAX_CONCURRENT_GENERATIONS`: Limit the number of concurrent image generation tasks.
- `MODEL_CONFIGS`: Add or remove AI models.
- `STYLE_PRESETS`: Define or modify style presets.
- `GENERATION_MODES`: Adjust default settings for different generation modes.

### Google Drive Integration

The studio automatically saves generated images and their metadata to your Google Drive in the specified `BASE_DIR`. Ensure Google Drive is mounted correctly in Colab for this feature to work.

### ngrok Public Access

The server launch cell sets up an ngrok tunnel to provide a public URL. This allows you to access the web interface and API from outside your Colab environment. If you have an ngrok auth token, provide it in the `NGROK_TOKEN` environment variable or directly in the `main_code` cell for a more stable URL.

## 🆘 Troubleshooting

- **CUDA Out of Memory:** If you encounter CUDA out of memory errors, try reducing the image size, lowering the `steps` count, or reducing `MAX_CONCURRENT_GENERATIONS`. Ensure no other GPU-intensive processes are running.
- **Model Loading Failed:** Check your internet connection and ensure you have the necessary permissions to access the specified models on Hugging Face (if using gated models).
- **Slow Generation:** Image generation, especially at higher resolutions and step counts, can take time. This is normal behavior.
- **API Key Issues:** Double-check that you are including the `X-API-Key` header or `api_key` query parameter with the correct value in your API requests.


---

**🎉 Enjoy creating amazing AI art with RafalW3bCraft**
