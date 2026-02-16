# ai-debate

An AI-powered debate simulator built with [CrewAI](https://www.crewai.com/) that stages structured debates on any topic. The system uses multiple AI agents to propose arguments, oppose them, and judge which side presents the more convincing case—all without human intervention.

## What It Does

**My Debate** runs a three-stage sequential debate:

1. **Propose** — The debater agent argues *in favor* of the motion.
2. **Oppose** — The debater agent argues *against* the motion.
3. **Judge** — A judge agent evaluates both arguments and decides which side is more convincing and why.

Each stage produces structured output that is written to markdown files, giving you a full transcript of the debate.

## Capabilities

| Capability | Description |
|------------|-------------|
| **Custom motions** | Run debates on any topic by changing the `motion` input (e.g., AI regulation, climate policy, tech ethics). |
| **Sequential process** | Tasks run in order: propose → oppose → judge. |
| **Configurable agents** | Agents (debater, judge) are defined in YAML and can be customized for role, goal, and model. |
| **File output** | Arguments and decisions are saved to `output/propose.md`, `output/oppose.md`, and `output/decide.md`. |
| **Verbose mode** | Full reasoning and step-by-step output are visible during execution. |
| **Train** | Train the crew over multiple iterations for improved performance. |
| **Replay** | Replay execution from a specific task for debugging or analysis. |
| **Test** | Run tests with evaluation against an LLM. |
| **Trigger support** | Run the crew with a JSON payload for external integrations. |

## Project Structure

```
my_debate/
├── src/my_debate/
│   ├── config/
│   │   ├── agents.yaml    # Debater & judge agent definitions
│   │   └── tasks.yaml     # Propose, oppose, judge tasks
│   ├── crew.py            # CrewAI crew definition
│   └── main.py            # Entry points (run, train, replay, test)
├── output/                # Debate outputs (propose.md, oppose.md, decide.md)
├── .env                   # API keys (OPENAI_API_KEY, MODEL)
├── pyproject.toml
└── README.md
```

## Requirements

- Python 3.10–3.13
- [OpenAI API key](https://platform.openai.com/api-keys) (used via CrewAI)

## Setup

1. **Clone** the repository and navigate to `3_crew/my_debate`.

2. **Create a virtual environment** and install dependencies:

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   pip install -e .
   ```

3. **Configure environment variables** in `.env`:

   ```env
   OPENAI_API_KEY=your-openai-api-key
   MODEL=gpt-4o-mini
   ```

## Usage

### Run a debate

Default motion: *"There needs to be strict laws to regulate LLMs"*

```bash
run_crew
```

Or call the `run()` function in `main.py` directly.

### Customize the motion

Edit the `inputs` dict in `main.py`:

```python
inputs = {
    'motion': 'Your debate topic here'
}
```

## Example Output

For the motion *"There needs to be strict laws to regulate LLMs"*:

- **Propose** — Arguments for regulation: misinformation, bias, privacy, accountability.
- **Oppose** — Arguments against: stifling innovation, centralization, inflexibility.
- **Judge** — A reasoned decision on which side is more convincing, based on the arguments presented.

Outputs are saved in the `output/` directory.

## Built With

- [CrewAI](https://github.com/joaomdmoura/crewAI) — Framework for orchestrating AI agents
- [OpenAI GPT-4o-mini](https://platform.openai.com/docs/models) — Model used by the agents

## License

MIT
