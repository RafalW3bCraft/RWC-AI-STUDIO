# 🎮 RWC-AI-Studio | The AI Art Quest

**The ultimate gamified AI image generation platform that transforms art creation into an epic RPG adventure!**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Stable Diffusion](https://img.shields.io/badge/Stable%20Diffusion-1.5-purple.svg)](https://huggingface.co/runwayml/stable-diffusion-v1-5)

---

## 🌟 Overview

RWC-AI-Studio is a revolutionary gamified AI image generation platform that combines the power of Stable Diffusion with engaging RPG mechanics. Level up your artistic journey, unlock legendary styles, earn achievements, and create stunning AI artwork in an immersive gaming environment!

### ✨ Key Features

- 🎮 **RPG Progression System** - Level 1-50 with XP rewards
- 🎨 **Tiered Art Styles** - 20+ styles from Common to Legendary
- 🏅 **Achievement System** - 6+ achievements with bonus XP rewards
- ⚔️ **Quest-Based Generation** - Text Quests & Transform Quests
- 💎 **Player Profile** - Persistent progress tracking and statistics
- 🌐 **Web Interface** - Beautiful gaming UI with real-time updates
- 📱 **Mobile Responsive** - Works perfectly on all devices
- 🔐 **Secure API** - Protected endpoints with authentication
- ☁️ **Cloud Integration** - Google Drive storage and Colab support

---

## 🚀 Quick Start

### Option 1: Google Colab (Recommended)

1. **Open in Colab**: Click the Colab badge above or [open directly](https://colab.research.google.com/)
2. **Upload Notebook**: Upload `RWC_AI_Game.ipynb` to your Colab environment
3. **Set HF Token**: Get your token from [Hugging Face](https://huggingface.co/settings/tokens)
   - Add to Colab Secrets as `HF_TOKEN` (recommended)
   - Or replace `your_hf_token_here` in the code
4. **Run All Cells**: Execute all cells in order
5. **Access Web UI**: Use the generated ngrok URL to access the gaming interface

### Option 2: Local Installation

```bash
# Clone the repository
git clone https://github.com/your-username/rwc-ai-studio.git
cd rwc-ai-studio

# Install dependencies
pip install diffusers transformers accelerate safetensors xformers torch torchvision pillow flask flask-cors pyngrok requests python-dotenv cryptography

# Set environment variables
export HF_TOKEN="your_hf_token_here"
export DEVICE="cuda"  # or "cpu"

# Run the notebook
jupyter notebook RWC_AI_Game.ipynb
```

---

## 🎮 Game Mechanics

### 🏆 Leveling System

- **Levels**: 1-50 with square-root scaling
- **XP Sources**: 
  - Base generation XP (10-200 based on style tier)
  - Step bonus (up to +20 XP)
  - Achievement rewards (50-1000 XP)
- **Formula**: Level = min(50, int((total_xp / 100) ** 0.5) + 1)

### 🎨 Art Style Tiers

| Tier | Unlock Level | Styles | XP Bonus | Examples |
|------|-------------|--------|----------|----------|
| 🔰 **Common** | Level 1 | 7 styles | 25-40 XP | Fantasy, Cyberpunk, Anime |
| ⭐ **Uncommon** | Level 8-14 | 4 styles | 60-90 XP | Pixel Knight, Magic Realism |
| 💎 **Rare** | Level 15-22 | 4 styles | 100-130 XP | Steampunk Fantasy, Void Walker |
| 🔥 **Epic** | Level 25-35 | 3 styles | 180-220 XP | Dragon Forge, Time Weaver |
| 🌟 **Legendary** | Level 45-50 | 2 styles | 400-500 XP | Quantum Dreams, Legendary Fusion |

### 🏅 Achievement System

| Achievement | Condition | XP Reward | Description |
|-------------|-----------|-----------|-------------|
| 🎯 **First Quest** | Generate 1st artwork | 50 XP | Begin your artistic journey |
| 🎨 **Style Explorer** | Try 5 different styles | 100 XP | Discover artistic diversity |
| 🔥 **Epic Collector** | Reach level 25 | 200 XP | Unlock Epic tier styles |
| 🌟 **Legendary Artist** | Reach level 50 | 1000 XP | Master of all artistic forms |
| ⚡ **Speed Demon** | Generate 10 images/session | 150 XP | Rapid creation mastery |
| 🏭 **Master Crafter** | Create 100 total artworks | 500 XP | Prolific artist achievement |

---

## 🖥️ Web Interface

### 🎮 Gaming Dashboard

- **Player HUD**: Level, XP, total artworks, achievements
- **Style Browser**: Visual style selection with tier filtering
- **Quest Modes**: Text-to-image and image-to-image generation
- **Real-time Updates**: Live progress tracking and notifications
- **Achievement Notifications**: Instant feedback for unlocks

### 📱 Mobile Features

- Fully responsive design
- Touch-optimized controls
- Mobile file upload support
- Optimized for portrait and landscape

---

## 🔧 API Reference

### Authentication

All generation endpoints require API key authentication:

```javascript
headers: {
    'X-API-KEY': 'your_api_key_here'
}
```

### Endpoints

#### Get Player Profile
```http
GET /api/player/profile
```

**Response:**
```json
{
    "player_level": 1,
    "total_xp": 0,
    "total_generations": 0,
    "achievements_unlocked": 0,
    "unlocked_styles": [...],
    "achievements": [...]
}
```

#### Get Available Styles
```http
GET /api/styles
```

**Response:**
```json
{
    "styles_by_tier": {
        "common": [...],
        "uncommon": [...],
        "rare": [...],
        "epic": [...],
        "legendary": [...]
    },
    "player_level": 1,
    "total_styles": 20
}
```

#### Generate Text-to-Image
```http
POST /api/generate_text
```

**Request Body:**
```json
{
    "prompt": "a magical floating island",
    "style": "fantasy",
    "negative_prompt": "blurry, low quality",
    "num_inference_steps": 35,
    "guidance_scale": 7.5
}
```

#### Generate Image-to-Image
```http
POST /api/generate_from_upload
```

**Form Data:**
- `file`: Image file (PNG, JPG, etc.)
- `prompt`: Text description
- `style`: Style ID
- `strength`: Transformation strength (0.1-1.0)
- Other parameters same as text generation

---

## 🎯 Usage Examples

### Notebook Generation

```python
# Quick generation example
result = generate_art_quest(
    prompt="a magical floating island with crystal trees",
    style_id="fantasy",
    negative_prompt="blurry, low quality",
    steps=30,
    guidance=7.5
)

if result["success"]:
    display(result["image"])
    print(f"Earned {result['player_progress']['xp_earned']} XP!")
```

### Web Interface

1. **Choose Quest Mode**: Text Quest or Transform Quest
2. **Select Style**: Browse styles by tier and unlock status
3. **Write Prompts**: Describe your artistic vision
4. **Configure Settings**: Steps, guidance, strength (for transforms)
5. **Generate**: Click "Begin Art Quest"
6. **Track Progress**: Watch XP gains and level-ups in real-time

### API Usage

```javascript
// Generate artwork via API
const response = await fetch('/api/generate_text', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'X-API-KEY': 'your_api_key'
    },
    body: JSON.stringify({
        prompt: 'cyberpunk cityscape at night',
        style: 'cyberpunk',
        num_inference_steps: 40,
        guidance_scale: 8.0
    })
});

const result = await response.json();
if (result.success) {
    // Display generated image and update UI
    updatePlayerProgress(result.player_progress);
}
```

---

## ⚙️ Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `HF_TOKEN` | Required | Hugging Face authentication token |
| `MODEL_ID` | `runwayml/stable-diffusion-v1-5` | Stable Diffusion model |
| `DEVICE` | Auto-detect | GPU/CPU device selection |
| `OUTPUT_DIR` | `/content/drive/MyDrive/ArtQuest/Gallery` | Generated images directory |
| `API_KEY` | Auto-generated | API authentication key |
| `MAX_CONCURRENT` | 2 | Maximum concurrent generations |

### Style Customization

Add new styles to `GAMIFIED_STYLE_PRESETS`:

```python
"my-custom-style": {
    "add": "custom art style, unique aesthetics",
    "neg": "generic, boring, plain",
    "tier": "rare",
    "unlock_level": 20,
    "xp_bonus": 150,
    "description": "My unique artistic vision"
}
```

---

## 🔧 Requirements

### System Requirements

- **GPU**: NVIDIA GPU with 4GB+ VRAM (recommended)
- **RAM**: 8GB+ system memory
- **Storage**: 10GB+ free space for models and generations
- **Python**: 3.8 or higher

### Dependencies

```txt
torch>=1.9.0
torchvision>=0.10.0
diffusers>=0.21.0
transformers>=4.21.0
accelerate>=0.12.0
safetensors>=0.3.0
xformers>=0.0.16
pillow>=8.0.0
flask>=2.0.0
flask-cors>=3.0.0
pyngrok>=5.0.0
pydrive2>=1.0.0
requests>=2.25.0
python-dotenv>=0.19.0
cryptography>=3.0.0
```

---

## 🎨 Style Guide

### Common Tier Styles
- **Fantasy**: Epic magical adventures
- **Cyberpunk**: High-tech dystopian futures  
- **Anime**: Japanese animation artistry
- **Photorealistic**: Camera-perfect realism
- **Watercolor**: Gentle flowing paint techniques
- **Pixel Art**: Retro gaming aesthetics
- **Comic Book**: Dynamic superhero action

### Advanced Tier Examples
- **Steampunk Fantasy** (Rare): Victorian magic meets mechanical engineering
- **Dragon Forge** (Epic): Mythical craftsmanship in molten flames
- **Quantum Dreams** (Legendary): Reality-bending interdimensional art

---

## 🤝 Contributing

We welcome contributions!

### Development Setup

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and test thoroughly
4. Submit a pull request with detailed description

### Areas for Contribution

- 🎨 New art styles and presets
- 🏆 Additional achievements and challenges
- 🌐 UI/UX improvements
- 📚 Documentation and tutorials
- 🐛 Bug fixes and optimizations

---

## 📄 License

This project is licensed under the MIT License.

---

## 📞 Support

### FAQ

**Q: Can I run this without a GPU?**
A: Yes, but generation will be much slower. GPU is highly recommended.

**Q: How do I unlock Legendary styles?**
A: Reach level 45-50 by generating lots of artwork and earning XP!

**Q: Can I add custom styles?**
A: Yes! Modify the `GAMIFIED_STYLE_PRESETS` dictionary with your own styles.

**Q: Is my progress saved?**
A: Yes! All player data is automatically saved to Google Drive in Colab.

---

**🎊 Ready to begin your Art Quest adventure? [Open in Colab](https://colab.research.google.com/) and start creating! 🎊**

---

*Made with ❤️ by the RafalW3bCraft & team*
