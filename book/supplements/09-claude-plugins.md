## Claude Code plugins — package your setup so others can install it

By this point in Module 9 you have authored a skill, wired a hook, and connected
a tool over MCP. Each of those lives in your project's `.claude/` directory:
personal, local, and easy to iterate on. **Plugins** are the next step — they
bundle those same building blocks into a single, versioned unit that a teammate
can install with one command instead of copying files by hand.

### Standalone configuration vs. a plugin

A standalone `.claude/` setup is the right call while the configuration is
personal, project-specific, or still changing. Reach for a plugin once you want
to *share* it across projects, a team, or the community. The trade-offs:

| | Standalone `.claude/` | Plugin |
| --- | --- | --- |
| Invocation | `/hello` | `/my-plugin:hello` (namespaced) |
| Scope | one project | reusable across projects |
| Sharing | copy files by hand | install from a marketplace |
| Versioning | none | explicit `version` or git commit SHA |
| Best for | personal workflows, quick experiments | team or community distribution |

The practical rule: start standalone for fast iteration, then convert to a
plugin when it is ready to travel. The namespacing (`/my-plugin:hello` rather
than `/hello`) is what prevents two installed plugins from colliding on the same
skill name.

### What a plugin bundles

A plugin is just a directory with a manifest at `.claude-plugin/plugin.json`
and its components sitting beside that folder at the plugin root — not inside
`.claude-plugin/`, which is the most common first mistake:

- **`skills/`** — model-invoked Agent Skills, one `SKILL.md` per folder.
- **`agents/`** — custom sub-agent definitions.
- **`hooks/hooks.json`** — the same hook events you met earlier in this module.
- **`.mcp.json`** — MCP server configurations shipped with the plugin.
- **`commands/`** — older flat-file commands; prefer `skills/` for new work.

The manifest itself is small. The `name` field doubles as the skill namespace:

```json
{
  "name": "score-candidates",
  "description": "Score N diffs on Correctness, Simplicity, and Fit.",
  "version": "1.0.0",
  "author": { "name": "Your Name" }
}
```

With that manifest, a `review/` skill inside the plugin is invoked as
`/score-candidates:review`. If you omit `version` and distribute over git, the
commit SHA becomes the version and every commit counts as a new release.

### Installing and sharing

Plugins are distributed through **marketplaces**. Two public ones ship with
Claude Code: `claude-plugins-official`, curated by Anthropic, and
`claude-community`, where third-party submissions land after review. You add a
marketplace and install from it with the `/plugin` command, then call the
namespaced skill. Teams that want to keep a toolkit internal can host a private
marketplace in their own repository — same workflow, no public listing.

While you are still building one, skip the install step entirely: load a
work-in-progress plugin with `claude --plugin-dir ./my-plugin` and run
`/reload-plugins` after each edit to pick up changes without restarting.

### From your skills library to a plugin

The Skills Library you assemble in this book (Appendix A) is already in the
right shape. To ship it as a plugin, drop a `.claude-plugin/plugin.json` next to
a `skills/` directory, move your `SKILL.md` folders in, and point a marketplace
at the repository. Your personal carry-out from the bootcamp becomes something
your whole team can install with a single line — which is exactly the leap from
*using* Claude Code to *engineering* with it that this module is about.
