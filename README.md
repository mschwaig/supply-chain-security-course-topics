# Supply Chain Security Presentation Topics

This lists the topics available in my course on
Software Supply Chain Security at JKU.

I will cover Block 0 in my lectures.
Topics from the other blocks are presented by sudents.
Students can also suggest their own topics.

I might update this file during the semester.

## Block 0: Lecture

These are topics that I could potentially cover in the lecture part of the course.

We will probably not be able to cover all of them.

I am also open to accepting student talks in these areas. Such talks would probably cover some specific aspect of the topics.

* the proposed SLSA Standard
* `.lock` files
* SBOMs
* Reproducibility as a concept
* From Source To Attestation
  - Trusted Boot
  - Transparency Logs
  - Remote Attestation
  - Source References
* Reproducibility VS signed binaries
* Nix

## Block 1: Version Control

Date: 15.11.2023

### The Git data model for supply chain security

How does git work and represents things like commits, tags and branches based on hashes.

Focus on the parts that are important for supply chain security.

Tell us what this data model means to us in the context of supply chain security.

For what purposes and in what contexts can we / can't we rely on git commit hashes, version tags etc.

Examples use cases:
* using commit hashes to identify a specific state of the code
* using tags or branches for naming/identifying specific 'releases' / name a specific state of the code
* recording authorship (author field, Co-authored-by and others, signed commits)
* are reviews recorded? what is in git/what is in GitHub (or another git hoster)

> [!NOTE]
> The first two use cases should be covered by your presentation.
> Let me know if you can or cannot manage to cover the other two as part of your presentation, so that I can prepare the that part outside your presentation.

### Secret management and re-writing repositories

Things like API keys, passwords, signing keys and other secrets frequently end up in public git repositories, for example on GitHub.

Fundamental questions:
What is the basic problem?
How does this problem arise?
What are potential consequences?

Consider referencing some media reports or publications about this issue to quickly get this point across.

Why does naively 'deleting files from version control' not address the issue?

How can we actually address the issue:

(1) dealing with already publicly exposed secrets
(2) re-writing history to remove them (e.g. ahead of releasing the code)

(How) can we audit our project's git history to help identify such issues?
Are there tools to do this quickly/easily?

### Advanced Topic: Guix Authentication

Source: https://archive.fosdem.org/2023/schedule/event/security_where_does_that_code_come_from/

Present this mechanisms that Guix uses, what Guix uses this mechanism for and also present your own commentary on it.

How useful do you think this is? In what contexts is it (not) useful? / What are the limitations?

> [!NOTE]
> I will probably not hand out this topic on its own but let me know if you want to cover it in your presentation or hear more about it.
> It might make a nice topic together with the last two use cases from the first git topic and signed commits. 

## Block 2: Package Manager case studies

Date: 29.11.2023
Count: 1-3

For the topics on this block I want you to present the package managers used in specific software ecosystems.

What those presentations should cover is largely independent of the specific package manager, so a lot of the topic description will be on this level with the individual topics only going into the specifics of the ecosystem that I think are important to cover.

Important questions to cover are:

* Can we use the package manager to produce a defined output?
  - ideally this means a bit-by-bit reproducible artifact
  - defined dependency versions or ranges are at least something
* What are the inputs consumed by the package manager?
  - Are they binaries or source? Both?
* How are the inputs obtained and hosted?
  - Is the used format well defined and used by more than one party?
* Is there a mechanism to ensure the integrity of inputs?
  - For example a `.lock` file?

You can also cover
* How can I look at the dependency graph of a project
* How well/badly this ecosystem is set up to handle supply chain security
* What are frequent problems? / What problems remain unsolved?
* Are there any automated tools
  - to update dependencies
  - audit dependencies

### Python

There's a few different tools in python.

For example:
* pip
* poetry
* anaconda

There is also the really annoying topic of `setup.py` files and their limitations and the `pip-audit` tool to audit dependencies.

Covering all of the package management options available for python would probably be too much for one talk, but it would be interesting to hear about why `pip` and how to get around that by using another tool or taking advantage of improvements in `pip` of which here have been a few recently. However I don't know if those improvements to pip cover everything we would like to have from a package manager.

### Rust's Cargo

