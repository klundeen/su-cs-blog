---
layout: post
title: "Who's the Evil Empire Now?"
subtitle: "A Visual Analytics in-class exercise, designed in a Monday-night session and runnable inside a class meeting, only because the AI is doing real work on both sides"
date: 2026-05-04
author: Kevin Lundeen
author_title: "Associate Teaching Professor, Department of Computer Science"
---

![The bump chart students will build tomorrow, generated from the synthetic dataset. Lower rank means closer to the evil-empire title.]({{ site.baseurl }}/assets/images/evil_empire_bump_chart.png)

Tomorrow my Visual Analytics students walk into an in-class exercise called *Who's the Evil Empire Now?* They'll work in groups, build a bump chart of six tech giants across thirty years, then peel off and each profile one company in depth. Perception against financials. Cross-examination at the end. The exercise scaffolds Saturday's midterm.

What I want to write about is not the design (though the design has its moments), but the fact that this assignment wasn't feasible a year ago. Not feasible for me to *create* on a Monday afternoon, and not feasible for students to *complete* in a single class meeting. AI is doing real work on both sides of it. That changes what an in-class exercise can be.

## What the students do

Each group of three or four gets the same dataset: six companies (Microsoft, Apple, Amazon, Google, Meta, X), thirty-two years (1995–2026), an evolving set of columns reflecting how perception measurement actually changed over those decades.[^schema] Their first deliverable, due at the break, is a bump chart of *evil_rank* over time, built collaboratively by the group, with all six companies on one chart and the rank-1 line at any year being that year's evil empire.

A bump chart of six entities across 32 years is a real piece of viz work. In Tableau or D3 or Vega-Lite or Observable, it's the kind of artifact a competent grad student could build in two to three hours. The constraint here is sixty minutes, group warm-up included. They get there because they're allowed (encouraged) to use AI to write the code while they direct the design. *Make the line for X dashed before 2013 because it wasn't a public company yet. Highlight the rank-1 line in red. Add a year slider.* The student knows what they want; the AI types fast.

Then they pick empires. Each member of the group takes a different one for the second deliverable, due at the end of class. Build a single viz that puts a perception measure next to a financial measure across that company's full era. Defend it in cross-examination. Write three to five sentences on what surprised you in the data, and three to five sentences on which part of the dataset you trust the least.

The cross-examination matters. The chart is a real artifact. Students need to actually render the perception-financial relationship, and a sloppy chart can't be salvaged by a strong defense. But a polished chart whose author can't answer *"what's the most surprising thing in your data?"* fails just as completely. Both the artifact and the defense get graded, because the exam will grade both.

## What the AI lets them do that they couldn't last year

A year ago this would have been three assignments, not one ICE. *Build a bump chart* would have been one homework. *Profile one company* would have been a second. *Defend the choices in writing* would have been a third. Each would have taken a week and the connection between them would have been mostly conceptual.

AI collapses the build time enough that all three motions can happen in a single class meeting. Not because the AI is doing the thinking (students still pick the metrics, still choose the form, still defend the choices), but because the AI removes the *mechanical* friction that used to dominate. Looking up the right Vega-Lite syntax. Wrestling with axis labels. Figuring out how to color-encode rank. The student who knows what they want is no longer gated on whether they can recall the API by heart.

