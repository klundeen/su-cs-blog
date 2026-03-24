---
layout: post
title: "The AI Knew It Was a Truck. The Other AI Didn't."
subtitle: "What happened when I stopped banning AI and started using it"
date: 2026-03-10
author: Kevin Lundeen
author_title: "Teaching Professor, Department of Computer Science"
---

A year ago, I thought LLMs were an annoying flea. They made it easier for my students to cheat. I banned all AI use in my courses. If you want to learn how to tie your shoes, don't buy velcro ones!

Then a few things happened in quick succession. My boss at OneTouchEMR — my consulting gig — went all gaga over AI, the way C-suite people do. So we built some AI systems into our medical records product. Meanwhile, I was tapped to build the online AI Systems course, ARIN 5360, for Seattle U's new MSAI program. I picked Claude as my primary tool because Anthropic claims HIPAA compliance, which matters for OneTouchEMR. With my subscription, I started using it for everything.

And I mean everything. Consulting work. Course development. Lecture prep. Grading rubrics. Debugging. Writing. I used AI to help build the AI course, of course. And of course I would let the students use AI in careful ways in the course, too.

Somewhere in there, I went from flea to enamored. This post is about what I've learned since.

---

## The truck

You may have heard this one. I was recording a lecture for ARIN 5360, live-coding a CNN image classifier on CIFAR-10.[^cifar] PyCharm's AI autocomplete offered to fill in the list of class names. I accepted. It produced nine. It left out "truck."

I didn't notice. A few minutes later, the classifier returned class index 9. My label list had no index 9. I had to debug it on camera, in front of my students.

The neural net that classified the image knew it was a truck. The neural net that wrote the code didn't.

