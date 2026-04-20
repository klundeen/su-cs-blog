---
layout: post
title: "A Reading List on CS Education in the Age of AI"
subtitle: "Arranged as a table of contents for a book I might or might not write"
date: 2026-04-20
author: Kevin Lundeen
author_title: "Teaching Professor, Department of Computer Science"
---

Anil Dash wrote a line in the *Times* a few weeks back that I keep coming back to: in creative fields, LLMs take away the soulful parts and leave the drudgery; in coding, they take away the drudgery and leave the soulful parts to you. We're on the lucky side of that deal. Our students need to be, too. This is fun!

That's the stance underneath this post. I've been 
having more fun teaching CS in the 
last year than I've had in a while, and 
more fun practicing it on the OneTouchEMR 
side of my life. Figuring out how to 
share that with students (not just the tools, the stance) is the work I'm trying to do. One of the stretch goals of that work is a short book, tentatively, on teaching and practicing software in the age of generative AI, from the dual vantage of graduate systems teaching and small-company engineering. I don't know yet whether the book will happen. But the working outline I've been drafting seems as good a scaffolding as any for a reading list on recent art in the field.

So that's what this post is. The recent work I'm reading, grouped under my tentative chapter headings. Three to six works per section, lightly annotated, weighted heavily toward 2024-2026.

A note on what's here and what isn't. The computing-education research community seems to have produced an enormous volume of work since late 2022. I've tried to pick the pieces that have become reference points (the ones everyone else cites) rather than the ones I might agree with most. Where an industry or practitioner piece has reshaped the conversation more than any paper, it's in.

The usual suspects will repeat. Ethan Mollick on the general question of working with AI, the Denny/Prather/MacNeil/Becker constellation on CS ed specifically. I'll resist re-annotating them each time.

To be clear about what this list is and isn't: I haven't read all of it yet. Some I have, especially the books in Parts I and IV. A lot of the academic papers and industry pieces I've picked based on a literature search, citation patterns, and a sense of what the field seems to be pointing at. The annotations reflect why I think each piece is worth reading, not a verdict after reading. The post is the reading list I'm working through. A future post might be the verdicts.

