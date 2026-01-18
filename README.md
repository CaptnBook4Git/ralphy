# Ralphy Wiggum Loop 🔄
### The Autonomous AI Coding Agent for Claude Code, OpenCode & Antigravity

**Ralphy** is a powerful shell wrapper and autonomous loop designed to turn CLI-based AI coding tools into fully autonomous software engineers. It enables **Claude Code**, **OpenCode**, and **CCS** to work in a continuous "Ralph Wiggum" loop: Plan, Code, Test, Document, and Commit - over and over again until the job is done.

> *"I'm helping!"* — Ralphy Wiggum

---

## 🚀 Key Features

*   **Autonomous Coding Loop**: Runs continuously to implement features from a PRD.
*   **Multi-Provider Support**: Works seamlessly with:
    *   **Claude Code** (Anthropic)
    *   **OpenCode CLI** (Antigravity, Gemini 3 Pro, Claude Opus 4.5)
    *   **CCS** (Claude Code Switch - GLM, DeepSeek, etc.)
*   **Institutional Memory**: Maintains a `progress.txt` and `important-perceptions.md` to prevent repetitive mistakes and context rot.
*   **Self-Healing**: Runs tests (`flutter test`, `npm test`, etc.) and fixes errors automatically before committing.
*   **SEO Optimized Workflow**: Designed for developers searching for "OpenCode Ralph Wiggum Loop", "Antigravity Ralph Wiggum", or "Claude Code Autonomous Agent".
*   **Thinking Mode Support**: Native support for "Thinking" models like Claude 3.7 Sonnet, Gemini 2.5 Flash Thinking, and GLM-4-Thinking.

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

---

## 📖 Usage

### Initializing a Project
Go to any project folder and run `ralphy`. If no configuration is found, Ralphy will offer to initialize it for you with templates (`.ralphy/prd.json`, `.ralphy/progress.txt`, etc.).

```bash
cd my-new-project
ralphy
```

### Running the Loop

**Standard Mode (Claude Code Default):**
```bash
ralphy              # Run 10 iterations using default Claude Code
ralphy 20           # Run 20 iterations
```

**OpenCode / Antigravity Mode:**
Perfect for using **Gemini 3 Pro** or **Claude Opus 4.5** via Antigravity.

```bash
ralphy --oc-gemini 15       # OpenCode + Gemini 3 Pro (15 iterations)
ralphy --oc-gemini-low 15   # OpenCode + Gemini 3 Pro (Low Thinking)
ralphy --oc-agy 10          # OpenCode + Antigravity Claude Sonnet 4.5
ralphy --oc-agy-opus 5      # OpenCode + Antigravity Claude Opus 4.5 (Thinking)
```

**CCS (Claude Code Switch) Mode:**
Use cheaper or specialized models via CCS.

```bash
ralphy --ccs-glm 50         # GLM 4.6 (Cost effective for overnight loops)
ralphy --ccs-glmt 10        # GLM 4.6 + Thinking
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

### Supported CLI Tools

*   **Claude Code**: The official Anthropic CLI.
*   **OpenCode**: Access Google's Antigravity models and others directly from the terminal.
*   **CCS**: Use any OpenAI-compatible API (DeepSeek, Qwen, GLM, etc.) with the Claude Code interface.

---

## 📁 Configuration

Ralphy relies on a `.ralphy/` folder in your project root:

*   `.ralphy/prd.json`: Your product requirements database (JSON format).
*   `.ralphy/progress.txt`: A chronological log of all changes made by the agent.
*   `.ralphy/RALPHY_PROMPT.md`: The system prompt used for the loop (customizable).
*   `.ralphy/important-perceptions.md`: A "Do's and Don'ts" file that the agent updates itself to learn from mistakes.

---

## 🤖 Keywords & SEO

*   **OpenCode Ralph Wiggum Loop**: Run autonomous loops with OpenCode CLI.
*   **Antigravity Ralph Wiggum**: Leverage Antigravity models for continuous coding.
*   **Claude Code CCS Ralph**: Use CCS to switch providers in a Ralph Wiggum loop.
*   **Autonomous Coding Agent**: Turn your terminal into an autonomous software engineer.
*   **Gemini 3 Pro Coding Loop**: Use the latest Gemini models for sustained development.

---

## 📄 License

MIT License. Feel free to modify and distribute.
