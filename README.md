# Colombia

Claude skills for Colombian business operations — accounting, tax, and regulatory workflows.

Install as a Claude Code plugin or use individual skills standalone.

## Skills

| Skill | Domain | Description |
|-------|--------|-------------|
| **contable** | Accounting & Tax | Retention computation, invoice processing, regime classification for Colombian businesses. |

## Install

```bash
# Claude Code plugin (all skills)
claude plugin add buritica/colombia

# Or reference a specific skill directory
claude skill add buritica/colombia/contable
```

## Structure

Each domain is a standalone plugin with its own skills, references, and configuration:

```
colombia/
├── contable/              # accounting & tax
│   ├── skills/
│   │   └── retencion/     # retention computation
│   └── references/        # rate tables, matrices, estatuto extracts
├── (future: construccion/)
├── (future: laboral/)
└── (future: societario/)
```

## References

Reference files are structured markdown — rate tables, decision matrices, legal extracts — optimized for agent consumption, not raw PDFs.

Sources are cited inline. Annual values (UVT, rate changes) are tagged with their effective year for easy updates.

## License

Apache-2.0
