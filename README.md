# Server Kitty CLI

**Server Kitty** is a context-aware CLI assistant for server management. It integrates with [Shell-GPT (sgpt)](https://github.com/tbckr/sgpt) and OpenRouter models to provide intelligent guidance, server stats, error analysis, and code-base assistance directly from your terminal.

---

## Features

### **Core Features**

* Interactive CLI assistant: `kitty` or `kitty <command>`
* Context-aware AI responses using SGPT or OpenRouter models
* View server stats (`/stats`)
* Track tasks (`/tasks`)
* Check recent system errors (`/errors`)
* Maintain conversation memory (`/memory`)
* 24-hour standup summaries (`/standup`)
* Contextual code & server help with `/look <question>`
* Tip and guidance when running `kitty` with no arguments

### **Customization**

* Stores logs, tasks, and conversation history locally (`~/.kitty_history`, `~/.kitty_tasks`, `~/.kitty_errors`)
* Can read recent terminal commands and outputs (`~/.kitty_terminal_output`)
* `/look` can be extended to include your project files for code-specific advice
* Fully compatible with interactive and single-command CLI usage

---

## Requirements

1. **Python 3.8+**
2. **[Shell-GPT (`sgpt`)](https://github.com/tbckr/sgpt)** installed and configured.

### SGPT Installation Options

**macOS (Homebrew)**

```bash
brew install tbckr/tap/sgpt
```

**Windows (Scoop)**

```powershell
scoop bucket add tbckr https://github.com/tbckr/scoop-bucket.git
scoop install tbckr/sgpt
```

**Using Go**

```bash
go install github.com/tbckr/sgpt/v2/cmd/sgpt@latest
```

### Adding SGPT to PATH

* **macOS/Linux:**
  Ensure the installation directory is in your PATH. For Go installs:

```bash
echo 'export PATH=$PATH:$(go env GOPATH)/bin' >> ~/.bashrc
source ~/.bashrc
```

* **Windows (PowerShell):**
  Add the Scoop or Go bin folder to your system PATH:

```powershell
$env:Path += ";C:\Users\<YourUsername>\scoop\shims"
```

Verify SGPT is available:

```bash
sgpt --help
```

3. **OpenAI API key** (for SGPT):

```bash
export OPENAI_API_KEY="your_openai_api_key"
```

4. **Optional OpenRouter setup** for free models like Qwen Code:

* Sign up at [OpenRouter](https://openrouter.ai/) and get your **API key**.
* Set the environment variable:

```bash
export OPENROUTER_API_KEY="your_openrouter_api_key"
```

* Configure SGPT to use OpenRouter as a model endpoint:

```bash
sgpt configure
# Choose "Custom API" and enter your OpenRouter API key
# Then select a free model like "Qwen-Code-7B"
```

5. Optional: access to system logs (`/var/log/syslog`) for error reporting. Root privileges may be required.

---

## Installation

1. **Download the `kitty` script**:

```bash
wget https://your-repo-link/kitty -O ~/kitty
chmod +x ~/kitty
```

2. **Ensure SGPT is installed and configured** as described above.
3. **Configure OpenRouter (optional)** if you want to use free models like Qwen Code.
4. **Make `kitty` available system-wide (optional)**:

```bash
echo 'export PATH=$HOME:$PATH' >> ~/.bashrc
source ~/.bashrc
```

5. **Persistent environment variables**:

### Bash (`~/.bashrc` or `~/.bash_profile`)

```bash
echo 'export OPENAI_API_KEY="your_openai_api_key"' >> ~/.bashrc
echo 'export OPENROUTER_API_KEY="your_openrouter_api_key"' >> ~/.bashrc
source ~/.bashrc
```

### Zsh (`~/.zshrc`)

```bash
echo 'export OPENAI_API_KEY="your_openai_api_key"' >> ~/.zshrc
echo 'export OPENROUTER_API_KEY="your_openrouter_api_key"' >> ~/.zshrc
source ~/.zshrc
```

### Fish (`~/.config/fish/config.fish`)

```fish
set -Ux OPENAI_API_KEY "your_openai_api_key"
set -Ux OPENROUTER_API_KEY "your_openrouter_api_key"
```

Verify:

```bash
echo $OPENAI_API_KEY
echo $OPENROUTER_API_KEY
```

This ensures Server Kitty can always access SGPT/OpenAI and OpenRouter models.

---

## Usage

### **CLI Mode**

```bash
kitty "Hello Kitty"
kitty standup
kitty /stats
kitty /look why is my deploy failing
kitty /look help me debug main.py
```

* Commands work with or without `/`.
* `/look <question>` provides AI help using recent terminal commands, output, and error logs.
* Running `kitty` with no arguments shows current **server stats** and a tip to use `/help`.

### **Interactive Mode**

```bash
kitty
ServerKitty> /tasks
ServerKitty> /look why is this script failing
ServerKitty> /help
ServerKitty> <press Ctrl+D or type /exit to quit>
```

---

## Files & Storage

* `~/.kitty_history` → conversation history
* `~/.kitty_tasks` → task log
* `~/.kitty_errors` → recent errors
* `~/.kitty_terminal_output` → recent terminal output for context

All paths can be customized in the script.

---

## Customization Options

* **Memory length**: adjust how many previous messages are stored (`view_memory()` reads last 50 messages).
* **Error log location**: change `/var/log/syslog` path in `view_errors()` for your OS.
* **Terminal context**: extend `get_terminal_context()` to include code files or project directories.
* **AI behavior**: prepend instructions in `ai_response()` to make Kitty humorous, formal, or technical.

---

## Contributing

1. Fork the repository
2. Make your changes
3. Submit a pull request

---

## License

MIT License – free to use and modify for personal or educational purposes.

