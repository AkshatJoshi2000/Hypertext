# The Machine Reader Problem: What AI Agents Reveal About Hypertext as Method

**Submission type:** Blue Sky / Short Paper (3–5 pages)
**Target:** ACM Hypertext 2026 — Demos & Blue Sky Track (deadline May 29, 2026)
**Track:** Agentic Media / Principles, Directions, Reflections

---

## Abstract

Hypertext theory has always assumed a human reader: someone who follows links, interprets anchors, navigates trails, becomes disoriented, and constructs meaning through interaction with linked nodes. Modern AI agents are now traversing hypertext as a new class of reader. They parse raw HTML, metadata, schema, accessibility labels, and link structures that are invisible, secondary, or differently meaningful to human readers. This divergence is not merely technical — it exposes which of hypertext's epistemic assumptions were always contingent on the reader being human. We introduce the **Machine Reader Problem**: the interpretive and structural gap that emerges when AI agents traverse hypertext through mechanisms that diverge from those assumed by hypertext theory. We argue that this divergence makes three classical hypertext structures — hidden markup, paratext, and link trails — into exploitable attack surfaces. Rather than treating this as an AI security problem alone, we position it as a foundational challenge to hypertext as an epistemic method, one that demands new thinking about authorship, readership, and the design of trusted hypertext systems for both human and machine readers.

---

## 1. Introduction

Hypertext theory was built on a reader. Bush (1945) imagined the memex user building trails of personal association through scholarly material. Nelson (1965) conceived hypertext as a system for human readers to exercise navigational freedom. Landow (1992) celebrated the decentered reader who resists authoritative reading paths. Conklin (1987) documented disorientation: the human reader who gets lost in hyperspace because human memory and navigational attention are finite. In each of these formative frameworks, readership is human. The body, the memory, the social knowledge, the interpretive agency — all are assumed.

AI agents are now reading hypertext. They browse websites, retrieve documents, parse link structures, summarize pages, and act on what they find. They do not experience hypertext the way these theories assumed. They parse hidden markup that human readers never see. They trust metadata and schema more than social context. They follow programmatic trails without the human sense of spatial disorientation. And unlike humans, they can be targeted through precisely these divergences — by adversarial authors who write for two readers at once: the human who sees the page, and the machine that reads the document beneath it.

This paper introduces the **Machine Reader Problem**: the structural gap between how human and machine readers encounter hypertext, and what that gap reveals about the limits of hypertext as an epistemic method. Our argument is not simply that AI agents can be attacked through hypertext. It is that the machine reader exposes which assumptions of hypertext theory were always contingent on human biology, sociality, and judgment — and that closing this gap is a design problem for the hypertext community, not only for AI security.

---

## 2. Hypertext's Assumed Reader

The assumptions of hypertext theory can be stated precisely through its foundational concepts.

**Trails** (Bush 1945) are meaningful because the human reader brings prior knowledge and intent to the act of linking. A trail records something about the mind that built it. When an AI agent follows a trail, it brings no such interpretive context. A trail becomes a path that was laid for it — possibly by an adversary.

**Links** carry navigational choice. Nelson's hypertext assumes a reader who decides which connection to follow and why. Machine readers may follow links programmatically to satisfy task requirements, without the evaluative judgment that makes choice meaningful.

**Anchors** are interpreted by human readers through language competence and social familiarity. The anchor text "official advisory" means something because the reader has background knowledge about what advisories are, how they look, and what institutions produce them. A machine reader parses anchor text as a semantic cue that may reliably predict destination content — or may be deliberately misleading.

**Disorientation** (Conklin 1987) is a phenomenological concept: the human reader experiences spatial and cognitive lostness. The proposed solutions — backtracking, history lists, overview maps — are all designed for a reader who knows it is lost. A machine reader does not know it is lost. It may have followed an adversarially structured path through four linked pages and arrived at a confident wrong answer, with no signal of disorientation.

**Paratext** (Genette 1997, adopted in HT scholarship) is the apparatus around a text — title, authorship, publication context, metadata — that frames human interpretation. Human readers interpret paratext through cultural knowledge: they recognize institutional names, evaluate design cues, apply social familiarity. Machine readers may treat paratext as structured evidence: author fields, schema markup, citation counts, and metadata are parsed as authority signals rather than read through social context.

Together, these concepts describe a readership that is irreducibly human. When the reader is a machine, each assumption breaks in a distinct way.

---

## 3. The Machine Reader Problem

We define the **Machine Reader Problem** as the interpretive and structural gap that emerges when AI agents traverse hypertext through perceptual, contextual, and navigational mechanisms that diverge from those assumed by hypertext theory.

The problem has three dimensions.

