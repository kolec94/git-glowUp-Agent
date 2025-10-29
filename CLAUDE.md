# GitHub Profile Glow-Up

## Purpose
This project helps users enhance their GitHub profile using the CM5 device. It guides them through:
1. Setting up GitHub authentication via `gh` CLI
2. Creating/updating their profile README with custom animations
3. Adding dynamic content that auto-updates

## Important Notes
**File Generation:** The `algorithmic-art` skill generates files in its skill directory, NOT `/tmp`. When using the skill, explicitly save generated files to `/tmp` for iterative development.

## Environment Setup
**ALWAYS create venv first:**
```bash
uv venv && source .venv/bin/activate
uv pip install pillow numpy
```

**Verify gifsicle is installed:**
```bash
gifsicle --version || sudo apt install -y gifsicle
```

## Workflow

### 1. GitHub Authentication
**ALWAYS start by checking if gh CLI is installed:**
```bash
gh --version
```

**If gh is not installed:**
```bash
sudo apt install gh
```

**Then check authentication status:**
```bash
gh auth status
```

If not authenticated, use the `gh-cli` skill to guide setup:
- Run `gh auth login` in background
- Extract the device code and verification URL from output
- Present code and link clearly to user
- Wait for confirmation before proceeding
- Also configure git with: `gh auth setup-git`

### 2. Profile README Setup
Check if user has a profile README:
```bash
gh repo view USERNAME/USERNAME
```

**If README exists:** Read it, show user, ask if they want changes.

**If no README:** Explain profile README benefits:
- Appears at top of profile page
- Can include custom animations (GIF format)
- Can display dynamic content

Let user choose what to add:
- Custom animation (use `algorithmic-art` skill for SVG)
- Stats/badges
- Project showcase
- Dynamic content (see below)

**CRITICAL - First-Time Setup:**
If this is the FIRST TIME creating the profile README repository, after pushing changes, you MUST:
1. Provide the user with the repo URL: `https://github.com/USERNAME/USERNAME`
2. Instruct them to click the **"Share to Profile"** button on the repo page
3. Explain that without this manual step, the README will NOT display on their profile
4. This is a one-time GitHub requirement for new profile READMEs

### 3. Custom Animations

**Workflow:**
1. Use `algorithmic-art` skill → generates HTML + philosophy (save to `/tmp`)
2. Immediately convert to GIF: 1200×600px, 150 frames, 5s
3. User sees GIF only (headless - cannot view HTML)
4. Iterate by editing `/tmp` files, regenerate GIF

**GIF Generation:**
```python
# Specs
CANVAS_WIDTH, CANVAS_HEIGHT = 1200, 600
FRAMES, FPS = 150, 30

# Save with optimization
frames[0].save("output.gif", save_all=True, append_images=frames[1:],
               duration=33, loop=0, optimize=True)

# Post-process
os.system("gifsicle -O3 --colors 128 output.gif -o output.gif")
```

**Personalization:** Check user repos first: `gh repo list USERNAME --limit 20`. Match animations to tech stack/interests (e.g., signal processing → wave patterns, AI/ML → neural networks, gaming → pixel art).

**Animation Ideas:** Particle systems, wave visualizers, geometric patterns, code rain, gradient morphing, network graphs.

### 4. Dynamic Content Ideas
Ask if they want auto-updating content:
- HackerNews trending articles (use `web-automation` skill)
- Trending repos in their top languages (use GitHub API via `gh-cli`)
- Custom web scrapers (use `playwright` skill for complex cases)

**Note:** Don't implement automation scheduling yet - focus on content generation.

## Guidelines
- Assume user is non-technical - explain each step clearly
- Always show what you're doing and why
- Use skills for specialized tasks:
  - `gh-cli` for all GitHub operations
  - `algorithmic-art` for SVG animations
  - `web-automation` or `playwright` for web scraping
- Keep explanations brief but friendly
- Preview changes before committing to GitHub
