---
layout: post
title: "From ℵ₀ to ℵ₁"
subtitle: "Is the gap between AI and human cognition a difference in degree or a difference in kind?"
date: 2026-03-20
author: Kevin Lundeen
author_title: "Teaching Professor, Department of Computer Science"
---

I had a conversation with Claude the other night that I can't stop thinking about. It started with a simple question about LLM scaling — how big do these things need to be? — and ended up somewhere I didn't expect.

Could be naive, but it seems worth thinking about.

[^cantor]: Georg Cantor proved in 1891 that some infinities are bigger than others. The reals are uncountably infinite (ℵ₁, aleph-one); the naturals are countably infinite (ℵ₀, aleph-null). The proof fits on a napkin and it broke mathematics. See any good analysis textbook, or Courant and Robbins, *What Is Mathematics?* (Oxford, 1941).

---

## Will they ever know everything?

The scaling laws research[^scaling] found that LLM performance improves as a power law with both parameter count and training data, but with diminishing returns on each. The curves don't flatten completely in the ranges we've tested, but they're clearly bending. So I asked: is there some asymptotic convergence? Some point where more training doesn't matter?

Think of it like lossy compression.[^jpeg] A JPEG encodes a photograph at various quality levels. More bits gives you a better reconstruction, but doubling the file size doesn't double the quality. Parameters work similarly — they're not storing facts like a database. They're storing statistical relationships, the way a JPEG stores frequency coefficients rather than individual pixels.

Here's where it gets interesting. There's a difference between *understanding* and *facts*. Understanding compresses well — once you grasp Newtonian mechanics, every new projectile problem is redundant. But the name of a beetle, where it was found, what it eats — that's essentially incompressible. Every fact is its own thing. You can't derive the name of a species from first principles.

So you'd hit a regime where the model has enough parameters to capture the patterns and reasoning structures — the framework — but runs out of room for the encyclopedia. It would understand entomology perfectly but not tell you about the specific beetle discovered on a Tuesday in 2847. This actually matches a real failure mode: I've watched Claude get the logic of an argument exactly right and hallucinate the citation. The relational knowledge compressed fine; the specific fact didn't survive.

