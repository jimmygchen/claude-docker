# Claude CLI in Docker

This repository provides a minimal setup to run the Claude Code CLI inside a Docker container, with your local files mounted and credentials provided via an `.env` file.

1. Build the docker image with 

```
# minimal setup
docker build -t claude-cli -f Dockerfile.claude .

# or include dev tooling for Lighthouse development
docker build -t claude-cli -f Dockerfile.dev .
```

2. Create a file at `~/.claude_env` with any environment variables or credentials to use with Claude.

3. Add an alias to your `~/.zshrc`, `~/.bashrc` or `~/.profile.`:

````
# Add this line to ~/.zshrc
alias claude='docker run --rm -it \
  -v "$(pwd)":"/home/claude/$(basename "$PWD")" \
  -v "$HOME/.claude.json":/home/claude/.claude.json \
  -v "$HOME/.claude":/home/claude/.claude \
  -w "/home/claude/$(basename "$PWD")" \
  --env-file $HOME/.claude_env \
  claude-cli'

# Reload your shell
source ~/.zshrc
````

4. Usage: from any directory, just run:

```
claude
```

The container will start with your current directory and credentials loaded from `~/.claude_env`.
