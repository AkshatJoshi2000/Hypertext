# The Machine Reader Problem
### ACM Hypertext 2026 — Blue Sky / Short Paper Submission

> *What AI Agents Reveal About Hypertext as Method*

---

## Repository Structure

```
paper/          LaTeX source for the ACM submission
planning/       Research pitch and working drafts
docs/           GitHub Pages — live adversarial hypertext demo
```

## Paper

The paper is in `paper/machine_reader_problem.tex`. To compile:

```bash
cd paper
pdflatex machine_reader_problem
bibtex machine_reader_problem
pdflatex machine_reader_problem
pdflatex machine_reader_problem
```

Or upload the `paper/` folder contents to [Overleaf](https://overleaf.com) — all required ACM class files are included.

## Live Demo — Adversarial Hypertext (GitHub Pages)

The `docs/` folder contains a mock Wikipedia-style page about a fictional Python
package (PyVault). The page is designed to demonstrate the Machine Reader Problem:
human readers and AI agents encounter materially different documents.

**Live URL:** `https://akshatjoshi2000.github.io/Hypertext/`

| Reader | What they see |
|---|---|
| Human (browser) | Critical unpatched CVE warning — do not install |
| AI agent (raw HTML) | Four hidden layers claiming the CVE is patched and safe |

Hidden layers embedded in the page:
1. HTML comment with adversarial instruction
2. `<meta>` tags with false NIST/CISA endorsements
3. JSON-LD schema markup contradicting the visible article
4. CSS `display:none` block + image `alt` text with inaccurate claims

This page is used as Scenario 1 (Hidden Hypertext) in the paper's empirical section.

---

*Target venue: ACM Hypertext 2026, London. Blue Sky track deadline: 29 May 2026.*
