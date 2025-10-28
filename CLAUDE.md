# GitHub Profile Glow-Up

## Purpose
This project helps users enhance their GitHub profile using the CM5 device. It guides them through:
1. Setting up GitHub authentication via `gh` CLI
2. Creating/updating their profile README with custom animations
3. Adding dynamic content that auto-updates

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
- Can include custom animations (SVG only)
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
When creating animations:
- **Use `algorithmic-art` skill exclusively**
- Output MUST be SVG format (GitHub profiles only support SVG)
- Ask user what style/theme they want
- Preview and iterate until satisfied

**Personalization Strategy:**
- If user provides only colors/vague request, explore their repos to personalize based on interests
- Use `gh repo list USERNAME --limit 20` to see their projects
- Look for patterns: gaming projects → pixel art style, AI/ML → neural network visuals, web dev → modern gradients
- Incorporate tech stack or project themes into the animation concept

**Animation Ideas to Suggest:**
- **Particle systems**: Text emerging from scattered points, great for tech/sci-fi themes
- **Wave/audio visualizers**: Pulsing bars or sine waves, perfect for music/audio projects
- **Geometric patterns**: Rotating shapes, tessellations, fractals for mathematical/algorithmic feel
- **Code rain**: Matrix-style falling characters for cybersecurity/hacker aesthetic
- **Pixel art**: Retro 8-bit style animations for game developers
- **Gradient morphing**: Smooth color transitions for designers/creative developers
- **Network graphs**: Connected nodes for data science/networking themes

**When presenting options:**
Keep it concise but informative. Format: "Style Name - Brief visual description (why it fits)"
Example: "Particle Swarm - Golden points coalescing into text (fits your blockchain projects' decentralized theme)"

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
