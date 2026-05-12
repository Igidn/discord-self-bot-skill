# Discord Self-Bot Skill

An agent skill that enables secure, temporary interaction with a real Discord account using `discord.py-self`.

> [!WARNING]
> Using self-bots violates [Discord's Terms of Service](https://discord.com/terms). This skill is provided for educational and personal automation purposes only. The user assumes all responsibility for how this skill is used.

## Setup

1. **Install the skill** into your agent's skill directory.

2. **Create your `.env` file** in the skill root:
   ```bash
   cp .env.example .env
   ```
   Then edit `.env` and replace `your_discord_token_here` with your actual Discord user token.
   > **Never share your `.env` file or commit it to version control.**

3. **Ensure `discord.py-self` is installed**:
   ```bash
   pip3 install discord.py-self python-dotenv
   ```

## How It Works

When you ask the agent to perform a Discord task (e.g., send a message, fetch guild info):

1. The agent writes a temporary Python script inside the `sandbox/` folder.
2. The script loads your token from `.env` and runs the requested task.
3. After completion, the agent **automatically deletes** all code from `sandbox/`.
4. The agent **never reads or exposes** your token.

## License

MIT
