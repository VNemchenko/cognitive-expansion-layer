# IP And Publication Strategy

## 1. Purpose

This document describes a practical publication strategy for [Brownyx](https://brownyx.com) CEL.

It is not legal advice. Consult an IP lawyer for legal decisions, patent strategy, trademark filings, or commercial licensing.

## 2. Recommended Strategy

Recommended approach:

1. Keep production [Brownyx](https://brownyx.com) implementation private.
2. Publish this documentation-only repository.
3. Use it as a defensive publication and public timestamp.
4. Include clear authorship and citation metadata.
5. Avoid publishing production prompts, scoring rules, secrets, or commercial know-how.
6. Create a tagged release such as `v0.1.0`.
7. Optionally archive the release with Zenodo, OSF, or another DOI-granting archive.

## 3. What Copyright Protects

Copyright generally protects concrete expression: text, diagrams, documentation, code, images, and specific written materials.

It does not generally protect the abstract idea of a cognitive expansion layer, a method in the abstract, or a general conceptual architecture.

Reference: WIPO Copyright FAQ: https://www.wipo.int/copyright/en/faq_copyright.html

This repository is useful for proving authorship and timestamp of the written expression and the project-specific framing.

## 4. Defensive Publication

A public repository can help establish prior art.

It may help show that the [Brownyx](https://brownyx.com) CEL concept, terminology, architecture ordering, and boundary rules were publicly disclosed at a given time.

This can be useful if another party later claims to have invented the same specific architecture after publication.

## 5. Trade Secret Boundary

Do not publish what should remain commercial know-how.

Keep private:

- exact production prompts;
- scoring thresholds used in production;
- model routing and fallbacks;
- proprietary evaluation datasets;
- production safety heuristics;
- implementation code;
- private runtime traces.

## 6. Patent Caution

If you believe CEL contains a patentable technical invention, do not publish detailed enabling material before speaking to a patent attorney.

Public disclosure may affect patentability depending on jurisdiction and timing.

Reference: WIPO Patents FAQ: https://www.wipo.int/patents/en/faq_patents.html

## 7. Trademark Strategy

The term `CEL` alone is short and generic.

Better candidates for brand protection:

- [Brownyx](https://brownyx.com);
- [Brownyx](https://brownyx.com) Mind;
- [Brownyx](https://brownyx.com) CEL;
- [Brownyx](https://brownyx.com) Cognitive Expansion Layer.

Trademark strategy should be handled separately from copyright and documentation licensing.

## 8. Recommended License Position

For this documentation-only repository, the recommended default is:

```text
CC BY 4.0 for documentation
trademarks reserved
production code not licensed
private implementation not disclosed
```

If stronger control is desired, use an all-rights-reserved notice instead.

Reference: Creative Commons CC BY 4.0: https://creativecommons.org/licenses/by/4.0/

## 9. GitHub License Note

GitHub notes that without a license, default copyright laws apply and others do not receive explicit rights to reproduce, distribute, or create derivative works from the work. For a public repository intended to be reusable and citeable, a clear license file is recommended.

Reference: GitHub Docs on repository licensing: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository

## 10. Suggested Public Notice

```text
Brownyx Cognitive Expansion Layer (Brownyx CEL) is a project-specific architecture concept by Vitaly Nemchenko.

This repository is a documentation-only defensive publication. It does not grant rights to production Brownyx source code, private prompts, trademarks, logos, infrastructure, or commercial implementation details.
```