![A museum drawer of pinned beetle specimens. Each one is its own fact — unique, incompressible, irreducible to first principles. Understanding how beetles work compresses beautifully. Knowing which beetle this is does not.](https://upload.wikimedia.org/wikipedia/commons/a/af/Display_drawer_1a_%2817407586030%29.jpg)
*"God has an inordinate fondness for beetles." — attributed to J.B.S. Haldane, probably apocryphal, definitely true. Photo: [Wikimedia Commons](https://commons.wikimedia.org/wiki/Category:Beetle_collections).*

The practical answer is retrieval-augmented generation — don't memorize every beetle, learn how beetles work and look up the specific one when you need it. That's what we're building in my AI Systems course.[^rag]

But here's the question I can't shake: is there a convergence point for the *framework itself*? If there is, that's a bold claim about human thought — it would mean the structure of human reasoning is finite. A finite set of ways that causes relate to effects, that arguments get structured, that narratives unfold. At some parameter count you'd have a model that has essentially "learned thinking." After that, more parameters only buy you beetle storage.

[^scaling]: Kaplan et al., "Scaling Laws for Neural Language Models," *arXiv*, 2020; Hoffmann et al., "Training Compute-Optimal Large Language Models" (the Chinchilla paper), *arXiv*, 2022. The Chinchilla work showed most large models were undertrained relative to their parameter count.
[^jpeg]: This isn't just an analogy — it's surprisingly close to what's actually happening. JPEG applies a discrete cosine transform to decompose an image into frequency components, then quantizes the high-frequency coefficients (fine details) more aggressively than the low-frequency ones (broad structure). The result: you keep the overall shape and lose the texture. LLM training does something eerily similar — gradient descent on a cross-entropy loss preferentially encodes high-frequency patterns (common reasoning structures, grammatical rules) and lossy-encodes the long tail (specific facts, rare names, that one beetle). The analogy runs deep enough that some researchers have formally connected neural network generalization to rate-distortion theory from information theory. See Shwartz-Ziv and Tishby, "Opening the Black Box of Deep Neural Networks via Information," *arXiv*, 2017 — the information bottleneck paper that started a lot of this thinking.
[^rag]: RAG: Retrieval-Augmented Generation. Don't try to know everything — learn how to think, then look things up. Lewis et al., "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks," *NeurIPS*, 2020.

## AlphaGo converged. Language might not.

AlphaZero — the version that learned Go purely from self-play — did reach a point where its improvement leveled off dramatically. Its Elo rating climbed steeply and then flattened into something that looks like an asymptote. And Go has a finite, deterministic rule set. There *is* a theoretically perfect player. So if convergence is possible anywhere, it's there. And it seems to have roughly converged.

Language is the messier version. The game board keeps expanding. The rules are fuzzy. New domains keep getting invented. You're asking whether a game with no fixed rules and an ever-growing board still has a learnable meta-strategy.

And then I realized: there's something one-dimensional about next-token prediction that might be the deeper problem. Not just "will it converge?" but "is convergence even the right frame?"

That's where Cantor[^cantor] came in.

## The bottleneck

Next-token prediction is serial. One word, then the next, then the next. The transformer has attention — it can look at everything at once — and the training is beautifully parallelized. I teach parallel computing; I appreciate the elegance. But at inference time, generation is autoregressive.[^vaswani] One token. Then one more. The parallelism is in how the model *considers*. Not in how it *creates*.

That's not an engineering constraint you can optimize away. Every internal state, no matter how rich the attention patterns, collapses into a probability distribution over the vocabulary for a single next token.

Compare that to how I actually think about a problem. When I'm designing a CUDA kernel, I'm holding the memory layout, the thread geometry, the warp divergence, and the data dependencies all at once. The solution comes from the *shape* of the whole structure, not from predicting the next word in a description of it. Or forget CUDA — when I'm hosting a party at the farmhouse, I'm tracking three conversations, reading body language, noticing someone's glass is empty, remembering that two guests have a history, and thinking about when to bring out the next course. That's not sequential. That's a high-dimensional state I hold all at once and act from holistically.

Token prediction optimizes for *plausible continuation*. Thinking often asks *what's the shape of the whole thing?* Only one of those lives on a line.

[^vaswani]: Vaswani et al., "Attention Is All You Need," *NeurIPS*, 2017. The transformer paper. The parallel attention was the innovation. The autoregressive generation is the bottleneck.

## The question Cantor answers

So we have two problems stacked on top of each other. First: token prediction is one-dimensional. Second: even if you could converge on the reasoning framework, human culture keeps generating new levels of organization that might expand the framework faster than any model can learn it.

Is the gap between what LLMs do and what human minds do a difference in *degree* — more parameters, more data, wait long enough — or a difference in *kind*, the way the real numbers are a fundamentally different size of infinity than the integers? You can't get from the naturals to the reals by adding more naturals. Is there an analogous barrier?

Cantor proved the reals can't be listed. His diagonalization argument: for any proposed enumeration of all the reals, you construct one that's not on the list by differing from the *n*th entry at the *n*th decimal place. The structure of what you're trying to capture exceeds any sequential enumeration.[^diagonal]

![Cantor's diagonal argument: take any proposed list of real numbers, read the diagonal digits, change each one, and you've constructed a number that can't be on the list. The reals are a bigger infinity than the naturals.]({{ site.baseurl }}/assets/images/cantor-diagonal.svg)

Maybe cognition has that property. For any sequential description of what a mind is doing, there's something that escapes it — not because you haven't described *enough*, but because sequential description is the wrong medium. The way insight arrives whole. The way you suddenly see the shape of a proof. Maybe those are the diagonalization — the thing that always escapes the listing.

Or maybe not. Maybe cognition just *feels* high-dimensional from the inside but is really an elaborate computation that could be serialized. Consciousness might be the illusion of ℵ₁ experienced by a process that's actually ℵ₀. Penrose argued something like this in *The Emperor's New Mind* (1989) — that consciousness involves non-computable quantum processes. Most people think he's wrong about the mechanism. But the intuition that something's being left out of the computational picture keeps coming back.

> **We don't know which cardinality we are.**

[^diagonal]: The diagonal argument is also the template for Turing's halting problem proof (1936) and Gödel's incompleteness theorem (1931). Same deep structure: assume you can enumerate everything, construct something that escapes. It keeps showing up.

## Multiple orders of random

The phrase "multiple orders of random" isn't mine. It's my sister's, from her one and only peyote experience, decades ago, walking the Arizona desert. She was examining desiccated cactus skeletons — ordered layers upon layers of seemingly random patterns, each level organized by the level above it. Patterns within patterns within patterns. No single layer captures the whole.

![A cholla cactus skeleton — the lattice-within-lattice structure that caught my sister's eye. Each hole is unique, but the pattern of holes is organized, and the pattern of patterns is organized differently still. Multiple orders of random.](https://upload.wikimedia.org/wikipedia/commons/d/d6/RanchoPuntaSanCristobal07.JPG)
*Cholla cactus skeleton. Photo: [Wikimedia Commons, CC BY-SA 4.0](https://commons.wikimedia.org/wiki/Category:Cholla_Cactus_Garden). If you've never seen one in person, they're worth the trip.*

I've always loved that image because it describes human societies. People form families. Families form clans. Clans form nations. Each level generates dynamics that aren't derivable from the level below.[^anderson] Knowing everything about individual psychology doesn't tell you how a family works. A diplomat negotiating a treaty is operating in a space shaped by personal psychology, family honor, tribal loyalty, national interest, and global economics all at once. And the levels interact — a single person's decision reshapes a family, shifts a community, tips an election, changes a nation's foreign policy.

An individual mind has fixed capacity. But culture — the collective, multi-generational thing — keeps growing. Nobody holds all of Western law, or all of mathematics, or all the social knowledge embedded in a language. Culture is distributed cognition at a scale that exceeds any individual, and it keeps generating new structure faster than any system can encode it.

Maybe individual cognition is ℵ₀ too, and *culture* is ℵ₁. A model might converge on what any individual can do — that finite reasoning framework I was wondering about earlier. But culture never converges because it keeps inventing new levels of organization, new kinds of games at scales we haven't seen. A thousand more years of civilization doesn't just produce more beetles. It produces new *kinds* of beetles, organized in ways that require new reasoning structures to understand. Park et al. put 25 LLM agents in a simulated town — they gossiped, formed relationships, organized a party.[^park] Entertaining. But the agents were simulating social behavior, not generating new social structures. They gossiped because GPT knows what gossip looks like, not because gossip emerged from first principles.

Nobody has seen multi-agent AI produce something that crossed a cardinality boundary.

[^anderson]: Philip Anderson, "More Is Different," *Science*, 1972. At each level of complexity, fundamentally new properties appear that aren't deducible from below. Particle physics doesn't predict chemistry. Chemistry doesn't predict biology.
[^park]: Park et al., "Generative Agents: Interactive Simulacra of Human Behavior," *UIST '23*, ACM, 2023.

## Goals change everything

Here's the structural problem. Token prediction is reactive. It answers "what would come next?" It has no notion of *I'm trying to get somewhere*. There's no *there*.

A goal is architecturally different. The system evaluates its distance from a target state. It can reject plausible continuations in favor of less obvious ones that serve the goal. It goes uphill against the likelihood gradient because it has a reason to.

AlphaGo.[^alphago] It wasn't predicting the next move a human would play. It was evaluating board states against a goal — winning — and choosing moves that maximized its probability of getting there, even when the moves looked insane to experts. Move 37 against Lee Sedol: no human would play it, a token predictor trained on human games would assign it near-zero probability, and it was brilliant. The goal gave the system a reason to leave the distribution of human play and go somewhere new.

But Go has a clean win condition. The board is observable. You can simulate millions of games. Try expanding the goal to "advance physics" or "maximize human flourishing." How do you write the loss function[^loss] for a unified field theory?

This is where I had a thought that might be naive but I'll say it anyway: couldn't we start smaller? Constrained domains with well-defined success criteria. Find room-temperature superconductors. Prove or disprove the Riemann hypothesis. Design a carbon capture process that works at scale. Each one is bounded, verifiable, enormously valuable. An AI trying to unify quantum mechanics and general relativity isn't going to accidentally paperclip[^paperclip] the universe. The domain is too narrow for the objective to go sideways.

Maybe the mistake in AI discourse is jumping to the godhood question when there's enormous value in bounded-goal territory we arguably already know how to build. We got distracted by the eschatology when the real work is giving AlphaGo a physics problem.

[^alphago]: Silver et al., "Mastering the game of Go with deep neural networks and tree search," *Nature*, 2016. And then "Mastering the game of Go without human knowledge," *Nature*, 2017 — AlphaGo Zero, which taught itself from scratch.
[^loss]: A loss function tells a model what "wrong" looks like — the distance between prediction and correct answer. The model minimizes the loss. The problem: for the most interesting questions, we can't define "correct answer."
[^paperclip]: Bostrom, *Superintelligence* (2014): an AI told to make paperclips might, if powerful enough and literal-minded enough, convert all matter in the universe into paperclips. It's probably wrong about how this plays out. But it's useful as a limit case.

## Copy nature's homework

Current AI has no mutation rate. Training optimizes for likelihood on existing data. The whole architecture is selection pressure *against* the unexpected. It produces competent mediocrity reliably and genuine novelty rarely.

Thousands of poets write badly so one original voice emerges. Thousands of physicists chase dead ends so one stumbles onto something. The waste is the point. Nature figured this out billions of years ago.

Ken Stanley showed that rewarding *novelty* instead of fitness toward a fixed goal actually produces better solutions in many domains, because it avoids the local optima that optimization gets stuck in.[^stanley] His book with Joel Lehman, *Why Greatness Cannot Be Planned* (2015), argues that ambitious objectives are *harder* to reach when you aim at them directly. You need stepping stones you can't predict. It maps onto how scientific progress actually works — the important discoveries are usually not the ones anyone was looking for.

But the money is going to making the token predictor better at commercial tasks. Chatbots, code generation, ad targeting. The novelty-search work, the bounded-goal scientific work, the architecturally different approaches — tiny fraction of the investment. The world enamored with its new toy is mostly using it to autocomplete emails faster.

[^stanley]: Lehman and Stanley, "Abandoning Objectives: Evolution Through the Search for Novelty Alone," *Evolutionary Computation*, 19(2), 2011. Stanley is currently SVP of Open-Endedness at Lila Sciences. His research agenda is one of the most interesting things in AI that the mainstream isn't paying attention to.

## The partnership

So where does this leave us? I think the interesting near-term picture isn't AI replacing human thought. It's AI holding the ℵ₀ while humans contribute the ℵ₁.

The model can only converge on what we've already thought. It's a magnificent mirror, but a mirror doesn't generate light. The genuine creative leaps — the things that add new structure rather than reorganize existing structure — might be the thing no amount of scaling produces.

That makes AI the most extraordinary *assistant* to human creativity that's ever existed. It holds the entire accumulated framework so a human thinker doesn't have to, freeing them to focus on the leap. A vast reference library with deep structural understanding, in service of a mind that can do the one thing it can't.

That's a partnership, not a replacement. And frankly, it's a nicer future than the paperclip maximizer.

## What I don't know

I want to be honest: this is a metaphor, not a proof. Cantor's theorem is mathematically precise. The claim that cognition is a higher cardinality than token prediction is speculative. Maybe the gap is real. Maybe it's illusory and cognition is just a very elaborate ℵ₀ that feels transcendent from the inside. I have days where I suspect I'm not even that complicated.

But the framing clarifies the stakes. If it's a difference in degree, more scale gets us there eventually. If it's a difference in kind, no amount of parameters crosses the barrier. You'd need something architecturally different, and nobody knows what that looks like.

Either way, the practical work is the same. Build bounded, goal-directed systems. Treat AI as a partner. Teach students to verify, to understand, to tell confident from correct.

And maybe, along the way, find out which cardinality we actually are.

## How this was made

This started as a late-night conversation with Claude. I was poking at the convergence question and the one-dimensional feeling, and at some point I said "aleph-0 and aleph-1" — and that turned out to be the frame that made everything click. We chased the analogy for an hour through societies, AlphaGo, evolutionary biology, and whether culture is the higher infinity. It was genuinely productive, which is interesting evidence about the ℵ question, though I'm not sure which direction it points.

I asked Claude to turn the conversation into a blog post. The first draft was smooth and confident — the voice of someone who knows exactly what they think. I rewrote it to sound more like someone who had an interesting conversation and is still chewing on it. The peyote-and-cactus origin story is real. My sister really did walk the Arizona desert once and come back with that image. Some of the best ideas come from people paying attention to the wrong thing.

---

*Kevin Lundeen is a teaching professor in the Department of Computer Science at Seattle University, where he teaches parallel computing, distributed systems, and AI systems. He is also VP of Software Engineering at OneTouchEMR. Previously, he was a managing director at Goldman Sachs, where he co-created SecDB (Goldman's trading and risk management system) and [Slang](https://en.wikipedia.org/wiki/Slang_(programming_language)) (a proprietary language similar to Python). He is 66 years old and started programming with Fortran on punched cards, which means he has been watching computers get smarter for longer than most people reading this have been alive. He is not yet convinced they've caught up.*
