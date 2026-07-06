---
name: ej-access-security
description: Enforce EJ Coding Standards Section III — Access & Security (Standards 24–25). Covers least privilege access scoping, input sanitization, encryption at rest and in transit, strict access control at every layer, and regular security audits. Use for any security-sensitive code path or permission model.
license: MIT
compatibility: opencode
---

## What I do

I apply Standards 24–25 of the EJ Coding Standards when writing, reviewing, or auditing security-sensitive code. I enforce access scoping and first-class security requirements from the first line of code.

## When to use me

Use me when:
- Designing or reviewing permission models, access rights, or privilege scoping
- Writing code that handles user-supplied input, sensitive data, or protected resources
- Implementing authentication, authorization, or access control logic
- Auditing code paths for encryption, sanitization, or security hardening gaps
- Reviewing third-party dependencies for known vulnerabilities

---

## Standards

### Standard 24 — Least Privilege
Every module, function, thread, or component receives only the access rights and resources it strictly requires to fulfill its specific responsibility — nothing more.

**Rules:**
- Access is scoped, earned, and explicitly granted — never inherited by default or assumed from context
- The less access a unit holds, the less damage it can cause when it fails or is exploited
- Never request broad permissions when narrow ones suffice
- Revoke access as soon as the task requiring it is complete

**Applies to:** file system permissions, database query privileges, API keys and tokens, thread/process privileges, network socket access, memory regions.

> Standard 24 restricts what a module is *permitted to access* — a runtime access control concern.
> Standard 23 (Structure & Responsibility) restricts what a module *exposes* — a design-time encapsulation concern.

### Standard 25 — Security
Security is a first-class engineering requirement from the first line of code — not a checklist applied at the end.

**Input Sanitization**
- All external input must be sanitized before use
- Validate type, format, length, and range at the point of entry
- Reject and log invalid input before it can propagate into system logic
- Never trust data arriving from outside a function or service boundary

**Encryption**
- Sensitive data must be encrypted at rest and in transit
- Use established, current cryptographic standards — never roll your own crypto
- Key management is part of the security design, not an afterthought

**Access Control**
- Apply strict access control throughout the codebase, not only at perimeters
- A system is only as secure as its weakest, least-considered code path
- Security must be considered at every layer

**Security Audits**
- Conduct regular security audits as an engineering practice, not a release-gate exercise
- Treat every dependency as a potential attack surface

---

## Enforcement Checklist

- [ ] Does every component have only the access it strictly needs? (Std 24)
- [ ] Is access explicitly granted — never assumed from context? (Std 24)
- [ ] Is all external input sanitized at the point of entry? (Std 25)
- [ ] Is sensitive data encrypted at rest? (Std 25)
- [ ] Is sensitive data encrypted in transit? (Std 25)
- [ ] Are access controls applied throughout — not only at the perimeter? (Std 25)
- [ ] Have third-party dependencies been reviewed for known vulnerabilities? (Std 25)
