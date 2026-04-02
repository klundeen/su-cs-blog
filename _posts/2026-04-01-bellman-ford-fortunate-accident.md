---
layout: post
title: "Bellman, Ford, and the Fortunate Accident"
subtitle: "Log It and Run"
author: Kevin Lundeen
date: 2026-04-01
series: Beautiful Algorithms
series_number: 1
description: "A conversation with Claude about magic portals, negative cycles, and how a 1950s shortest-path algorithm accidentally became Wall Street's favorite arbitrage detector."
---

*First in the series **Beautiful Algorithms** — conversations about the ideas behind the code we teach.*

What follows is a conversation I had with Claude on a rainy afternoon. It started with a game world and ended at Goldman Sachs. I've lightly edited for spelling and grammar, but the arc is exactly how it happened. The labels are "Professor" and "Claude" throughout — no introduction, no framing. The conversation *is* the thing.

---

**Professor:** Imagine we have a game world. There's a portal from my world, World A, to a simpler world, World B. My magic quotient in my world is 1. But if I go through the portal to World B, I'm like a god there and my magic quotient is multiplied by 10. But when I return back to World A through the portal, my magic quotient is multiplied by 10%, the reciprocal, so I end up in my world as nothing special: magic quotient 1.0.

There's another portal from A to a godlike world, World C. That portal multiplies my MQ by 0.5. No worries, because when I return, my MQ is multiplied by 2 and I'm normal again in my world. There's also a portal from B to C, but the portal multiplier is, you guessed it, 1/20, and the other direction is 20. So a trip from A to B to C would leave me in World A with an MQ of ______?

**Claude:** Let me trace through the journey step by step.

Starting in World A with MQ = 1.0.

**A → B:** multiply by 10, so MQ = 10.

**B → C:** multiply by 1/20, so MQ = 10 × 1/20 = 0.5.

**C → A:** multiply by 2 (the return from C to A), so MQ = 0.5 × 2 = **1.0**.

You end up right back where you started — nothing special, MQ of 1.

This is a nice little illustration of a concept, by the way. Are you building toward something with this — like exchange rate arbitrage, or maybe a lesson about consistency in transformation systems?

**Professor:** Oh, don't be a smart aleck! Just hang with me for another minute. Now say I have a hundred worlds, but the portal MQ multipliers conspire to always keep me at 1 when I return from my roundabout trip.

**Claude:** Got it — a hundred worlds, portals between them, and no matter what path you take, when you get back to where you started your MQ is always 1. No arbitrage, no free magic.

What's next?