A presentation of cargo should for sure cover
* the sometimes sprawling dependency trees seen in Rust
* the lack of an ABI and what it means for packaging with Cargo
* `.lock` files
* The lawless hellscape that is `build.rs` files
* the tools available in rust to inspect and audit dependencies

### Some specific Linux distribution

I don't know too much about how specific Linux distributions package software, but I am sure there is a lot to discuss there.
For a lot of Linux distributions how they handle this topic could make for a good presentation.
Since each of those projects has their own culture and processes, which are quite different from each over those processes could also make for an interesting part of the conversation.

For example
* Debian sometimes votes on issues and
* Arch Linux has the huge Arch User Repository (AUR) which is less curated than their main repositories
* NixOS is very interesting but I'm not sure how difficult it would be to cover as a topic

## Block 3: CI workflows and automation

Date: 13.12.2023 / alternative date possible
Count: 1

Pick a specific tool like GitHub Actions or Jenkins Pipelines or GitLab CI/CD.

Show how the CI file can be used to describe the **intended process** to
* build
* test
* release and
* deploy
software in a way that's checked into version control.

Important aspects you need to cover are
* the permissions that come with executing in CI and
* how 'malicious inputs' to CI can be mitigated for example by
  - only respecting specific configuration from the `main` branch
  - isolating CI runs from each other, from internal systems and from the public internet
* supplemental tools for some of:
  - dependency tracking
  - dependency updating
  - vulnerability scanning
* support for credential handling
* how do people release defined versions of software with those tools

## Block 4: Security Incident Reports

Date: 13.12.2023
Count: 1-3

Pick any interesting attack on supply chain security that either has enough public sources available or that you can present based on personal experience.

Examples are
* SolarWinds
* Log4J
* Microsoft losing signing keys

Present this attack in detail and show how it does or does not relate to what we are discussing in this course.

## Block 5: Security Measures

Date: 17.01.2021

### Reproducibility

Your presentation could present the work that various projects are doing for reproducibility or tools that are used by other projects to achieve reproducibility.

Examples for interesting projects are
* gitian
  - I think tor and bitcoin are using this
* diffoscope


Another topic of interest would be reproducibly building container images or significant related work on personal projects.

> [!NOTE]
> The big problem with this topic is that presenting one tool or project will probably not be enough material for a presentation. I still have this topic suggestion in here in case someone has an good idea for putting together a good presentation with enough material.

### Producing an SBOM

Date: alternative date possible

You could present a few of the available options for producing an SBOM.

You should not only explain the file format (which you do not have to cover in detail) but also a selection of tools an techniques for producing SBOMs. The presented tools and techniques do not have to apply to any possible software, you can pick a variety of specific languages or other circumstances where good tooling is available.

Make sure to try out the techniques you present yourself so that you have first hand experience.
If possible have the files and tools ready to demonstrate.

### Supply Chain Security Tools

Count: 1-3

You could present one of the popular tools, protocols and standards that try aim to improve software supply chain security.
Some promising candidates to present are:

* in-toto
* Chainguard's Sigstore
* The Update Framework (TUF)

Present the tools and their advantages and disadvantages.
When presenting a tool that you could easily try out yourself make sure to do so and if possible bring it along for a quick Demo.

We can have multiple presentations that showcase different tools. In that case please coordinate so that we don't get two very similar presentations because your talking about the same thing. You can instead coordinate and try to contrast and compare and focus a bit more on the differences.

### Legal mandate

Date: alternative date possible

There have been various recent efforts to regulate the software supply chain.

In the US there has been one or multiple executive orders in February and May of 2021, which have touched on those topics.
In the EU the Cyber Resilience Act (CRA) was proposed, which is the most relevant proposal to us in he EU.
There have also been a number of other proposals in other jurisdictions.

You can either strictly focus on the CRA or also take other legislation into account.
Either way present what is in this (proposed) legislation not (only) based on the documents themselves but mostly based on various expert opinions on the public record.

Your presentation should focus on supply chain security and present the topic in an interesting manner.

## Other Topic Ideas

* Trade-offs with regards to trust
  - On premise VS in the cloud
  - Open source VS closed source
  - Trusting code VS trusting developers
* Vulnerability management/tracking tools
* Secret management tool (à la HashiCorp Vault)