![PyCharm's AI autocomplete fills in the CIFAR-10 class list — nine classes, no truck. Note the "Code Completion → Insert Inline Proposal" tooltip at the bottom.]({{ site.baseurl }}/assets/images/bug-introduced.jpg)

![A few minutes later: back in the editor, staring at lines 62–70. Airplane, automobile, bird, cat, deer, dog, frog, horse, ship. Count them. Nine.]({{ site.baseurl }}/assets/images/where-is-truck.jpg)

It tickled me. And it turned into a way of thinking about a much bigger question: how do we teach students to be the one who knows?

[^cifar]: CIFAR-10: 60,000 tiny images in 10 classes. The "hello world" of image classification. Krizhevsky, "Learning Multiple Layers of Features from Tiny Images," University of Toronto, 2009.

## A starting premise

Banning AI from our classrooms is like banning calculators from a math department (sometimes, yes!). But as a blanket policy, it's impractical, and it doesn't prepare students for the world they're about to enter. Our students will use these tools professionally on day one after graduation.

Steve Yegge says he's "10 to 20 — to even 100 — times as productive" with AI.[^yegge] That might be hyperbole, but even the conservative version is a big deal. And as Ryan Salva puts it: "I care less that the models are really good at producing the right result the first time. I care much more that there are validation steps in place so that it eventually gets the right answer."[^salva]

That's the whole game. Not whether students use AI, but whether they can validate what it gives them.

And here's the thing Anil Dash wrote in the *Times* that I keep coming back to: in creative fields, LLMs take away the soulful parts and leave the drudgery. But in coding, they take away the drudgery and leave the soulful parts to you.[^dash] We're on the lucky side. Our students need to be, too.

[^yegge]: Steve Yegge, "Cheating Is All You Need," blog post, 2025.
[^salva]: Ryan Salva, VP of Product at GitHub, on the GitHub Copilot podcast, 2025.
[^dash]: Anil Dash, "A.I. Is Making the Coder's Life Better," *New York Times*, 2025.

## The tier matters

After the truck incident, I started seeing the same pattern across everything I teach. But the nature of the challenge — and the right teaching response — depends entirely on what tier of AI engagement your course sits at. This taxonomy matters, because one size doesn't fit all.[^tier]

**Build It** — In CPSC 5600 (Parallel Computing), students are learning the internals: attention mechanisms, GPU kernels, the infrastructure AI runs on. They need to understand tiling and warp divergence[^warp] and why shared memory exists. The AI can write a kernel that compiles. The student needs to know how it's leaving 90% of performance on the table. Traditional exams still work here, because the questions are about *understanding*, not output.

**Integrate It** — In ARIN 5360 (AI Systems), students are building RAG pipelines and retrieval systems. They're using AI components as building blocks. Assessment here is about process: commit history, design documents, the reasoning behind architectural choices. The truck story lives here — you need to understand the seams between components.

**Supervise It** — This is the tier that keeps us teachers up at night. In standard coding courses — 5001, 5042, 5510 — the AI can do the homework. Not "help with" — *do*. The student submits code, and it works, and the provenance is unknowable.[^laundering] The approach here is scaffolded in-class practice with proctored exams that ask about the homework. The subtle shift is less "write it" and more "evaluate, debug, and improve it."

**Use It** — In CPSC 5320 (Visual Analytics), using AI well *is* the assessment. Students generate visualizations, analyze datasets, iterate with AI tools. The question isn't whether they used AI — it's whether they caught the sawtooth-that-isn't-seasonality, whether they could tell plausible from correct. The skill is the verification.

The teaching approach has to match the tier. A no-AI exam makes sense in "Build It." A submit-your-AI-transcript assignment makes sense in "Use It." Applying the wrong approach to the wrong tier is how you get bad policy.

[^tier]: I presented this taxonomy in a faculty talk in March 2026. The four tiers evolved from an earlier version with slightly different framing — the key insight is that the *relationship* between the student and the AI determines what good teaching looks like.
[^warp]: Warp divergence: when threads in a GPU warp take different branches, the GPU executes both serially, killing parallelism. AI-generated kernels routinely ignore this.
[^laundering]: This isn't hypothetical. A student once submitted work that I recognized as my own reference solution — they'd prompted an LLM with the assignment description and it gave them back something very close to what I'd written. They were honest about it when I asked. This is the provenance problem in practice.

## Things I'm actually trying

Here's where I stop being philosophical and start being practical. These are concrete experiments, some tested, some planned.

### In-class AI sessions

Show the mess, not just the result. I use AI live during lectures — let students see when it gets things wrong, how I redirect, when I accept versus push back. The truck story happened during one of these. Deliberately showing failure, the bad code, the hallucinated API, the "wait…" moments — that's the pedagogy. Students need to see the *process*, not polished outputs.

### Directed dialogs

Scripted prompting exercises with specific learning goals. Start with "write a function to merge two sorted lists." See what the AI gives you cold. Read the code — does it handle edge cases? Empty lists? Tell the AI "that fails on [1,3] and [2]." Debug through dialog. Challenge it with duplicates. Students submit the full transcript. The conversation is the assignment.

### Battling AIs

The truck story as a method. One AI generates code or analysis. A different AI critiques it — finds errors, challenges assumptions, suggests improvements. The student is the judge. Who's right? This builds verification habits by making the student the arbiter between two confident, articulate, possibly-wrong systems.

### Submitted transcripts

In Visual Analytics, I'm planning: "Discuss this paper with an AI, then submit the conversation." The grading rubric is about quality of prompts, quality and originality of the analysis, and whether the student caught errors. The process becomes visible and assessable. This could work in any reading-heavy course.

### Scaffolded coding quizzes

In-class, no-AI checkpoints that build toward AI-assisted work. The student proves they understand the concept on a quiz, *then* they get to use AI on the larger assignment. The quiz isn't punitive — it's the scaffold that makes the AI-assisted work meaningful. And proctored exams are still the top tool for face-to-face assessment. Ask about the homework.

### Per-assignment AI policy

Default is "no AI," opened when it serves learning. The syllabus frames it: the goal is arriving at the solution, not the solution itself. And don't publish direct solutions — they end up in training data, and then they end up back in your students' submissions. I know this because it happened to me. A student prompted an LLM with my assignment description and got back something I recognized as my own reference solution. That's how I caught it.[^laundering2]

[^laundering2]: The student was honest about what happened when I asked. They didn't realize they were submitting my work back to me, laundered through an AI. The provenance problem is real and it runs in both directions.

## The column of A's

Here's the thing I don't have an answer for.

![A gradebook from one of my courses. The "Total" column reads A, A-, A, A-, A, A, A, A. The callout says it: "No differentiation!"]({{ site.baseurl }}/assets/images/column-of-as.jpg)

If students are more productive with AI — and they are — and they're turning in better work — and they are — then grades go up. I'm looking at a column of A's in some of my courses. Is that grade inflation? Or is it the new baseline? If a carpenter gets better tools, we don't give them a worse grade for using them. But if the tools are doing the carpentry...

I don't know. This is genuinely unsettled. If you have ideas, I want to hear them.

## Where's this headed?

The tools are getting better faster than our pedagogy. Agentic coding is already here — AI that writes, tests, and deploys its own code.[^agentic] What does "teach coding" even mean then?

The semester conversion is consuming all our oxygen at Seattle U right now — but this conversation can't wait until 2028. Whatever policy we set today may be obsolete by next quarter.

I don't have a unified theory. I have experiments, some principles I hold lightly, and a truck story. The truck story tells me this: the AI doesn't know what it doesn't know, and neither do you, unless you have the domain expertise to check. That means the domain expertise is more important than ever, not less.

That's good news, if you're a teacher.

[^agentic]: See, for example, Anthropic's Claude Code, Cursor, and similar tools that go beyond code completion into autonomous multi-step coding workflows. The capability gap between "autocomplete" and "autonomous agent" is closing fast.

## How this was made

This post started as two faculty talks — the truck talk in early March and a follow-up at the department meeting on March 19. I then sat down with Claude and said, roughly, "turn my talks into a blog post." The first draft was too philosophical and not concrete enough — it wanted to write an essay about principles when I wanted to write about things I'm actually doing. Several drafts later we got here. I rewrote a lot of it; Claude restructured a lot of it; we argued about tone. The usual.

The recursion goes deeper: the March 19 slides were themselves built with Claude. The last slide before discussion shows me asking Claude to add a slide about using Claude to make the slides. That's what "Use It" looks like.

---

*Kevin Lundeen is a teaching professor in the Department of Computer Science at Seattle University, where he teaches parallel computing, distributed systems, computer networks, and AI systems. He is also VP of Software Engineering at OneTouchEMR, where he recently built AI clinical documentation features and learned that HIPAA compliance is not the most exciting reason to choose an AI vendor, but it is a valid one. Previously, he was a managing director at Goldman Sachs, where he co-created SecDB (Goldman's trading and risk management system) and [Slang](https://en.wikipedia.org/wiki/Slang_(programming_language)) (a proprietary language similar to Python). He started programming with Fortran on punched cards in the late 1970s. The truck has been found. He is pretty sure there are more trucks.*