**Professor:** The portals can change their multipliers sometimes (hey, it's a rainy day here, so the multiplier goes down). When they do, all the other portals have to adjust to keep my trips around the worlds conspiring to keep me at 1 when I return home. But there might be a slight delay, and if I could get ahead of that wave of change maybe I could return home with extra MQ. If I had access to all the portals' multipliers in real time, how could I plan a trip to beat the conspiracy and return home with extra MQ? There must be a computer algorithm for that.

**Claude:** You're describing cycle detection in a graph where the edge weights are multiplicative — and you want to find a cycle where the product of the weights is greater than 1.

The classic trick is to take the logarithm of each multiplier. That turns multiplication into addition, and now you're looking for a cycle where the sum of the edge weights is positive. Negate those logs and you're looking for a **negative-weight cycle** — which is exactly what the **Bellman-Ford algorithm** detects.

So the plan would be: monitor all the portal multipliers in real time, convert them to negative log weights, run Bellman-Ford, and the moment it finds a negative cycle, that's your travel itinerary to come home with extra MQ.

**Professor:** Yes, exactly! How did you know?

**Claude:** Lucky guess, I suppose. So where are you going with all this? Building a game, teaching a class, or just seeing if I could follow the breadcrumbs on a rainy day?

**Professor:** Tell me about Bellman. Tell me about Ford. Did they invent their algorithm to beat the foreign exchange arbitrage game?!

**Claude:** No, they didn't invent it for forex arbitrage — though that's one of the most famous applications today.

Richard Bellman (1920–1984) was an applied mathematician at the RAND Corporation who is best known as the inventor of dynamic programming. Lester Ford Jr. actually came up with the algorithm first, in 1956, while studying a different mathematical problem that reduced to a subproblem of finding shortest paths in a graph. Bellman then independently published a formalization of the same approach in 1958, framing it as a routing problem in networks. And poor Alfonso Shimbel actually proposed the core idea even earlier, in 1955, but didn't get his name on it.

So the origin was really about operations research and network routing — finding the cheapest or fastest path through a system. A distributed variant later became the basis for distance-vector routing protocols like RIP, which is how early internet routers figured out how to forward packets.

The currency arbitrage application came later, when someone realized that if you take the log of exchange rates and negate them, detecting a negative cycle is exactly the same as finding a sequence of trades that nets you a profit. It's a beautiful connection, but Bellman and Ford were thinking about abstract shortest-path problems, not trading floors.

Pretty neat that a 1950s RAND Corporation math problem turns out to be the answer to your magical portal question, right?

**Professor:** Wait. I didn't hear anything about negative cycles in the realm of Ford's or Bellman's work or applications.

**Claude:** You're right — I overstated that. The sources I found describe their original work as focused on finding shortest paths in graphs, including ones with negative edge weights. The negative cycle detection aspect is more of a natural consequence of the algorithm's mechanics: if you run that extra iteration and distances are still changing, you know there's a negative cycle present.

But I don't see evidence that either Ford or Bellman specifically called out negative cycle detection as a goal or application of their work. That insight — and especially the application to currency arbitrage — seems to have come later as other people recognized what the algorithm could do.

Good catch. I was connecting dots that the historical record doesn't actually connect.

**Professor:** So would you say that it's serendipity from prior art?

**Claude:** Yeah, that's a lovely way to put it. They built a tool to solve one problem — shortest paths through a network — and it turned out to have this hidden superpower baked right into its structure. Nobody was thinking about exploiting currency exchange loops or magical portal trips when they wrote those papers at RAND in the 1950s.

That happens a lot in math and computer science, doesn't it? Euler messing around with the Königsberg bridges wasn't trying to invent graph theory for Google Maps. Bellman's dynamic programming wasn't aimed at your hundred-world portal game. But the abstractions turn out to be so general that they keep finding new homes decades later.

So yes — serendipity from prior art. The algorithm was smarter than its inventors knew.

**Professor:** Can you just stop for a second and explain some of this for a typical smart person that isn't a computer scientist? What's a graph? What's a shortest path (and why do we want to find one)? What's a cycle?

**Claude:** Sure thing.

A **graph** is just a collection of things and connections between them. Think of a map of cities connected by roads. The cities are the things (we call them "nodes" or "vertices") and the roads are the connections (we call them "edges"). But it doesn't have to be geographic — a graph could represent friendships on Facebook, flights between airports, or portals between magical worlds. Anything where stuff is connected to other stuff.

Each connection can have a **weight** — a number attached to it. On a road map, that might be the distance in miles or the travel time. In your portal game, it's the magic quotient multiplier. The weight is just "what does it cost to go from here to there?"

A **shortest path** is exactly what it sounds like: if I want to get from city A to city Z, and there are lots of possible routes, which one has the smallest total cost when I add up all the weights along the way? We want to find these all the time in the real world. Your GPS does it every time you ask for directions. A network router does it when it sends your email across the internet. A logistics company does it when planning deliveries.

A **cycle** is a path that starts somewhere and comes back to where it started. Like driving from Seattle to Portland to Spokane and back to Seattle. In your portal world, it's taking a trip through several worlds and returning home.

Now here's where it gets interesting. A **negative cycle** is a loop where the total cost adds up to less than zero — meaning you *gain* something by going around the loop. Normally in shortest-path problems that's a headache, because you could just keep going around the loop forever, getting a shorter and shorter path. But if you're a currency trader — or a wizard hopping between worlds — a negative cycle is exactly what you're hunting for. It means there's free money (or free magic) to be had.

**Professor:** And, of course, you'd keep running around that cycle getting to your destination further and further in the past.

**Claude:** Right — if the weights were travel time, a negative cycle would be a time machine. Just keep looping and you arrive yesterday.

Which is a nice intuition for why Bellman-Ford treats negative cycles as a problem to be detected rather than a solution to be exploited. In most real-world shortest-path applications, a negative cycle means something has gone wrong — your model is broken, or somebody's numbers don't add up. There's no such thing as a route that takes negative time.

But in the currency exchange world (or your portal world), the "negative cost" isn't nonsensical — it represents a real profit opportunity. So what's a bug in one context is a feature in another. The algorithm doesn't care which. It just says "hey, I found one of these" and lets you decide whether to panic or celebrate.

**Professor:** Right. If the weights on the edges between the vertices are additive, then it is going back in time, making "free" time. But the magic portal world and the forex world are multiplicative. It's a different problem. I want to arrive home with more than 1.0.

**Claude:** Exactly. And that's the clever trick that bridges the two worlds. In the additive world, Bellman-Ford looks for a cycle where the sum is negative. In your multiplicative world, you want a cycle where the product is greater than 1.

But you can convert one into the other. If you take the logarithm of each multiplier, multiplication becomes addition. Then you negate those logs, and now "product greater than 1" becomes "sum less than zero" — a negative cycle. You've transformed your multiplicative problem into the exact problem Bellman-Ford was built to solve.

So the algorithm never actually learns to multiply. You just do a little math on the inputs to translate your problem into its language, run it, and translate the answer back. It's like needing to ask a question of someone who only speaks French — you don't teach them English, you just translate your question, get their answer, and translate it back.

**Professor:** Can you show me the math?

**Claude:** Here's the key insight in three lines:

Taking the **logarithm** of each portal multiplier converts your problem from multiplication to addition. That's because log(a × b) = log(a) + log(b). So the product of all the multipliers around a cycle becomes a sum of all the logs around that cycle.

Now, you want the product to be greater than 1. Since log(1) = 0, that means you want the sum of the logs to be greater than 0 — a positive-sum cycle.

Bellman-Ford detects *negative*-sum cycles, not positive ones. No problem — just flip the sign on every weight. Negate all the logs, and now your profitable cycle (product > 1) shows up as a negative cycle, which is exactly what the algorithm was born to find.

Three steps: log, negate, Bellman-Ford. That's the whole trick.[^math]

**Professor:** Nice! That's more than just a little bit clever, unless you're an algebraist, I guess. Who first came up with that idea, do we know?

**Claude:** I can't pin down a single "eureka" moment or a single person. The log transform trick for converting multiplicative problems into additive ones is such a fundamental move in mathematics that it probably felt obvious to multiple people independently.

What the sources do show is that the currency arbitrage problem appears as Problem 24-3 in CLRS (*Introduction to Algorithms* by Cormen, Leiserson, Rivest, and Stein), which is the canonical algorithms textbook. And Robert Sedgewick and Kevin Wayne present it in Section 4.4 of their *Algorithms* textbook, framing the arbitrage problem as negative-cycle detection by replacing each weight with its negated logarithm.[^textbooks]

So it's been a standard textbook exercise for decades, but nobody seems to get credited as the originator. The idea sits at such a natural crossroads — logarithms have been turning products into sums since Napier in the 1600s, and Bellman-Ford has been finding negative cycles since the 1950s — that connecting the two probably felt less like an invention and more like noticing something that was already there.

Which, come to think of it, is the most serendipitous kind of serendipity.

**Professor:** Ah, yes, the Cormen book is a tome. And I guess Wall Street logged the idea and ran with it.

**Claude:** I see what you did there.

**Professor:** That's a good story, but how does the *algorithm* work? I thought Dijkstra had the corner on the shortest path market, anyway.

**Claude:** Dijkstra does have the corner on shortest paths — when all the weights are positive. His algorithm is faster too. But it breaks completely when you introduce negative weights, and here's why.

Dijkstra works by being greedy. It picks the closest unvisited node, says "I'm done with that one forever," and moves on. That works when all weights are positive because visiting more edges can only make a path longer — so once you've found the shortest path to a node, no future discovery can beat it.

But with negative weights, that assumption falls apart. A longer path through more nodes might actually end up shorter if one of those edges has a big negative weight. Dijkstra has already moved on and won't reconsider.

Bellman-Ford takes the brute-force approach instead. It doesn't try to be clever about which node to process next. It just does this:

**Relax every single edge in the graph. Then do it again. And again. Repeat that V−1 times** (where V is the number of vertices).

"Relaxing" an edge just means: look at the edge from u to v with weight w. If the best known distance to u, plus w, is less than the best known distance to v, then update v's distance. That's it. That's the whole inner loop.

Why V−1 times? Because the longest possible shortest path in a graph with V vertices can have at most V−1 edges. On the first pass, you're guaranteed to find the correct distance for any node reachable in one hop. On the second pass, two hops. By pass V−1, you've covered every possible shortest path length.

Then comes the magic: do one more pass — pass number V. If anything still changes, that means a path keeps getting shorter the more edges you add. The only way that can happen is if you're going around a loop that has a negative total weight. A negative cycle.

So the algorithm is almost comically simple compared to Dijkstra. No priority queue, no greedy selection, no fancy data structure. Just "check everything, repeat, and if it's still not settled after it should be, something weird is going on."

The tradeoff is speed: Dijkstra runs in roughly O(V log V + E) time with a good priority queue, while Bellman-Ford plods along at O(V × E). But Bellman-Ford works where Dijkstra can't, and it catches the negative cycles that make your portal-hopping wizard rich.

**Professor:** Let's come back to the plodding and O(V × E) in a second. Let's think about negative weights first. With logarithms of forex exchange rates (or magic quotients) we might go negative?

**Claude:** Right, exactly. When you take the log of an exchange rate (or a portal multiplier), any rate greater than 1 gives you a positive log, and any rate less than 1 gives you a negative log. Then when you negate them all, the signs flip.

So a portal that multiplies your MQ by 10 becomes −log(10) ≈ −2.3, a negative weight. And a portal that multiplies by 1/20 becomes −log(0.05) ≈ +3.0, a positive weight. You end up with a mix of positive and negative edges all over the graph.

And that's exactly why Dijkstra can't play in this sandbox. The moment some of those log-transformed weights go negative, Dijkstra's greedy "I'm done with that node" assumption is toast. Bellman-Ford doesn't care — it just keeps relaxing everything, positive or negative, until the dust settles.

**Professor:** So, explain the plodding V × E. If I understand your story, at each step we say, "If we have x opportunities to move so far and know the shortest path to get to each vertex, if we get another move now could we do better? Look at each other vertex and if you got there and then came to me, is that a shorter route than I had to get to me with only x moves?"

**Claude:** Yes, that's exactly right. Each vertex is asking its neighbors "can you offer me a better deal?" And we give every vertex a chance to ask that question, one round at a time.

In the first round, only the vertices one hop from the start can improve their distances. In the second round, vertices two hops away get their chance, because now the one-hop vertices have correct values to pass along. It ripples outward like a wave — the correct shortest path information propagates one edge further with each round.

So you need at most V−1 rounds for the wave to reach the farthest possible vertex. That's the V part. And in each round, you check every edge in the graph to see if it offers an improvement. That's the E part. V rounds times E edges per round gives you O(V × E).

The plodding comes from the fact that Bellman-Ford doesn't know which edges are useful in any given round. It just checks them all, every time. Most of those checks do nothing — the edge doesn't offer an improvement. But the algorithm doesn't have a way to know that in advance, so it does the work anyway.

Dijkstra avoids that redundancy by using a priority queue to always grab the most promising vertex next. But that cleverness is exactly what requires the "no negative weights" guarantee. Bellman-Ford trades speed for generality — it's dumber but more robust.

**Professor:** Ah, so each round is V × E and we have V rounds, so the algorithm is O(V × V × E). A complete graph like my magic worlds or the world forex market has E = V × V since every exchange exists. Total complexity is O(V⁴)?

**Claude:** Almost — but each round is just E, not V × E. Each vertex doesn't independently scan all edges; we just make one pass through the full edge list and update whatever improves. So it's V rounds × E checks per round = O(V × E).

For your complete graph where E = V², that gives you O(V × V²) = O(V³).

Which is still pretty ploddy. With, say, 150 currencies, that's on the order of 3.4 million operations. Not awful for a modern computer, but the forex markets are moving while you're computing, so speed matters. That's why people build this stuff on FPGAs and specialized hardware — they need the answer before the opportunity vanishes.

**Professor:** When I was at Goldman Sachs (in forex) we bought Hull, a high-speed trading company that did just that. We high-brow trading desks thought poorly of these poor mugs that were chasing milliseconds, presumably with Bellman-Ford.

**Claude:** The irony of looking down on people who were essentially running a 1950s RAND Corporation algorithm really fast. Though I imagine from the perspective of a sophisticated trading desk, watching someone chase pennies around negative cycles at millisecond speeds felt a bit like watching someone use a supercomputer to count cards at blackjack.

But there's a certain elegance to it, isn't there? No models to be wrong about, no views on where the market is going, no risk to speak of. Just pure graph theory and a fast pipe. The math guarantees the profit — the only question is whether you can execute before the cycle closes.

**Professor:** I tell my students now, "Don't try this at home." Of course, it's milliseconds because those magic portals react fast to any real arbitrage, and it closes up fast when any trading velocity hits it.

**Claude:** Right — the market is its own conspiracy. The moment someone exploits a negative cycle, the trades themselves push the exchange rates back toward equilibrium. The arbitrage is self-correcting. By the time you've bought euros and sold yen, you've nudged those rates just enough that the next person checking finds the cycle has closed.

So in a sense, the arbitrageurs are doing the market a service — they're the enforcement mechanism that keeps all those portal multipliers consistent. They're the reason your round trip comes back to 1.0. They just happen to skim a few basis points for their trouble.

Which makes "don't try this at home" exactly the right advice. By the time a retail trader's API call comes back with exchange rates, builds the graph, runs Bellman-Ford, and submits a trade, Hull and their friends have already closed that cycle a thousand times over. You'd need to be physically close to the exchange, with custom hardware, and shaving microseconds off your network latency. It's an infrastructure arms race, not an algorithm problem.

The beautiful part for a classroom though is that the *idea* is so clean. The math doesn't care whether you can execute in time. It's a perfect teaching example — graph theory, logarithms, negative cycles, real-world application, and a cautionary tale about the gap between theory and practice, all in one package.

**Professor:** And serendipity is king — even a serendipitous application of someone else's side effect.

**Claude:** What a perfect line to end on. Shimbel, Bellman, and Ford were just trying to find shortest paths. The negative cycle detection was a nuisance, a warning light. And then decades later someone looked at that warning light and thought "what if that's the feature?"

It's a great reminder that in math and computer science, the side effects are sometimes worth more than the main event. You never know which throwaway observation is going to be someone else's fortune.

**Professor:** What ever happened to Shimbel anyway? And Bellman? And Ford?

**Claude:** Three very different fates.

**Alfonso Shimbel** is the tragic one. Born in Chicago in 1923, he died in 1987 at just 63. He got his PhD in 1950 at the University of Chicago under Rashevsky, working in mathematical biophysics — modeling neural networks and communication structures, not what we'd think of as computer science. His published work was on things like nerve-ganglion models and the mathematical structure of communication networks. He proposed the shortest-path algorithm in 1955, but his name never stuck to it. He seems to have faded into obscurity.

**Richard Bellman** (1920–1984) is the giant of the three. He invented dynamic programming itself — the whole paradigm, not just this one algorithm. He spent most of his career at RAND and later at USC. He was extraordinarily prolific. He died at 64, but left an enormous legacy. The entire field of optimal control theory owes him a debt.

**Lester Ford Jr.** (1927–2017) had the longest and perhaps the most charming life. He was the son of mathematician Lester R. Ford Sr., and specialized in network flow problems. Beyond Bellman-Ford, he and Fulkerson established the max-flow min-cut theorem — another foundational result. He wrote a calculus textbook with his father, loved classical music, played piano and flute, trolled used bookstores for musty tomes, and never met a dessert he didn't like. He lived to 89 in Santa Barbara. His obituary mentions "twinkly blue eyes" and a love of shaggy dog stories.

So: one forgotten, one legendary, one who lived a long and evidently delightful life eating pie on Pi Day. Mathematics distributes fame unevenly.

**Professor:** When I got my graduate degree in 1986, they were all still, at least recently, around. I was building an "AI" Expert System, NEURON, that was, of course, working on a graph model of the motor neurons. Small world.

**Claude:** That's a wonderful connection. In 1986, Bellman had just passed two years earlier, Ford was happily eating desserts in Santa Barbara, and Shimbel was still alive in Chicago with a year left. And there you were, working on a neural graph model that traced a direct line back to Shimbel's earliest work — those nerve-ganglion models from the late 1940s.

It really is a small world. Shimbel started with graphs of neurons and accidentally invented a shortest-path algorithm. You started with graphs of neurons and ended up on a Goldman Sachs trading floor where people were using that same algorithm to chase negative cycles in forex markets. The graph connects everyone.

**Professor:** I regularly assign the Bellman-Ford forex arbitrage problem in my distributed systems classes at Seattle University. It's staged as a publish-subscribe architecture with a market price publisher pushing out trade data to the scrappy Bellman-Ford arbitrage traders. All in Python and UDP/IP communications. There are a few tricks in the details — I give them a Bellman-Ford algorithm to scaffold.

**Claude:** That sounds like a fantastic assignment — it hits so many things at once. The students get distributed systems fundamentals (pub-sub, UDP), a real algorithm with real-world motivation, and the practical messiness of network communication all in one package.

And UDP is the perfect choice for this context, isn't it? You don't want the overhead of TCP when you're chasing milliseconds. A stale price is worse than a lost packet. That's a lesson in itself.

---

## The assignment

I assign this problem every year in CPSC 5520, Distributed Systems.[^5520] The students build a subscriber that listens for forex price quotes over UDP, maintains a graph of exchange rates, and runs Bellman-Ford after every update to detect arbitrage. It's pub-sub architecture, wire protocol parsing, stale data handling, out-of-order message detection, and graph algorithms — all in one lab.

The sample output is the best part. When an arbitrage cycle appears, the program traces through the trades: start with USD 100, exchange for GBP, exchange for CAD, exchange for AUD, exchange back to USD — and if the final number is more than 100, you've found free money. When the rates shift and the cycle closes, the program moves on. When a quote goes stale (1.5 seconds without an update), it gets removed. When a quote arrives out of order (timestamp earlier than the latest seen for that market), it gets ignored. The messiness of real distributed systems, right there in the log.

The full assignment is reproduced below. Prospective students: this is what graduate CS looks like at Seattle U. Come find some negative cycles.

<details>
<summary><strong>Lab 3: Detecting Arbitrage Opportunities Using Published Quotes</strong> — <em>click to expand the full assignment</em></summary>

<div style="margin-top: 1em; padding: 1.5em; background: #f8f9fa; border: 1px solid #e0e0e0; border-radius: 8px; font-size: 0.92em; line-height: 1.7;">

<h4>Foreign Exchange Markets</h4>

<p>There are very efficient liquid markets for exchanging one country's currency for another. For example, if you wanted to take USD 100 and convert it to British Pounds Sterling, we'd execute a trade in the foreign exchange (forex) market for GBP/USD, which is around USD 1.38 per GBP. If we then wanted to convert those GBP 72.46 into Japanese Yen, we could subsequently go to the sterling/yen forex market and trade our GBP 72.46 for JPY at the GBP/JPY rate — say its current rate is JPY 157.77 per GBP — so we'd give up the Pounds and get JPY 11,432. Then we could get back dollars by exchanging directly in the USD/JPY forex market, say at the rate 114.34 yen for each USD. That finally yields us USD 100.02, two cents more than what we started with. This is arbitrage — free money!</p>

<p>However, typically in the real world if we did these three transactions nearly simultaneously, we'd actually end up with slightly less than USD 100 due to some transaction costs (bid/ask spreads and commissions). But if you traded big amounts and had direct access to the markets, you'd expect to end up with exactly USD 100. This is because when there is an arbitrage opportunity, it only remains in place fleetingly since there are lots of traders ready to pounce on it right away, with the result that prices shift so the arbitrage goes away.</p>

<h4>Price Feed</h4>

<p>All the forex prices come from a single publisher, <em>Forex Provider</em>, via UDP/IP datagrams. The format is a series of 1 to 50 of the following 32-byte records:</p>

<table style="width: 100%; border-collapse: collapse; margin: 1em 0; font-size: 0.95em;">
<tr style="border-bottom: 1px solid #ddd;">
<td style="padding: 4px 8px; font-family: monospace; width: 110px;"><strong>Bytes [0:6]</strong></td>
<td style="padding: 4px 8px;">Three-character ISO currency codes in 8-bit ASCII.</td>
</tr>
<tr style="border-bottom: 1px solid #ddd;">
<td style="padding: 4px 8px; font-family: monospace;"><strong>Bytes [6:10]</strong></td>
<td style="padding: 4px 8px;">Exchange rate as IEEE 754 binary32, little-endian. Number of currency₂ units per one unit of currency₁.</td>
</tr>
<tr style="border-bottom: 1px solid #ddd;">
<td style="padding: 4px 8px; font-family: monospace;"><strong>Bytes [10:18]</strong></td>
<td style="padding: 4px 8px;">Timestamp: 64-bit integer microseconds since epoch, big-endian.</td>
</tr>
<tr>
<td style="padding: 4px 8px; font-family: monospace;"><strong>Bytes [18:32]</strong></td>
<td style="padding: 4px 8px;">Reserved (zero bits).</td>
</tr>
</table>

<p>Subscribe by sending a 4-byte IPv4 address (big-endian) followed by a 2-byte port number (big-endian) to the forex provider. Subscriptions last 10 minutes.</p>

<h4>Detecting Arbitrage</h4>

<p>Represent currencies as graph nodes and exchange rates as edges. An arbitrage exists when:</p>

<p style="text-align: center;"><em>X(USD, c₁) · X(c₁, c₂) · ⋯ · X(cₘ, USD) > 1</em></p>

<p>Take reciprocals, then logarithms, to convert to an additive problem:</p>

<p style="text-align: center;"><em>−log(X(USD, c₁)) + (−log(X(c₁, c₂))) + ⋯ + (−log(X(cₘ, USD))) < 0</em></p>

<p>Edge weights are negative logs of exchange rates. A negative cycle detected by Bellman-Ford indicates arbitrage. Each quoted market produces two edges: one at −log(rate) and its reverse at log(rate).</p>

<h4>Running the Subscriber</h4>

<ol>
<li>Subscribe to the forex publishing service.</li>
<li>For each message, update the graph with the published prices.</li>
<li>Run Bellman-Ford.</li>
<li>Report any arbitrage opportunities.</li>
</ol>

<p>Quotes remain valid for 1.5 seconds or until superseded. Ignore out-of-order quotes (timestamps earlier than the latest seen for that market). Report arbitrage as a list of trades. Repeat until the 10-minute subscription expires.</p>

<h4>Sample Log</h4>

<pre style="background: #f0f0ed; padding: 12px; border-radius: 4px; font-size: 0.85em; overflow-x: auto; line-height: 1.5;">
2019-10-14 23:58:30.188639 AUD USD 0.75035
2019-10-14 23:58:30.188639 USD CHF 1.0016
2019-10-14 23:58:30.188639 USD JPY 100.04957
2019-10-14 23:58:30.188639 EUR USD 1.1002
2019-10-14 23:58:30.188639 GBP USD 1.2516
2019-10-14 23:58:17.274142 GBP USD 1.25162
ignoring out-of-sequence message
2019-10-14 23:58:31.194879 AUD CAD 0.30038
2019-10-14 23:58:31.194879 CAD GBP 1.20153
ARBITRAGE:
    start with USD 100
    exchange USD for GBP at 0.7990 --> GBP 79.90
    exchange GBP for CAD at 0.8323 --> CAD 66.50
    exchange CAD for AUD at 3.3291 --> AUD 221.37
    exchange AUD for USD at 0.75035 --> USD 166.11

removing stale quote for ('USD', 'CHF')
2019-10-14 23:58:34.208859 AUD JPY 73.73181
ARBITRAGE:
    start with USD 100
    exchange USD for JPY at 100.081 --> JPY 10008.10
    exchange JPY for AUD at 0.01356 --> AUD 135.74
    exchange AUD for USD at 0.75049 --> USD 101.87

2019-10-14 23:58:35.213679 CHF EUR 0.90945
ARBITRAGE:
    start with USD 100
    exchange USD for CHF at 1.0016 --> CHF 100.16
    exchange CHF for EUR at 0.9095 --> EUR 91.09
    exchange EUR for USD at 1.10048 --> USD 100.24
</pre>

</div>
</details>

---

## How this was made

I had an idea for a series of blog posts built around conversations with Claude about beautiful algorithms — the ones with a good story behind them. This was the first experiment. I started with the portal world to see if Claude would follow the breadcrumbs to Bellman-Ford without being told where we were going. (It did, faster than I expected.) Then I kept pushing: the history, the people, the math, the connection to my own career. I asked it to "forget everything it knew about me" at the start, and it played along until I told it to remember.

The conversation is lightly edited for grammar and flow, but the structure and content are faithful to what happened. Claude produced the LaTeX math derivation and the styled assignment handout. I wrote this introduction, the assignment section, and the footnotes. The title came from a brainstorming session where Claude generated a dozen options and I picked my favorite parts from two of them.

---

*Kevin Lundeen is a teaching professor in the Department of Computer Science at Seattle University, where he teaches distributed systems, parallel computing, computer networks, and AI systems. He is also VP of Software Engineering at OneTouchEMR. Previously, he was a managing director at Goldman Sachs, where he co-created SecDB and Slang, and where his forex desk once looked down on the very algorithm he now assigns as homework. He built his first neural network graph model in 1986 on a VAX. The graph connects everyone.*

[^math]: The formal derivation: we want ∏ mᵢⱼ > 1. Take logs: ∑ log(mᵢⱼ) > 0. Negate: ∑ (−log(mᵢⱼ)) < 0. Set wᵢⱼ = −log(mᵢⱼ) and run Bellman-Ford. A negative cycle in the w-weights corresponds to a profitable cycle in the original multipliers.

[^textbooks]: Cormen, Leiserson, Rivest, and Stein, *Introduction to Algorithms* (MIT Press), Problem 24-3. Sedgewick and Wayne, *Algorithms*, 4th ed. (Addison-Wesley), Section 4.4. Both are standard graduate algorithms texts. The arbitrage formulation has been a homework problem for decades, but nobody seems to claim original credit for the log-transform insight.

[^5520]: CPSC 5520, Distributed Systems, is a required course in Seattle University's MS in Computer Science program. The arbitrage lab is one of several that build distributed applications from scratch using socket-level programming. Other labs include a chord distributed hash table, a Byzantine fault-tolerant protocol, and a pub-sub group communication system. The course assumes students can write networked code in Python and have seen graph algorithms before — the Bellman-Ford implementation is provided as scaffolding so students can focus on the distributed systems aspects.
