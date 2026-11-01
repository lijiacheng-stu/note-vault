context window：claude的记忆能够容纳的空间。

What Happens When Context Fills Up？
- the context window is automatically **compacted**.

命令：
- /context
- /compact: It's handy when you want to free up context space while keeping a memory of what you previously worked on.
- `/clear`:when you want to start a new feature. You don't want the previous conversation to introduce bias into something new.For things you want Claude to remember across sessions, put them in your CLAUDE.md file so it doesn't have to rediscover things from scratch.
	- CLAUDE.md


节省空间的技巧：
- be specific with your prompts
- **Manage your MCP servers.**
	- a connected MCP server loads only its tool names and instructions into context, and Claude loads a tool's full details when it needs that tool.
	- Each server still takes some space, so if you have servers configured for things unrelated to the current project, consider turning them off.
- **Use subagents.** Subagents run in parallel with your main agent but have a **completely separate context window**. For tasks where you only need the answer — like "where are the authentication endpoints located?" — a subagent does the work and returns just a summary to your main agent, keeping your primary context clean.
- 