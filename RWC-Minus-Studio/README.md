# 🐔 RWC-Minus-Studio
# RWC-Minus-Studio

**RWC-Minus-Studio** is a web application built with Flask that leverages Stable Diffusion models for image generation. It provides endpoints for text-to-image and image-to-image generation, as well as a simple frontend for interaction.

---

## ✨ Features
- 🎨 **Text → Image** generation with style presets (fantasy, cyberpunk, anime, oil painting).  
- 🖼 **Image → Image (Img2Img)** editing and enhancement.  
- 📂 **Upload for training** to collect images for fine-tuning datasets.  
- 🚀 **Google Drive integration** (optional, if running in Colab).  
- 🔒 **API key security** for endpoints.  
- ⚡ Optimized for GPU with FP16 + xformers (when available).  
- 🖥 Built-in cyberpunk web UI with neon theme.  

---

## 📦 Requirements
- Python 3.9+  
- CUDA-capable GPU (recommended, but CPU fallback supported)  
- Hugging Face account + model access (optional for some models)  

Install dependencies:
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install diffusers transformers accelerate scipy
pip install flask flask-cors pydrive2 pillow
```

---

## ⚙️ Configuration

Environment variables:

| Variable           | Default                              | Description                                 |
| ------------------ | ------------------------------------ | ------------------------------------------- |
| `MODEL_ID`         | `Lykon/DreamShaper`                  | Hugging Face model to use                   |
| `HF_TOKEN`         | *(none)*                             | Hugging Face token (if model requires auth) |
| `DEVICE`           | `cuda` if available else `cpu`       | Compute device                              |
| `OUTPUT_DIR`       | `/content/drive/MyDrive/Result`      | Output directory                            |
| `INPUT_DIR`        | `/content/drive/MyDrive/InputImages` | Input directory                             |
| `META_DIR`         | `/content/drive/MyDrive/ResultMeta`  | Metadata directory                          |
| `NGROK_DOMAIN`     | `yourmastertrainai.pagekite.me`      | Custom domain (optional)                    |
| `API_KEY`          | `changeme_local_only`                | API key (must change in production)         |
| `MAX_UPLOAD_BYTES` | `6MB`                                | Upload size limit                           |
| `MAX_CONCURRENT`   | `1`                                  | Concurrent inference limit                  |

---

## ▶️ Running

Start the server:

```bash
python rwc_minus_studio.py
```

By default:

* Flask runs on `http://0.0.0.0:80`
* If `NGROK_DOMAIN` is set, will attempt to tunnel via ngrok.

---

## 🖥 UI Features

* Mode selector (Text→Image, Image→Image, Enhance)
* Prompt + Style dropdown
* Live image preview
* Upload images for dataset building

---

## 🔒 Security Notes

* Change the default `API_KEY` before exposing to public.
* This is **not hardened for production** — intended for research and personal projects.
* Avoid exposing ngrok link without authentication.

---

## 📜 License

MIT License © 2025 RafalW3bCraft

