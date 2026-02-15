# Ralphy Wiggum Loop 🔄
### The Autonomous AI Coding Agent for OpenCode

**Ralphy** is a powerful shell wrapper and autonomous loop designed to turn OpenCode CLI into a fully autonomous software engineer. It enables continuous "Ralph Wiggum" loops: Plan, Code, Test, Document, and Commit - over and over again until the job is done.

> *"I'm helping!"* — Ralphy Wiggum

---

## 🚀 Key Features

*   **Autonomous Coding Loop**: Runs continuously to implement features from a PRD.
*   **Any Model via OpenCode**: Use any model available through `opencode models` — GPT-5.2, Gemini 3 Pro, Claude Opus 4.5, GLM 4.7, and many more.
*   **Institutional Memory**: Maintains a `progress.txt` and `important-perceptions.md` to prevent repetitive mistakes and context rot.
*   **Self-Healing**: Runs tests (`flutter test`, `npm test`, etc.) and fixes errors automatically before committing.
*   **GH-Issues Workflow**: Create PRDs directly from GitHub Issues and let agents work through them automatically.
*   **Dynamic Model & Agent Selection**: Interactive menus for choosing models and agents at runtime.

---

## 🛠️ Installation

1.  **Clone the Repository** (or download the source):
    ```bash
    git clone https://github.com/CaptnBook4Git/ralphy.git ~/Code/ralphy
    ```

2.  **Add to PATH**:
    Add the following line to your `~/.bashrc` or `~/.zshrc`:
    ```bash
    export PATH="$HOME/Code/ralphy/bin:$PATH"
    ```

3.  **Reload Shell**:
    ```bash
    source ~/.bashrc
    ```

4.  **Verify Installation**:
    ```bash
    ralphy --version
    ```

5.  **Prerequisites**: [OpenCode CLI](https://opencode.ai) must be installed:
    ```bash
    curl -fsSL https://opencode.ai/install | bash
    ```

---

## 📖 Usage

### Initializing a Project
Go to any project folder and run `ralphy`. If no configuration is found, Ralphy will offer to initialize it for you with templates (`.ralphy/prd.json`, `.ralphy/progress.txt`, etc.).

```bash
cd my-new-project
ralphy
```

### Running the Loop

```bash
ralphy              # Run 10 iterations (default model: gpt-5.2)
ralphy 20           # Run 20 iterations
ralphy -m google/antigravity-gemini-3-pro 15   # Gemini 3 Pro, 15 iterations
ralphy -m zai-coding-plan/glm-4.7 50          # GLM 4.7, 50 iterations
```

### Choosing a Model

Use `-m` / `--model` to select any model available via OpenCode:

```bash
ralphy -m github-copilot/gpt-5.2          # GPT-5.2 (default)
ralphy -m google/antigravity-gemini-3-pro  # Gemini 3 Pro via Antigravity
ralphy -m google/antigravity-claude-opus-4-5-thinking  # Claude Opus 4.5
ralphy -m cerebras/zai-glm-4.7            # GLM 4.7 via Cerebras
ralphy --list                              # Show all available models
```

### GH-Issues Workflow

```bash
ralphy create-prd --gh-issues              # Create PRD from all open GitHub Issues
ralphy create-prd --gh-issues 1,3,5        # Only specific issues
ralphy 10                                   # Loop starts, auto-detects GH-Issues
```

### Bugfix Mode

```bash
ralphy --bugfix 10    # Use bugs.json instead of prd.json
```

---

## 🧠 How It Works

Ralphy enforces a strict disciplined workflow for the AI agent:

1.  **Read Context**: Loads `prd.json` (what to do), `progress.txt` (what was done), and `important-perceptions.md` (what not to forget).
2.  **Pick Task**: Selects the highest priority item from the PRD that hasn't passed yet.
3.  **Implement**: Writes code, creates files, refactors.
4.  **Verify**: Runs the project's build and test commands (e.g., `flutter test`).
5.  **Document**: Updates the progress log and marks the item as passed in the PRD.
6.  **Commit**: Creates a clean git commit.
7.  **Repeat**: Starts the next iteration.

---

## 📁 Configuration

Ralphy relies on a `.ralphy/` folder in your project root:

*   `.ralphy/prd.json`: Your product requirements database (JSON format).
*   `.ralphy/progress.txt`: A chronological log of all changes made by the agent.
*   `.ralphy/RALPHY_PROMPT.md`: The system prompt used for the loop (customizable).
*   `.ralphy/important-perceptions.md`: A "Do's and Don'ts" file that the agent updates itself to learn from mistakes.

### OpenCode Agents

Ralphy ships custom OpenCode agents in `templates/opencode-agents/`. To use them, symlink them into your OpenCode agent config:

```bash
ln -sf ~/Code/ralphy/templates/opencode-agents/selector.md ~/.config/opencode/agent/selector.md
```

*   **selector**: Intelligent task selector that analyzes PRD, progress, and codebase to pick the strategically best next issue. Automatically prioritizes unfinished tasks (started but not completed).

---

## 🌿 Feature-Branch Detection

When running on a feature branch (not `main`/`master`), Ralphy automatically:

1. Detects unfinished tasks from `progress.txt` (started but not completed).
2. Instructs the Selector Agent to prioritize resuming that work.
3. Prevents starting new tasks while previous work is incomplete.

---

## 📄 License

MIT License. Feel free to modify and distribute.