The most useful section for you might be the ["What's missing, and why"](#whats-missing-and-why) part at the bottom, where I name the gaps. If you know work I should be reading, that's where the conversation is most open.

![A drawer in the Indiana State Library card catalog, headings Lover through Luma. Every reading list is a smaller version of this — someone's ordering of a pile too big to hold in your head.](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/Card_catalog_at_the_Indiana_State_Library_-_headings_Lover_through_Luma.jpg/1024px-Card_catalog_at_the_Indiana_State_Library_-_headings_Lover_through_Luma.jpg)

**Contents**

- [Part I. Epistle](#part-i-epistle)
- [Part II. Industry and Students](#part-ii-industry-and-students)
- [Part III. The Four Domains as Preparation](#part-iii-the-four-domains-as-preparation)
- [Part IV. The Practitioner's Stance](#part-iv-the-practitioners-stance)
- [Part V. Program Design, and Honest Uncertainty](#part-v-program-design-and-honest-uncertainty)
- [What's missing, and why](#whats-missing-and-why)

---

## Part I. Epistle

Short by design. Enough to set the vantage and the central claim: much of the "how" of software becomes cheaper with AI, and what remains load-bearing is human judgment, taste, accountability, and competence in off-distribution territory. These pieces frame that claim without overclaiming either way.

- Dash, A. (2026, March 13). [What Do Coders Do After AI?](https://www.anildash.com/2026/03/13/coders-after-ai/) *New York Times Magazine*. The essay this whole post takes its stance from. Dash's observation that coding may be one of the lucky creative domains, where AI takes the drudgery and leaves the soulful parts, is the most generative single line I've read on this topic in a year. This can be read in a single sitting.

- Mollick, E. (2024). *Co-Intelligence: Living and Working with AI*. Portfolio/Penguin. The reference point for the working-with-AI framing in the popular market. His centaur/cyborg distinction and "invite AI to the table" posture are the generalist baseline any CS-specific treatment writes against and alongside. Strong on stance, thinner on CS-specific practice, which is part of why a CS-specific book has room to exist. His ongoing Substack, [*One Useful Thing*](https://www.oneusefulthing.org/), is the fastest way to track how his positions evolve.

- Bowen, J. A., & Watson, C. E. (2024; 2nd ed. 2025). [*Teaching with AI: A Practical Guide to a New Era of Human Learning*](https://www.press.jhu.edu/books/title/54122/teaching-ai). Johns Hopkins University Press. The generalist higher-ed book. Owns the shelf for faculty of all disciplines. Useful as the thing my book wouldn't be: it covers the breadth of postsecondary teaching; I'd go narrow and deep on systems-adjacent graduate CS.

- Prather, J., Denny, P., Leinonen, J., Becker, B. A., et al. (2023). [The Robots Are Here: Navigating the Generative AI Revolution in Computing Education](https://arxiv.org/abs/2310.00658). *ITiCSE-WGR '23*. The foundational working-group report. Synthesizes 71 primary articles and surveys students and instructors across 20 countries. Still the single most-cited reference in the CS-ed-and-AI literature. If there's one paper a CS faculty member should read before anything else, this is it.

- Denny, P., Prather, J., Becker, B. A., et al. (2024). [Computing Education in the Era of Generative AI](https://cacm.acm.org/research/computing-education-in-the-era-of-generative-ai/). *Communications of the ACM* 67(2), 56-67. [DOI: 10.1145/3624720](https://doi.org/10.1145/3624720). Shorter, CACM-venue companion to the working-group report. Probably the piece to hand to the provost.

---

## Part II. Industry and Students

The practitioner vantage. An AI-role taxonomy (tool / gofer / assistant / junior / TA / oracle) would live here, grounded in OneTouch case studies. Supporting literature is more economic and industry-facing than pedagogical.

- Karpathy, A. (2025, June 17). [*Software Is Changing (Again)*](https://www.youtube.com/watch?v=LCEmiRjPEtQ). YC AI Startup School keynote. The "Software 3.0" frame (1.0 handwritten code, 2.0 learned weights, 3.0 natural-language prompts) is the industry-side taxonomy anyone writing in this space will likely have to engage with. Also the origin of "jagged intelligence," which seems genuinely useful for describing AI's uneven capability profile to students. Latent Space has a [solid annotated write-up](https://www.latent.space/p/s3).

- Karpathy, A. (2025, February 2). [Vibe coding post on X](https://x.com/karpathy/status/1886192184808149383). And his subsequent pivot to "agentic engineering" in February 2026, [summarized at The New Stack](https://thenewstack.io/vibe-coding-is-passe/). Worth citing together as evidence of how fast the vocabulary shifts inside a single year. The 2026 move is the kind of perishable specific worth handling carefully so the writing doesn't date itself.

- Willison, S. (2025, March 11). [*Here's how I use LLMs to help me write code*](https://simonwillison.net/2025/Mar/11/using-llms-for-code/). Widely cited as a standout practitioner essay on working with AI in code, and the one I most want to read carefully. Willison's yearly retrospectives ([2023](https://simonwillison.net/2023/Dec/31/ai-in-2023/), [2024](https://simonwillison.net/2024/Dec/31/llms-in-2024/), [2025](https://simonwillison.net/2025/Dec/31/the-year-in-llms/)) look like the closest thing to a primary source we have for tracking practitioner vocabulary as it stabilizes.

- Becker, J., Rush, N., Barnes, E., & Rein, D. (2025). [Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity](https://arxiv.org/abs/2507.09089). METR. The 19% slowdown finding. Experienced developers on mature codebases were slower with AI tools, and [misjudged the effect of AI on their own work by roughly forty percentage points in the wrong direction](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/). This looks like an important data point for the claim that AI performance drops sharply on domain-idiosyncratic code, and I want to read it carefully before relying on it. METR's [February 2026 follow-up](https://metr.org/blog/2026-02-24-uplift-update/) on why they're redesigning the study is worth reading too; it shows how hard this measurement is.

- Brynjolfsson, E., Chandar, B., & Chen, R. (2025). [Canaries in the Coal Mine? Six Facts about the Recent Employment Effects of Artificial Intelligence](https://digitaleconomy.stanford.edu/wp-content/uploads/2025/08/Canaries_BrynjolfssonChandarChen.pdf). Stanford Digital Economy Lab. The entry-level-software-engineering decline finding. Roughly -13% for ages 22-25 in highly exposed occupations, with employment for older workers in the same jobs stable or growing. Whatever one thinks of the methodology, this is likely the paper admissions deans are reading.

- Anderson, E., Parker, G., & Tan, B. (2025, August 18). [The Hidden Costs of Coding with Generative AI](https://sloanreview.mit.edu/article/the-hidden-costs-of-coding-with-generative-ai/). *MIT Sloan Management Review*. The brownfield argument. AI productivity gains are largest in greenfield work and most dangerous in legacy systems deployed by inexperienced developers. Maps directly onto my day job at OneTouch (CakePHP 2, mature healthcare codebase). The piece I would point VPs at.

- GitClear's annual *AI Copilot Code Quality* reports, [surveyed in LeadDev, August 2025](https://leaddev.com/technical-direction/how-ai-generated-code-accelerates-technical-debt). The "code churn doubled, copy-pasted lines exceed moved lines, refactoring dropped from 25% to under 10%" numbers. Whether the trend lines survive scrutiny or not, they've anchored the industry conversation about AI and technical debt.

---

## Part III. The Four Domains as Preparation

The pedagogical payload of the hypothetical book. Each domain (systems, architecture, AI systems, visualization) pairs one course with one characteristic AI relationship, one characteristic expert-mode, and worked assignments. Literature below covers both the CS-ed research corpus and domain-specific pedagogy.

### Systems (CPSC 5042) as the "Tutor" Relationship

- Prather, J., Reeves, B. N., Leinonen, J., MacNeil, S., et al. (2024). [The Widening Gap: The Benefits and Harms of Generative AI for Novice Programmers](https://arxiv.org/abs/2405.17739). *ICER '24*. [DOI: 10.1145/3632620.3671116](https://doi.org/10.1145/3632620.3671116). The metacognition result. Novices split into accelerated and hindered groups when given AI tools, and previously-known metacognitive difficulties don't just persist. They compound. Grounds my claim that systems courses need to keep the productive-struggle floor intact even as AI is introduced.

- Margulieux, L. E., Prather, J., Reeves, B. N., Becker, B. A., et al. (2024). Self-Regulation, Self-Efficacy, and Fear of Failure Interactions with How Novices Use LLMs to Solve Programming Problems. *ITiCSE '24*. The companion piece to Widening Gap. Self-regulation and self-efficacy moderate AI's effects; the students who least can afford AI's pitfalls are often the ones most drawn to it.

- Porter, L., & Zingaro, D. (2023; 2nd ed. 2025). [*Learn AI-Assisted Python Programming with GitHub Copilot and ChatGPT*](https://www.manning.com/books/learn-ai-assisted-python-programming-second-edition). Manning. The AI-first CS1 textbook, and the cleanest example of "tutor" pedagogy built around AI as a scaffold. Strong on problem decomposition, reading code, and testing as the new fundamentals. Less suited to systems-deep courses, but useful as a contrast case.

### Architecture (CPSC 5600) as the "Sculpture" Relationship

I haven't drafted this domain yet, and the literature is thinner than I'd like. Placeholder sources:

- Kumar, A. N., Raj, R. K., et al. (2024). [*Computer Science Curricula 2023* (CS2023)](https://ieeecs-media.computer.org/media/education/reports/CS2023.pdf). ACM/IEEE-CS/AAAI. The decade guideline document. The "Generative AI and the Curriculum" chapter is worth reading in full, particularly the software-implications section.

- Simha, R., Kumar, A. N., & Raj, R. K. (2024, February). Principles and Pitfalls in Computer Science Curriculum Design. *Communications of the ACM*. The CS2023 task-force members' own framing of the constraints on curriculum design. Useful for Part V too.

### AI Systems (ARIN 5360) as the "Product" Relationship

- Denny, P., Leinonen, J., Prather, J., Luxton-Reilly, A., et al. (2024). [Prompt Problems: A New Programming Exercise for the Generative AI Era](https://doi.org/10.1145/3626252.3630909). *SIGCSE '24*. The prompt-problem as a new exercise type. Relevant to thinking about what an assignment in an AI systems course actually is.

- Denny, P., MacNeil, S., Savelka, J., Porter, L., & Luxton-Reilly, A. (2024). [Desirable Characteristics for AI Teaching Assistants in Programming Education](https://arxiv.org/abs/2405.14178). *ITiCSE '24*. [DOI: 10.1145/3649217.3653574](https://doi.org/10.1145/3649217.3653574). Companion on the TA side.

- MacNeil, S., Tran, A., Hellas, A., Kim, J., Sarsa, S., Denny, P., et al. (2023). [Experiences from Using Code Explanations Generated by Large Language Models in a Web Software Development E-Book](https://doi.org/10.1145/3545945.3569785). *SIGCSE '23*. Earlier piece but foundational for the "AI as explanation generator" thread.

### Visualization (CPSC 5320) as the "Collaborator" Relationship

- Chen, X., et al. (2025). [Not Everyone Wins with LLMs: Behavioral Patterns and Pedagogical Implications in AI-assisted Data Analysis](https://arxiv.org/abs/2509.21890). Behavior-grounded study of how technical expertise translates to strategic AI use in a data-analysis course. Technical experts write clearer prompts, provide more context, and use AI proactively to explore alternatives (e.g., "give me a better visualization"). Novices use AI reactively, to unstick immediate blockers. The piece that most directly justifies teaching AI as a collaborator rather than a tutor at the graduate visualization level.

- Bendeck, A., & Stasko, J. (2025). [Evaluating LLMs for Visualization Generation and Understanding](https://arxiv.org/abs/2507.22890). LLMs generate simple charts competently and fail on complex ones. Their visualization literacy is uneven and often relies on pre-existing knowledge rather than actually reading the chart. Useful for grounding the critique-mode material I'm building around the 5320 mode bank.

- Lo, L. Y.-H., Zeng, H., Gotz, D., et al. (2025). [Do LLMs Have Visualization Literacy?](https://arxiv.org/abs/2501.16277). IEEE VIS. Companion piece. The "LLMs lean on priors rather than read the visualization" finding is exactly what a Visual Analytics student needs to notice and name.

- Wongsuphasawat, K., Moritz, D., Anand, A., Mackinlay, J., Howe, B., & Heer, J. (2016). [Voyager: Exploratory Analysis via Faceted Browsing of Visualization Recommendations](https://idl.cs.washington.edu/papers/voyager). *IEEE TVCG*. Pre-LLM vis-recommender. Surfaces charts based on statistical properties of the data. I assign this in C6 of CPSC 5320.

- Moritz, D., Wang, C., Nelson, G. L., Lin, H., Smith, A. M., Howe, B., & Heer, J. (2019). [Formalizing Visualization Design Knowledge as Constraints: Actionable and Extensible Models in Draco](https://idl.cs.washington.edu/papers/draco). *IEEE TVCG*. The constraint-based companion to Voyager. Encodes visualization design knowledge as weighted constraints that a solver can optimize against. Paired with Voyager in C6, for the same reason: grounding students in pre-LLM approaches so they can recognize what an LLM collaborator is and isn't doing when it proposes a chart.

---

## Part IV. The Practitioner's Stance

This part is about the practitioner's relationship to the tool. How to hold yourself in relation to AI once you've accepted it's here, and how to teach that stance to students. The woodworker's disposition toward a new tool: skeptical, playful, continuously recalibrating. This is where craft, aesthetics, the off-distribution thought experiment, and the teaching-a-stance problem all live. The reading below blends the software-engineering literature with the aesthetics-of-design tradition.

One thread worth sitting with, tentatively: CS has always attracted people for a mix of reasons, intrinsic and extrinsic. The salaries and the boom brought many of us in, and a lot of us then discovered the work itself was the good part. If AI is quietly reweighting that mix, the craft and the fun become more central to why anyone stays. Does this inform our teaching at all?

The readings below are lighter on dispositional pedagogy and the craft-tradition canon than this part's title suggests. That's a gap I'm still working on; see "[What's missing, and why](#whats-missing-and-why)" at the end.

### On AI-generated code, legacy code, and what breaks at scale

- Wang, Y., et al. (2025). [Debt Behind the AI Boom: A Large-Scale Empirical Study of AI-Generated Code in the Wild](https://arxiv.org/html/2603.28592). Empirical evidence that AI-assisted development changes how technical debt enters and persists in production systems. Code smells are the most common form of AI-introduced debt and are easy to accept during review.

- Bavota, G., et al. (2025). ["TODO: Fix the Mess Gemini Created": Towards Understanding GenAI-Induced Self-Admitted Technical Debt](https://arxiv.org/abs/2601.07786). The self-admitted technical-debt angle, grounded in GitHub comments that explicitly reference AI tools. A useful corpus for worked examples.

- Sonar's "great toil shift" findings, [February 2026](https://www.sonarsource.com/blog/how-ai-is-redefining-technical-debt). 88% of developers report at least one negative impact of AI on technical debt; 93% also report at least one positive one, with documentation of legacy systems as the most cited benefit. Both-sides pattern is real, and any serious treatment has to hold it.

### On craft, pattern, and the quality without a name

- Alexander, C. (1979). *The Timeless Way of Building*. Oxford University Press. The source for "the quality without a name." Alexander's argument that good form emerges from resolving a system of forces, not from applying an abstract template, is the architectural grounding for the claim that craft is situated. His pattern-language work influenced object-oriented programming (Beck and Cunningham at OOPSLA in the late 80s) and through it much of modern software practice. For readers who haven't read the book, Wikipedia has [a reasonable summary of the QWAN concept](https://en.wikipedia.org/wiki/The_Timeless_Way_of_Building).

- Gabriel, R. P. (1996). [*Patterns of Software: Tales from the Software Community*](https://dreamsongs.com/Files/PatternsOfSoftware.pdf). Oxford University Press. Full text free from Gabriel's site. His translation of Alexander into software terms, including "habitability" as the software analogue of Alexander's quality without a name. I lean on Gabriel's argument that systems have to be conceptually coherent to the minds that maintain them, and that this is what makes composability actually matter.

- Scarry, E. (1999). [*On Beauty and Being Just*](https://press.princeton.edu/books/paperback/9780691089591/on-beauty-and-being-just). Princeton University Press. The aesthetic argument proper. Scarry's claim that beauty presses us toward a greater concern for justice isn't the part I draw on most. What I draw on is her more local claim, that the experience of beauty is the experience of something you cannot imagine otherwise, where every part seems to have had to be exactly so. That "couldn't imagine it otherwise" quality is what scrap solutions and great hacks share with good carpentry, and what AI structurally cannot participate in because AI does not live with its outputs. The stakes aren't ornamental. They're about why some code is a treasure and other code is waste, even when both compile.

### On the off-distribution thesis, lightly

- The METR paper and the Sloan piece on legacy systems (both cited in Part II above) work here too. The weird-code argument is really those findings generalized: AI is strongest on conventional code; our curricular edge is the un-conventional.

---

## Part V. Program Design, and Honest Uncertainty

The closing moves. Program-level decisions (what to keep, what to retire, what to add), the earned argument about non-elite programs possibly being well-positioned for this moment rather than poorly-positioned, and a closing on what is and isn't known. Less pedagogy here, more institutional and economic.

- Bick, A., Blandin, A., & Deming, D. (2024; updated 2025). [*The Rapid Adoption of Generative AI*](https://www.nber.org/papers/w32966). NBER Working Paper 32966. The best available data on adoption rates. Roughly 36-46% of U.S. workers reporting generative AI use at work by late 2025, rapidly climbing. The baseline against which any program-design decision has to be measured.

- Brynjolfsson, E., Li, D., & Raymond, L. R. (2025). [Generative AI at Work](https://doi.org/10.1093/qje/qjae044). *Quarterly Journal of Economics* 140(2), 889-942. The customer-support productivity study. Key finding: gains are largest for initially lower-performing workers, producing skill compression. The empirical piece that most supports (without proving) the possibility that non-elite programs may be in a better position than historically thought, because their graduates are precisely the workers AI most amplifies.

- Acemoglu, D. (2024). [*The Simple Macroeconomics of AI*](https://www.nber.org/papers/w32487). NBER Working Paper 32487. Cited mainly as counterweight to Brynjolfsson et al. The honest picture of aggregate labor effects through 2025 is that they're small, uneven, and genuinely contested.

- International Center for Law & Economics. (2026, February). [*AI, Productivity, and Labor Markets: A Review of the Empirical Evidence*](https://laweconcenter.org/resources/ai-productivity-and-labor-markets-a-review-of-the-empirical-evidence/). A useful overview that synthesizes roughly a dozen of the key labor-market studies from 2023-2026, including the ones above.

- The CS2023 document (linked in Part III) and Simha et al.'s CACM commentary, for program design at the faculty level. The CS2023 AI chapter is useful but too optimistic about scaffolding for novice learning given the Widening Gap evidence. A tension worth sitting with rather than smoothing over.

---

## What's missing, and why

This list isn't comprehensive in several places, and I want to name the gaps:

- **Architecture pedagogy.** The 5600 section is thin because the literature on architecture-courses-and-AI is thin, and because I haven't yet figured out which of the CS2023 systems-development perspectives I most lean on. Plausible candidates include the Fred Brooks / conceptual-integrity tradition and more recent writing on system design interviews as pedagogy. Not settled.

- **Accountability and assessment.** I haven't included the academic-integrity / AI-detection literature because I find most of it misdirected. But I'll need to engage with at least the Sadasivan et al. and Liang et al. detection-limitations papers to earn that dismissal rather than just perform it.

- **The students themselves.** There's a genre of student-voice and student-survey work I've only sampled. Worth a dedicated pass before I'd feel good about the Part V material on non-elite students.

- **The meta-literature.** I've deliberately excluded most of the systematic reviews of systematic reviews because they add little over Prather et al. 2023. May be a mistake if the field stabilizes in the next year.

Whether or not the book happens, the reading list gets better the more eyes are on it. Send me yours.

---

## How this was made

The outline came out of a working session with Claude in mid-April, pressure-testing whether a book on CS ed in the age of AI had a shape worth building out. The reading list didn't exist until this week. Claude did the searches, proposed annotations, and drafted structure. I pushed back on what was too formal, added the aesthetics material for Part IV, and rewrote the framing in my own voice. Links were verified during drafting; any that break on you are on me.

---

*Kevin Lundeen is a teaching professor in the Department of Computer Science at Seattle University, where he teaches computer systems, distributed systems, parallel computing, visual analytics, and AI systems. He is also VP of Software Engineering at OneTouchEMR. Previously, he was a managing director at Goldman Sachs, where he co-created SecDB and Slang. Writing the book is the stretch goal; reading the field is the job.*