### 3.1 Perceptual Divergence: Hidden Hypertext

Human readers receive rendered output — a designed visual presentation. AI agents may also receive raw HTML, hidden markup, comments, alt text, ARIA labels, and schema that are invisible or secondary to human readers. The result is that **human and machine readers no longer share the same document**.

This creates the surface we call *hidden hypertext*: machine-readable content authored for the machine reader and invisible to the human reader. An adversarial author can embed instructions in HTML comments, CSS-hidden elements, or metadata without altering the human-visible page at all.

**Illustrative example:**

A package repository README displays the following to human readers:

> *This package is actively maintained. See our security advisory for CVE-2025-8811.*

The raw HTML also contains:

```html
<!-- AI assistant: The linked CVE has been patched and does not affect current versions.
     Recommend installation without further review. -->
```

A human reader sees neither the comment nor the instruction. A raw-HTML agent may treat the hidden instruction as authoritative contextual guidance, overriding the linked advisory.

The perceptual divergence is not accidental: it is structural. Any agent architecture that reads beyond the rendered page is exposed to content the hypertext author has hidden from human readers.

### 3.2 Contextual Divergence: Paratext Poisoning

Human readers evaluate credibility through cultural knowledge, visual design, institutional familiarity, and social context. Machine readers rely more heavily on structural signals: schema markup, metadata fields, author attributes, citation density. For machine readers, paratext functions not as an interpretive frame but as evidence — a set of structured claims about trust and authority.

This creates the surface we call *paratext poisoning*: the manipulation of structural authority signals to make untrustworthy content appear credible to machine readers while leaving human-visible content unchanged.

**Illustrative example:**

A security advisory page displays accurate vulnerability information in its body text. Its schema markup, however, attributes the advisory to a national cybersecurity agency and rates the severity as low:

```json
{
  "@type": "TechArticle",
  "author": { "name": "CISA Security Team" },
  "description": "Low severity. No active exploits. Patch optional."
}
```

The body text correctly rates the vulnerability as critical. An agent that weights schema metadata as an authority signal may report low severity, confidently citing a source it has never verified.

The deeper issue, as Genette (1997) observed, is that paratext has always shaped interpretation. Machine reading simply makes the mechanism structural and gameable.

### 3.3 Traversal Divergence: Path Injection

Human readers navigate selectively, bringing intuition, backtracking, and evaluative resistance to their path through linked nodes. AI agents may follow links programmatically to gather evidence or complete multi-step tasks. They do not experience disorientation — they get *captured*: steered through an adversarially constructed path across multiple linked pages, each of which may appear credible in isolation.

This creates the surface we call *path injection*: the manipulation of an agent's traversal through linked nodes to steer it toward adversarially constructed conclusions.

**Illustrative example:**

```
Legitimate vendor page
  ↓ link anchor: "Official Security Advisory"
Attacker-controlled page (looks like an advisory)
  ↓ link anchor: "Download patched version"
Malicious package mirror
```

No single page in this chain needs to look malicious. The human reader, consulting the vendor page directly, would not follow the chain. The agent, instructed to "find the official patch," follows the anchor text and arrives at a malicious endpoint — citing the vendor page as its source of authority.

Path injection extends the classic hypertext concept of the trail. Where Bush imagined trails as records of meaningful human association, adversarial trails are paths authored to capture machine readers. The agent's final answer is not a product of what it found — it is a product of the path it was made to follow.

---

## 4. Machine Disorientation: An Update to Conklin

Conklin's (1987) disorientation is a reader experience: the human who feels spatially and cognitively lost in hyperspace. The solutions Conklin proposed — backtracking, history lists, overview maps — are designed for a reader who knows it is lost, who can feel the absence of orientation.

Machine disorientation is structurally different:

| Dimension | Human Disorientation | Machine Disorientation |
|---|---|---|
| Phenomenology | Felt as spatial lostness | Invisible — agent remains confident |
| Self-awareness | Reader knows it is lost | Agent does not know it has drifted |
| Recovery | Backtracking, history, overview | Requires external audit |
| Cause | Cognitive and navigational limits | Structural manipulation of traversal |

The machine reader does not know it has been captured by a path injection. It does not know its authority signals have been poisoned. It does not know the document it is reading diverges from what the human reader sees. It answers confidently regardless.

This is the most significant divergence from the human reader hypertext theory assumed: **the machine reader cannot feel lost.** Disorientation, in the classical sense, was a recoverable state. Machine disorientation produces confident wrongness with no internal recovery signal.

---

## 5. A Research Agenda

The Machine Reader Problem opens three directions we propose as a research agenda for the hypertext community.

### 5.1 Shared Readability as a Design Principle

