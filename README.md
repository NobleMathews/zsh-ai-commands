# ZSH AI Commands (with an LLM endpoint)
![zsh-ai-commands-demo](./zsh-ai-commands-demo.gif)

This plugin works by sending a query to any LLM endpoint that uses the openai schema for terminal commands that achieve the described target action.

To use it just type what you want to do (e.g. `list all files in this directory`) and hit the configured hotkey (default: `Ctrl+o`).
When the LLM responds with its suggestions just select the one from the list you want to use.

## Requirements
* [curl](https://curl.se/)
* [fzf](https://github.com/junegunn/fzf)
  * note: you need a recent version of fzf (the apt version for example is fairly old and will not work)
* awk

## Installation

### oh-my-zsh

Clone the repository to you oh-my-zsh custom plugins folder:

``` sh
git clone https://github.com/muePatrick/zsh-ai-commands ${ZSH_CUSTOM:=~/.oh-my-zsh/custom}/plugins/zsh-ai-commands
```

Enable it in your `.zshrc` by adding it to your plugin list:

```
plugins=(... zsh-ai-commands ...)
```

Set keys you want to override:

```
export ZSH_AI_COMMANDS_ENDPOINT="http://swag-gpu:8000"
export ZSH_AI_COMMANDS_LLM_NAME="meta/llama-3.3-70b-instruct"
```

Replace the placeholder with your own key.
The config can be set e.g in your `.zshrc` in this case be careful to not leak the key should you be sharing your config files.

## Configuration Variables

| Variable                                  | Default                                 | Description                                                                                                |
| ----------------------------------------- | --------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `ZSH_AI_COMMANDS_ENDPOINT`                | `https://api.openai.com` | The endpoint to send the request to |
| `ZSH_AI_COMMANDS_API_KEY` | `xyz` | OpenAI API key should be set here if you are not using a setup that ignores the key |
| `ZSH_AI_COMMANDS_HOTKEY` | `'^o'` (Ctrl+o) | Hotkey to trigger the request |
| `ZSH_AI_COMMANDS_LLM_NAME` | `gpt-4o` | LLM name |
| `ZSH_AI_COMMANDS_N_GENERATIONS` | `5` | Number of completions to ask for |
| `ZSH_AI_COMMANDS_EXPLAINER` | `true` | If true, GPT will comment the command |
| `ZSH_AI_COMMANDS_HISTORY` | `false` | If true, save the natural language prompt to the shell history (and atuin if installed) |


## Known Bugs
- [x] Sometimes the commands in the response have to much / unexpected special characters and the string is not preprocessed enough. In this case the fzf list stays empty.
- [ ] The placeholder message, that should be shown while the GPT request is running, is not always shown. For me it only works if `zsh-autosuggestions` is enabled.
