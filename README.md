# ask-chatgpt

`ask-chatgpt` is a minimal-friction command-line interface (CLI) written in `zsh` for interacting with the OpenAI Chat Completions API (ChatGPT). It allows you to send prompts directly from the terminal, optionally attach files, choose models, and render output nicely with [glow](https://github.com/charmbracelet/glow).

---

## Features

- Send prompts directly via CLI arguments or prompt files.
- Attach local file contents appended to the prompt.
- Choose which OpenAI model to use (default: `gpt-3.5-turbo`).
- List available models from the OpenAI API.
- Optional output rendering using [glow](https://github.com/charmbracelet/glow).
- Verbose mode for debug/info output.
- Robust error handling and minimal dependencies (`curl`, `jq`, `base64`).

---

## Requirements

- `zsh`
- `curl`
- `jq` (for JSON parsing)
- `base64` (standard on most UNIX systems)
- [glow](https://github.com/charmbracelet/glow) (optional, only if using `-g` flag)
- An OpenAI API key set via the environment variable `OPENAI_API_KEY`

---

## Installation

1. Copy the script and save it as `ask-chatgpt`:

```bash
chmod +x ask-chatgpt
```

2. Make sure it is in your `PATH` or invoke it via `./ask-chatgpt`

3. Export your OpenAI API key:

```bash
export OPENAI_API_KEY="your_openai_api_key_here"
```

---

## Usage

```bash
ask-chatgpt [-m <model>] [-g] [-f <file>] [-p <prompt file>] [-v] [-i] <prompt>
```

### Positional Arguments

- `<prompt>`  
  Prompt text to send to the ChatGPT API (can also be omitted if using `-p` or stdin).

### Options

| Option          | Description                                                                                     |
|-----------------|-------------------------------------------------------------------------------------------------|
| `-p <prompt>`   | Read prompt text from a file instead of the command line.                                       |
| `-m <model>`    | Specify the model to use (default: `gpt-3.5-turbo`, or value of `OPENAI_DEFAULT_MODEL`).         |
| `-f <file>`     | Attach a local file whose contents will be appended to the prompt.                              |
| `-g`            | Render output using [glow](https://github.com/charmbracelet/glow) for pretty terminal formatting.|
| `-v`            | Enable verbose output showing diagnostic info on `stderr`.                                     |
| `-i`            | List available models from the OpenAI API and exit.                                            |
| `-h`, `--help`  | Show this help message and exit.                                                               |

---

## Examples

### Basic prompt

```bash
ask-chatgpt "Explain the difference between TCP and UDP."
```

### Read prompt from file

```bash
ask-chatgpt -p my_prompt.txt
```

### Attach a file's contents to the prompt

```bash
ask-chatgpt -f example.txt "Please summarize the attached file and provide key insights."
```

### Choose a model

```bash
ask-chatgpt -m gpt-4 "Generate a poem about the sea."
```

### Pipe large prompt from another program or stdin

```bash
cat large_prompt.txt | ask-chatgpt
```

### List available OpenAI models

```bash
ask-chatgpt -i
```

### Use glow to render Markdown output nicely

```bash
ask-chatgpt -g "Write a sample README in markdown format."
```

---

## Environment Variables

- `OPENAI_API_KEY` **(required)**: Your OpenAI API key.
- `OPENAI_DEFAULT_MODEL`: Default model to use if `-m` is not specified. Defaults to `gpt-3.5-turbo`.

---

## Troubleshooting

- **OPENAI_API_KEY is not set**  
  Make sure to export your API key, e.g.:

  ```bash
  export OPENAI_API_KEY="your_api_key"
  ```

- **File not found error**  
  Ensure the file supplied to `-p` or `-f` exists and is readable.

- **`glow` not found when using `-g` option**  
  Install [glow](https://github.com/charmbracelet/glow) if you want to use pretty Markdown rendering.

- **API errors**  
  Check your API key and network connection. Use `-v` to see verbose output.

---

## License

This script is released under the MIT License. See the LICENSE file for details.

---

## Acknowledgments

Thanks to OpenAI for the Chat Completions API, and to the authors of `jq` and `glow` for essential tools used in this CLI.

---

Enjoy interacting with ChatGPT directly from your terminal! 🚀