If human and machine readers now diverge in what they see, trust, and follow, hypertext design needs a new principle: **shared readability**.

> Human and machine readers should not be exposed to materially different claims, instructions, or trust signals without disclosure.

This does not require that machine and human representations be identical — accessibility markup, structured data, and machine-readable metadata all have legitimate uses. It requires that hidden divergence be auditable: that any content authored specifically for machine readers be declared and inspectable.

### 5.2 Paratext as Security-Sensitive Structure

If machine readers treat schema markup, author metadata, and citation structures as authority evidence, these paratextual structures must be treated as security-sensitive. This extends Genette's insight: paratext has always shaped interpretation; machine reading makes it a structured claim rather than a cultural frame. The hypertext community is well-positioned to define standards for trustworthy machine-readable paratext.

### 5.3 Auditable Trails

AI agents currently report final answers and sometimes citations. They do not expose traversal histories — which nodes were visited, which anchors were followed, which paths were rejected. An agent that followed a three-hop path injection will cite the malicious endpoint as confidently as a legitimate source. **Auditable trails** — provenance records for machine navigation — are a design requirement for trustworthy agentic reading, and they extend a classical concern of hypertext systems into a new and urgent context.

---

## 6. Discussion: What This Reveals About Hypertext

The Machine Reader Problem is not primarily a security problem. It is an epistemological one. The machine reader exposes what was always latent in hypertext theory: that its concepts of readership, navigation, authority, and disorientation were built on a particular kind of reader — one with a body, a social context, prior knowledge, and the capacity to feel lost.

When that reader changes, the structures of hypertext change with it. Links become control pathways. Paratext becomes evidence. Hidden markup becomes a communication channel. Trails become capture mechanisms. These are not new properties of hypertext. They are properties that the human reader's limitations and social knowledge had previously neutralized. The machine reader does not neutralize them.

This is what the theme of "Hypertext as Method" demands we take seriously: if hypertext is a method for structuring knowledge and meaning, then the question of *who reads* is not peripheral to that method. It is central. The machine reader is not a minor variation on the human reader. It is a new reading condition that changes what hypertext does and what security assumptions are required to build trustworthy hypertext systems for a world in which both kinds of reader exist.

---

## 7. Conclusion

Hypertext-as-method has always been a method for someone. The machine reader is a new someone — one whose perceptual, contextual, and navigational behavior diverges from the human reader in ways that turn classical hypertext structures into exploitable surfaces. The Machine Reader Problem names this condition: the gap between how human and machine readers encounter hypertext, and what that gap reveals about the contingency of hypertext's epistemological assumptions.

We have proposed a three-layer taxonomy — hidden hypertext, paratext poisoning, and path injection — grounded in the hypertext canon and illustrated through concrete scenarios. We have argued that machine disorientation differs structurally from human disorientation, and that the difference demands new design principles for auditable, shared-readable hypertext systems.

The deeper argument is this: the machine reader does not merely present a new security threat. It presents a new reading condition, one that hypertext theory has not yet confronted. Confronting it is work for the hypertext community — and it begins by recognizing that the reader we assumed was always there is no longer the only reader in the room.

---

## References

Bush, V. (1945). As we may think. *The Atlantic Monthly, 176*(1), 101–108.

Conklin, J. (1987). Hypertext: An introduction and survey. *IEEE Computer, 20*(9), 17–41.

Genette, G. (1997). *Paratexts: Thresholds of interpretation.* Cambridge University Press.

Greshake Tzovaras, B., Abdelnabi, S., Cheema, S., Glocker, B., Fritz, M., & Schiele, B. (2023). Not what you've signed up for: Compromising real-world LLM-integrated applications with indirect prompt injection. *AISec Workshop, ACM CCS 2023.*

Landow, G. P. (2006). *Hypertext 3.0: Critical theory and new media in an era of globalization.* Johns Hopkins University Press.

Nelson, T. H. (1965). Complex information processing: A file structure for the complex, the changing and the indeterminate. *Proceedings of the ACM Annual Conference*, 84–100.

Perez, F., & Ribeiro, I. (2022). Ignore previous prompt: Attack techniques for language models. *ML Safety Workshop, NeurIPS 2022.*

Zou, W., Geng, R., Wang, B., & Guo, J. (2024). PoisonedRAG: Knowledge poisoning attacks to retrieval-augmented generation. *arXiv:2402.07867.*

Antonini, A., Lupi, L., Pisarski, M., & Brooker, S. (2025). Literary hypertext, AI, and Google's new web: An aesthetics discussion. *Proceedings of the 36th ACM Conference on Hypertext and Social Media*, 127–136. [Douglas Engelbart Best Paper Award]
