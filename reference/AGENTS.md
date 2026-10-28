EconomyCore Rewrite — Engineering Rules

Project

Build an original, production-quality Minecraft economy and shop plugin for canvasmc 1.21.11.

Primary goals:

1. Complete, polished player-facing features.
2. Modern, intuitive inventory GUIs.
3. Reliable economy transactions and persistent data.
4. Compatibility with the existing server ecosystem.
5. Good performance and maintainable code.

Mandatory workflow

- Read docs/FEATURE_MATRIX.md and docs/UNKNOWN_BEHAVIOR.md before implementation.
- Preserve every verified requirement unless explicitly approved otherwise.
- Mark unknown requirements instead of inventing behavior.
- Implement in small, reviewable phases.
- Build and test after every major module.
- Never report success without actual verification.

Platform

- Verify the exact target API and Java toolchain before configuring the build.
- Target Leaf 1.21.11 compatibility.
- Prefer supported Paper/Bukkit APIs over unstable server internals.
- Verify third-party APIs and versions before integrating them.
- Keep optional integrations isolated and gracefully disabled when unavailable.

GUI and UX

- Use reusable GUI components, consistent item layouts, pagination, navigation, and configurable text.
- Prevent duplicate clicks and stale inventory interactions.
- Revalidate permissions, prices, stock, and balances when processing transactions.
- Keep menus readable, consistent, and visually restrained.
- Provide clear success and failure messages.
- Avoid hardcoded prices, unnecessary animations, and excessive sound effects.

Economy correctness

- Use atomic or appropriately synchronized transaction logic.
- Prevent negative balances, duplicated payments, and item duplication.
- Handle concurrent transactions and failed persistence operations safely.
- Use exact monetary representations, not floating-point values for balances.
- Validate amounts, permissions, and all player-controlled inputs.
- Never silently discard failed writes.
- Document transaction consistency guarantees.

Storage

- Choose SQLite or MySQL based on documented requirements.
- Use parameterized queries, appropriate indexes, and bounded connection resources.
- Never perform blocking database operations on the server main thread.
- Respect Bukkit/Paper thread ownership when accessing player, inventory, or world APIs.
- Implement safe shutdown, error handling, backups where appropriate, and schema migrations.
- Do not introduce a migration that risks existing data without an explicit plan.

Quality

- Test economy operations, shop purchases, sales, permissions, persistence, reload, and failure scenarios.
- Test duplicate clicks, simultaneous transactions, insufficient funds, invalid prices, and inventory-full cases.
- Measure performance before making performance claims.
- Keep dependencies minimal and justified.
- Review concurrency, memory leaks, compatibility, and security before release.

Delivery

- Provide reproducible build instructions and a clean JAR.
- Include default configuration, command and permission documentation, and installation instructions.
- Report exactly which tests passed, failed, or could not run.
- Never deploy to the production server without explicit approval.

