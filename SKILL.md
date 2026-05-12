# Discord Self-Bot Skill

This skill allows the agent to interact with a real Discord account using `discord.py-self` to perform tasks requested by the user.

## Important Rules

1. **NEVER read the user's Discord token.** The token is stored in `.env` under the key `TOKEN`. You must treat this file as strictly confidential and never open, read, or log its contents.
2. **Always prefer `pip3`** when installing Python packages, as it is the default for most users.
3. All temporary self-bot code must be written inside the `sandbox/` folder.
4. After completing the task, you **must delete** all code files written in `sandbox/`.
5. Do not commit or share any code that contains or references the token.

## Workflow

1. **Check Dependency**
   - Before starting, ensure `discord.py-self` is installed:
     ```bash
     pip3 install discord.py-self
     ```
   - If `pip3` is unavailable, fallback to `pip`.

2. **Request Token Setup**
   - Check if `.env` exists in the skill root. If not, ask the user to create it with their Discord token:
     ```
     Please create a `.env` file in the skill directory with the following content:
     TOKEN=your_discord_token_here
     ```
   - **Do not read the `.env` file.** Just check for its existence (e.g., with `ls -a` or `test -f`).

3. **Write Code in `sandbox/`**
   - Create Python scripts inside `sandbox/` to accomplish the user's task.
   - The script should load the token using `python-dotenv` from the parent directory's `.env` file.
   - Example pattern:
     ```python
     import os
     from dotenv import load_dotenv
     import discord

     load_dotenv(os.path.join(os.path.dirname(__file__), '..', '.env'))
     TOKEN = os.getenv('TOKEN')

     client = discord.Client()

     @client.event
     async def on_ready():
         # task logic here
         await client.close()

     client.run(TOKEN)
     ```

4. **Run the Code**
   - Execute the script from the skill root directory:
     ```bash
     pip3 install python-dotenv  # if not already installed
     python3 sandbox/task_script.py
     ```

5. **Cleanup**
   - After the script finishes, delete everything inside `sandbox/`:
     ```bash
     rm -rf sandbox/*
     ```

## Safety Reminders

- Never log, print, or expose the `TOKEN` variable.
- Never read the `.env` file contents.
- Only perform actions the user explicitly requests.
- If the user asks to send messages, ensure they understand it will be sent from their real account.
- Keep scripts minimal and focused on the single requested task.
