# 🎓 Academic Research Website — Setup Guide

A personal research website hosted for free on **GitHub Pages**.
No domain purchase needed. Your site will be at `https://yourusername.github.io`.

---

## 📁 Project Structure

```
yourusername.github.io/
│
├── index.html              ← Homepage (paper list + about)
├── style.css               ← All styles (edit colors/fonts here)
├── main.js                 ← Homepage interactions
├── assets/
│   ├── photo.jpg           ← Your profile photo
│   └── cv.pdf              ← Your CV (optional)
│
└── papers/
    ├── paper-1/
    │   ├── index.html      ← Paper detail page (COPY THIS for each paper)
    │   ├── paper.pdf       ← The actual PDF
    │   ├── infographic-1.png
    │   ├── infographic-2.png
    │   ├── slides.pptx     ← Optional direct download
    │   └── sim.html        ← Optional self-contained sim
    ├── paper-2/
    │   └── index.html
    └── paper-3/
        └── index.html
```

---

## 🚀 Step 1 — Create Your GitHub Repository

1. Go to [github.com](https://github.com) and sign in (or create a free account)
2. Click **New repository**
3. Name it **exactly**: `yourusername.github.io`
   (replace `yourusername` with your actual GitHub username — this is critical)
4. Set it to **Public**
5. Click **Create repository**

---

## 📤 Step 2 — Upload Your Files

**Option A — Browser (easiest):**
1. Open your new repo on GitHub
2. Click **Add file → Upload files**
3. Drag and drop all your files/folders
4. Click **Commit changes**

**Option B — Git (recommended for ongoing updates):**
```bash
git clone https://github.com/yourusername/yourusername.github.io
# Copy all files into this folder
git add .
git commit -m "Initial site launch"
git push origin main
```

---

## ⚙️ Step 3 — Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages** (left sidebar)
2. Under **Source**, select **Deploy from a branch**
3. Select branch: **main**, folder: **/ (root)**
4. Click **Save**
5. Wait ~2 minutes, then visit: `https://yourusername.github.io` 🎉

---

## ✏️ Step 4 — Personalize the Homepage

Open `index.html` and replace:

| Placeholder | Replace with |
|---|---|
| `Dr. Your Name` | Your name |
| `YourName.` (nav logo) | Your name |
| `you@university.edu` | Your email |
| `Researcher · Engineer · Scientist` | Your roles |
| `[your research area]` | Your field |
| `University / Lab Name` | Your institution |
| Paper card content | Your actual papers |

---

## 📄 Step 5 — Add Each Paper

For each paper:

1. **Copy** the `papers/paper-1/` folder and rename it (e.g. `papers/my-2024-paper/`)
2. **Place files** in the folder:
   - `paper.pdf` — your PDF
   - `infographic-1.png`, `infographic-2.png`, etc.
   - `slides.pptx` (optional)
3. **Edit** `index.html` in that folder:
   - Update title, authors, year, venue, abstract
   - Set the correct `src` paths for your files
4. **Add a card** on the homepage `index.html` linking to this folder

---

## 🎬 Embedding Videos (YouTube / NotebookLM)

1. Upload your NotebookLM audio/video to YouTube (or use any YouTube video)
2. In the paper's `index.html`, find the video `<iframe>` and replace `VIDEO_ID_HERE`:

```html
src="https://www.youtube.com/embed/dQw4w9WgXcQ"
```

---

## ⚙️ Embedding OpenAI Gym Simulations

The cleanest free approach uses **Hugging Face Spaces**:

1. Create a free account at [huggingface.co](https://huggingface.co)
2. Click **New Space** → choose **Gradio** app type
3. Create a simple Gradio app that runs your Gym environment:

```python
# app.py (example)
import gradio as gr
import gymnasium as gym
import numpy as np
from PIL import Image

def run_step(action):
    env = gym.make("CartPole-v1", render_mode="rgb_array")
    obs, _ = env.reset()
    obs, reward, done, _, _ = env.step(int(action))
    frame = env.render()
    env.close()
    return Image.fromarray(frame), float(reward)

demo = gr.Interface(fn=run_step, inputs=gr.Slider(0,1,step=1), outputs=["image","number"])
demo.launch()
```

4. Once deployed, embed in your paper page:

```html
<iframe src="https://huggingface.co/spaces/yourname/yourspace?embed=true" ...>
```

---

## 🎨 Customizing Colors

Edit the `:root` block at the top of `style.css`:

```css
:root {
  --bg:      #0a0b0e;   /* main background */
  --accent:  #5b8cff;   /* highlight color — change this to your color */
  --accent2: #c084fc;   /* secondary accent */
  --accent3: #34d399;   /* green accent */
}
```

---

## 📬 Custom Domain (Optional, Free with Cloudflare)

If you later want a custom domain like `yourname.com`:
1. Buy a domain (~$10/yr on Namecheap or Cloudflare)
2. In GitHub Pages settings → **Custom domain** → enter your domain
3. Add a `CNAME` DNS record pointing to `yourusername.github.io`

---

## 🔄 Updating the Site

Every time you push to the `main` branch, GitHub automatically rebuilds the site within ~30 seconds.

```bash
git add .
git commit -m "Add paper-2 with infographics"
git push
```

---

*Built with plain HTML/CSS/JS · Hosted free on GitHub Pages*
