# AI Command-Line Assistant (Binary Release)

A lightweight **terminal AI assistant** for Linux/Mac.  
You can pipe logs, configs, or questions directly into an OpenAI-compatible API (e.g. DeepSeek, OpenAI).  

---

## ✨ Features
- Ready-to-use **binary** (no need to compile)
- Reads from **stdin** and/or a config file
- Modes: `explain`, `review`, `troubleshoot`, `auto`
- Concise, actionable outputs with code blocks
- Works with any **OpenAI-compatible API**

---

## 📥 Installation

1. Download the prebuilt binary `ai` from [Releases](./ai).  
2. Copy it into your local bin directory:
   ```bash
   mkdir -p ~/.local/bin
   cp ai ~/.local/bin/
   chmod +x ~/.local/bin/ai


3. Ensure `~/.local/bin` is in your `PATH`:

   ```bash
   echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc
   source ~/.bashrc
   ```

Now you can run `ai` from anywhere.

---

## ⚙️ Configuration

Set the following environment variables (add them to `~/.bashrc` or `~/.zshrc`):

```bash
# DeepSeek example
export AI_API_KEY="dsksk-XXXX"
export AI_API_BASE="https://api.deepseek.com"
export AI_MODEL="deepseek-reasoner"

# OpenAI example
# export AI_API_KEY="sk-XXXX"
# export AI_API_BASE="https://api.openai.com"
# export AI_MODEL="gpt-4o-mini"
```

---

## 🚀 Usage

```bash
ai [options] [question...]
```

### Options

* `-m {explain|review|troubleshoot|auto}` – choose mode (default: auto)
* `-f <file>` – include a file as context
* `-s "<extra>"` – extra system instructions
* `--json` – show raw JSON payload instead of calling API
* `-h` – help

---

## 📚 Examples

**Explain logs**

```bash
journalctl -u nginx -n 100 --no-pager | ai -m explain
```

**Review a config file**

```bash
ai -m review -f /etc/netplan/01-netcfg.yaml "Gateway not applied; please check"
```

**Troubleshoot errors**

```bash
tail -n 200 /var/log/syslog | ai -m troubleshoot "Frequent DNS timeout"
```

**Ask a question**

```bash
ai "Safest way to restart a crash-looping systemd service on Ubuntu?"
```

---

## ⚠️ Notes

* Input from stdin is truncated at **80KB**
* Do not pipe sensitive data (API keys, private certs) into public APIs
* Works with any OpenAI-compatible endpoint (`/chat/completions`)

---