This is exactly the *Use It* tier I wrote about in [the truck post](https://klundeen.github.io/su-cs-blog/2026/03/10/the-ai-knew-it-was-a-truck/).[^tier] The AI is a collaborator. The skill being graded is whether the student can direct it well: whether they catch the sawtooth that isn't seasonality, whether they can tell plausible from correct. That's hard to assess on a homework that gets turned in at midnight. It's much more visible in a class session where I'm walking around and watching.

## What the AI let me do that I couldn't last year

The dataset is synthetic. I built it Monday night.[^synthetic]

That sentence sounds small but it's actually the thing that made the whole exercise possible. I needed thirty years of perception data for six companies covering eras when most of these companies didn't exist or weren't public. There is no real dataset like this. I tried. Harris Poll RQ exists but is paywalled and methodologically inconsistent. Google Trends starts in 2004, outside Microsoft's evil-empire peak. Wikipedia pageviews start cleanly only in 2015. Stitching together a real dataset would have taken a week, and the result would have been so full of gaps and asymmetries that the exercise would collapse for the X group while the Microsoft group breezed through.

So I synthesized it. With Claude. In about three hours.

What that involved: writing a Python generator that produces calibrated curves for each company across the full window, accounting for founding dates, public/private transitions, and the historical inflection points that make the chronology read right. Designing an "evil empire" formula that produces the actual chronology you'd recognize: Microsoft in the antitrust years, Meta during Cambridge Analytica, X in the Musk era. Iterating that formula maybe a dozen times until the rankings came out the way they should. Planting three surprises layered by depth and one red herring, then writing a private answer key documenting where each one lives.

I would not have done this a year ago. I might have done a watered-down version of it (three companies, ten years, a single rough metric), but it wouldn't have been the exercise I'm running tomorrow. The combination of *I can write code that produces real-feeling synthetic data* and *I can iterate on it at conversational speed* is what made the leap from "interesting idea on a napkin" to "actual deliverable artifacts in a Canvas page" something that fits inside a Monday afternoon.

The AI is doing the same thing for me that it's about to do for my students: removing the mechanical friction so the design can move at the pace of the thinking.

## The honesty problem, and the AI policy

I told the students it's synthetic. The Canvas page says so in the third paragraph. Some of them will be irritated by this (*"why didn't you just give us real data?"*), and that question is itself part of the exercise. The honest answer is *because real data doesn't exist for this question, and inventing it lets me grade you on whether you actually looked at what the data shows rather than whether you matched the public narrative.*

The AI policy on the ICE is carte blanche, with the only constraint being that students own what they submit and have to defend it. The AI policy on Saturday's exam is the same, plus a transcript-artifact requirement (export your full conversation and submit it). I built this assignment using the same workflow the students are about to use. I think that matters. It would feel dishonest to assign an AI-permitted exercise that I designed by hand, or to forbid AI on an exam in a class where I've spent the quarter training students on the AI mode bank.

There is a real risk in this kind of exercise that I'm watching for. If the AI does the building too well, the *direction* skill atrophies. The student who tells Claude *"build me a bump chart"* and accepts the first output without iterating is missing the assignment. The cross-examination round is the safeguard. A student who can't defend their choices is one whose AI did the work of selecting them. We'll see tomorrow whether the safeguard does what I want it to.

## How this was made

The exercise itself was built in a roughly three-hour conversation with Claude on Monday afternoon. I drafted the seed idea, audited data sources with Claude, decided to synthesize, iterated the evil-score formula until the chronology read right, planted the surprises, and wrote the Canvas pages in the established Week 6 styling. The conversation went through about eight design pivots, most of which I'll spare you. The pivot I'm proudest of is the move from a money-based size axis to a news-volume-based one. *Empire* in this phrase has always meant *occupying public attention*, not *having the biggest balance sheet*. Once I named that, the rest of the formula fell into place.

This post was drafted later the same evening, in a continuation of the same conversation. I asked Claude for a draft, rejected the first attempt as too long and too inside-baseball, asked for shorter and more above-the-fray, and rewrote large portions of the result. The thesis is mine: *AI made the assignment feasible on both sides*. That reframe is what made the post work. The pivot list, the cross-examination paragraph, and the dataset section are mostly Claude with my edits for tone.

The exam is Saturday. The exercise scaffolds it. I'll write a follow-up if the planted surprises actually got found.

---

*Kevin Lundeen is a teaching professor in the Department of Computer Science at Seattle University, where he teaches visual analytics, computer systems, distributed systems, and AI systems. He is also Principal Architect at OneTouchEMR. Previously, he was a managing director at Goldman Sachs, where he co-created SecDB and Slang. He is restoring a 1911 farmhouse in the Skagit Valley.*

[^schema]: The schema evolves on purpose. Early years (1995–2003) have only Harris-Poll-style reputation scores and news volume. Google Trends columns appear in 2004, Wikipedia pageviews in 2008, social mention scores and regulatory action counts in 2015. A student who tries to plot Google Trends for Microsoft 1998 hits an empty cell and has to confront the fact that *the proxy didn't exist then*. That's a Visual Analytics lesson the dataset teaches without me having to teach it.

[^tier]: [*The AI Knew It Was a Truck. The Other AI Didn't.*](https://klundeen.github.io/su-cs-blog/2026/03/10/the-ai-knew-it-was-a-truck/) CS Perspectives, March 10, 2026. The four-tier framework: Build It, Integrate It, Supervise It, Use It. Visual Analytics sits at the top tier because using AI well *is* the assessment.

[^synthetic]: The generator script, the dataset, and a private answer key documenting the planted surprises are all artifacts of the design session. Faculty colleagues who want a copy can ask me.
