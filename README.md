# Commit Oracle

Commit Oracle is a smart Git commit message generator that leverages AI to suggest contextually relevant commit messages based on your staged changes. It integrates seamlessly with your Git workflow and popular tools like [LazyGit](https://github.com/jesseduffield/lazygit).

## Features

- Generates 5+ AI-powered commit messages based on your staged Git changes
- Uses the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) format for structured, consistent messages
- Allows browsing and selection of suggested messages using FZF
- Supports editing of the selected message before committing
- Integrates with LazyGit for a smooth workflow

## Requirements

- [FZF](https://github.com/junegunn/fzf) - fuzzy finder
- [aichat](https://github.com/sigoden/aichat) - CLI tool for interacting with OpenAI's ChatGPT and other LLMs

## Installation

1. Clone this repository:

   ```sh
   git clone https://github.com/tfriedel/commit-oracle.git
   ```

2. Add the script to your PATH. Add this line to your `~/.bashrc` or `~/.zshrc`:

   ```sh
   export PATH=$PATH:/path/to/commit-oracle
   ```

3. Source your updated RC file or restart your terminal.

4. Install [aichat](https://github.com/sigoden/aichat) and [FZF](https://github.com/junegunn/fzf) by following the instructions in the repositories.

## Usage

### Standalone

Run the script in your Git repository after staging your changes:

```sh
commit-oracle.sh
```

### With LazyGit

To use Commit Oracle with LazyGit, add the following to your LazyGit config file (usually located at `~/.config/lazygit/config.yml`):

```yaml
customCommands:
  - key: <c-g>
    description: Pick LLM commit
    loadingText: "waiting for LLM to generate commit messages..."
    command: commit-oracle.sh
    # to use another editor
    # command: export EDITOR=nvim && commit-oracle.sh
    context: files
    subprocess: true
```

Now you can use the `<Ctrl-G>` shortcut in LazyGit to invoke Commit Oracle.

## How It Works

1. The script extracts the diff of staged changes.
2. It sends this diff to an LLM, requesting commit message suggestions.
3. The LLM generates multiple commit messages following the Conventional Commits format.
4. FZF presents these messages for you to browse and select.
5. You can edit the selected message in your preferred text editor.
6. The script commits the changes with your chosen (and possibly edited) message.
   In case you don't save the message, the script will abort the commit.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

The code is heavily based on the script that "deepanchal" posted [here](https://github.com/jesseduffield/lazygit/issues/2579#issuecomment-2161434274).  
This script was based on chhoumann's [template](https://github.com/chhoumann/bunnai/blob/af4b78efa24dce6940bb6576ad3f9f579f995111/src/template.ts).
