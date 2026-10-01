# site-theme

Shared Hugo theme for [0J Consulting Oy](https://0j.fi) sites — [dfir.fi](https://dfir.fi) and [csoc.fi](https://csoc.fi).

A dark, monospace, glitch-accented theme that renders a sortable **provider list**
(Company / Website / Added / Modified) from one Markdown file per provider, with
git-based last-modified dates, a sister-site menu link with a glitch transition,
and referral (`utm_source`) tagging on outbound links.

## Per-site configuration

The theme is brand-neutral; each site supplies its identity through config and a
wordmark image. Relevant `hugo.toml` params:

| Param | Purpose | Example (dfir.fi) |
|-------|---------|-------------------|
| `brand` | `<title>` prefix, logo alt/aria-label, Training H1 prefix | `"DFIR-FI"` |
| `trainingTitle` | full Training H1, overriding `brand` + page title (optional) | `"DFIR Training"` |
| `siteName` | footer copyright line | `"dfir.fi"` |
| `company_name` / `company_link` | footer "operated by" | `"0J Consulting Oy"` / `"https://0j.fi"` |
| `referralQuery` | appended to outbound provider/training links | `"utm_source=dfir.fi&utm_medium=referral"` |
| `[params.sisterSite]` `name` / `url` | sister-site menu link + glitch | `"CSOC.FI"` / `"https://csoc.fi/"` |
| `enableGitInfo = true` | required for the Modified column | |
| `lastmodIgnoreCommits` | commit hashes that don't count as a modification | |

Each site provides its own wordmark at `static/images/logo.png` (the theme no
longer bundles one). The 0J favicon set and footer mark ship with the theme.

The RSS menu link renders only when the home page emits an RSS output format, so a
site with `[outputs] home = ["HTML"]` shows no RSS link.

## Providers

```
hugo new --kind provider content/providers/<name>.md
```

Front matter: `company`, `website`, `date` (the "Added" date). The Modified column
comes from git history (last commit touching the file), excluding any hash listed
in `lastmodIgnoreCommits`.
