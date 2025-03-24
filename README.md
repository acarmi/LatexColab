# LatexColab - Collaborative LaTeX Agent

<div align="left">
  <img src="assets/LC1.png" alt="LatexColab Logo" width="400">
  <img src="assets/LC3.png" alt="LatexColab Logo" width="400">>
</div>

## Overview

LatexColab is a powerful tool that enables real-time collaboration with AI reasoning agents directly in your LaTeX documents. It maintains bidirectional synchronization between your local LaTeX files and Overleaf repositories, ensuring your work is always backed up and available.

<div align="center">
  <img src="assets/Jellyfish.gif" alt="LatexColab Animation" width="400">
</div>

## Features

- 🧠 **In-document AI collaboration**: Interact with AI models (Claude, GPT-4, etc.) directly from your LaTeX documents
- 🔄 **Bidirectional sync**: Changes made locally or on Overleaf are automatically synchronized
- 🛡️ **Fail-safe workflow**: Works with separate local and repository files to prevent data loss
- 📊 **Visual logging**: Monitor synchronization and agent activity through a clean interface
- 🧩 **Model flexibility**: Use any LLM supported by OpenRouter
- 🔍 **Reasoning transparency**: See both the reasoning process and final answer from AI models

## How It Works

LatexColab bridges the gap between your local LaTeX editor and Overleaf, while adding powerful AI assistance capabilities:

1. You maintain a local LaTeX file separate from the git repository
2. The agent monitors changes to your local file
3. When changes are detected, they are pushed to the Overleaf repository
4. When you engage the AI agent in your document, it responds directly in your LaTeX file
5. All changes are synchronized bidirectionally

## Getting Started

### Prerequisites

- Python 3.7+
- Git
- LaTeX installation
- Overleaf account with API access

### Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/latexcolab.git
cd latexcolab
```

2. Install the required dependencies:
```bash
pip install -r requirements.txt
```

3. Set up your API keys in `set_api_keys.py`:
```python
OPENROUTER_API_KEY = "your_openrouter_api_key"
```

### Usage

The basic usage is simple:

```bash
./lc path/to/your/local_file.tex
```

To engage the AI agent, add a user environment to your LaTeX document:

```latex
\begin{user}
What is the significance of Euler's identity in mathematics?
%parameters: model=claude-3.7-sonnet, status=start
\end{user}
```

The 'model' parameter may be any of the models supported by Openrouter. An illustrative list of models may be found in [LLM_models.py](LLM_models.py).
Once saved, any changes in the local latex file are picked by the agent. The response would then be streamed/embedded within new 'reasoning' and 'answer' environments. Changes made remotely on the Overleaf server are pulled every 10 seconds to the local git repository (may be tweaked in AgenticLatexGitPush.py)
which may postpone the agent response. Any of these processes are logged and may be viewed in the logger window.

The agent will process your query and respond with:

```latex
\begin{reasoning}
[The agent's step-by-step reasoning process will appear here]
\end{reasoning}

\begin{answer}
[The agent's final, concise answer will appear here]
\end{answer}
```

During the reasoning phase the 'status' parameter would shift from 'start' to 'reasoning_<timestamp>_<id>' and finally 'completed_<timestamp>_<id>'.


## Latex Template Examples

See [LatexProjects/template.tex](LatexProjects/template.tex), and an example remote/local project under [LatexProjects/Example].

## PDF Viewer Examples

<div align="center">
  <table>
    <tr>
      <td align="center" width="33%">
        <a href="assets/sc1.png" target="_blank">
          <img src="assets/sc1.png" alt="Compiled main.pdf" width="100%">
          <br>
          <em>Compiled main.pdf</em>
        </a>
      </td>
      <td align="center" width="33%">
        <a href="assets/sc2.png" target="_blank">
          <img src="assets/sc2.png" alt="Local main.tex" width="100%">
          <br>
          <em>Local main.tex</em>
        </a>
      </td>
      <td align="center" width="33%">
        <a href="assets/sc3.png" target="_blank">
          <img src="assets/sc3.png" alt="Overleaf main.tex" width="100%">
          <br>
          <em>Overleaf main.tex</em>
        </a>
      </td>
    </tr>
  </table>
  <p><em>Click any image to view full size</em></p>
</div>

## Configuration

Edit the `lc` script to configure:

- Your Overleaf git URL
- Git credentials
- Local repository path
- Other sync parameters

For detailed instructions on obtaining Overleaf credentials, see [Overleaf_git_access.md](Overleaf_git_access.md).

## Supported Models

Any model available through OpenRouter can be used, including:

- `claude-3.7-sonnet` - Anthropic's Claude 
- `o1`, `o3-mini-high`  - OpenAI
- `deepseek-r1`

## Advanced Features

### Local Compilation

The agent can automatically compile your LaTeX documents locally:

```bash
./lc path/to/your/file.tex --local-compile --open-pdf
```

### Package Management

LatexColab can automatically install missing LaTeX packages:

```bash
./lc path/to/your/file.tex --auto-install-packages
```

## Troubleshooting

### Git Issues

If you encounter git synchronization problems:
- Ensure your Overleaf API token is correct
- Check if you have write permissions to the repository
- Verify your network connection

### Agent Not Responding

If the agent isn't responding to your queries:
- Make sure you included `status=start` in your parameters
- Check that your OpenRouter API key is valid
- Verify the model name is correct

## License

## Acknowledgments

- The Anthropic Claude team for their advanced LLM capabilities
- The Overleaf team for their excellent LaTeX collaboration platform