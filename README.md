# Cybersecurity Learning Portfolio

I'm a freshman computer science student learning cybersecurity through OverTheWire, Linux practice, and small projects. I use this repository to keep notes on what I try, what goes wrong, and what I learn along the way.

I leave out passwords and full challenge solutions.

## Current Focus

- Linux command-line fundamentals
- File formats, compression, and archives
- Basic networking and system concepts
- Security-focused problem-solving
- Clear, ethical technical documentation

## Featured Learning

### Linux File Analysis and Layered Data

In an OverTheWire Bandit exercise, I worked with data that had been transformed through several layers of encoding, compression, and archiving. I learned to inspect the data itself instead of trusting its filename, choose the correct utility for each format, and repeat the process until reaching readable text.

[Read the concept-focused lab write-up](linux/bandit-file-analysis.md)

## Repository Guide

```text
cybersecurity-portfolio/
├── README.md
├── linux/
│   ├── README.md
│   └── bandit-file-analysis.md
└── learning-log/
    └── README.md
```

| Section | What it contains |
| --- | --- |
| [Linux](linux/README.md) | Command-line notes and hands-on Linux labs |
| [Learning Log](learning-log/README.md) | Short reflections, milestones, and next steps |

## Skills Demonstrated

- Using the command line to create a safe working directory and manage files
- Reconstructing binary data from a textual hexdump
- Redirecting command output into a file
- Identifying a file by its contents rather than its extension
- Working with gzip, bzip2, and tar data
- Following an iterative investigate-and-verify workflow
- Documenting security exercises without sharing credentials or spoilers

## Learning Roadmap

- [x] Linux navigation and file management
- [x] Hexdumps, compression, and archives
- [ ] Users, groups, ownership, and permissions
- [ ] Processes, services, and logs
- [ ] Networking fundamentals and packet analysis
- [ ] Bash or Python security automation
- [ ] Introductory web application security

## Ethics and Spoiler Policy

This repository does not contain passwords, flags, credentials, or complete walkthroughs for active challenges. Write-ups focus on transferable concepts and security relevance. Any examples use generic filenames and sanitized output.

## About This Portfolio

I am early in my cybersecurity journey, so this portfolio will grow as my skills develop. Each entry aims to answer three questions:

1. What problem or concept did I explore?
2. What did I learn from it?
3. Why does it matter in cybersecurity?

---

*Built through hands-on practice and continuous learning.*
