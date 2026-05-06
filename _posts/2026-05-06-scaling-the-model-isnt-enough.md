---
layout: post
title: "Scaling the model isn't enough: A lesson from chess engines"
date: 2026-05-06
---

I've been learning about chess engines, and one of the things that surprised me most is the neural net at the heart of the strongest engine in the world. The rule I'd internalized about deep learning was that complex problems need deep networks.

Chess seemed obviously complex. So I expected the network running the best chess engine ever built to be deep and sophisticated.

Instead it's wide and shallow. And I can beat it.

The engine is Stockfish — nineteen-time champion of the Top Chess Engine Championship, the best chess player that has ever existed by a comfortable margin. It runs an evaluator called NNUE (Efficiently Updatable Neural Network) that can score tens of millions of positions per second on a typical computer. The thing is fast, and not much else.

DeepMind, by contrast, published a paper in 2024 called "Grandmaster-Level Chess Without Search," where they trained a 270-million-parameter dense transformer to predict Stockfish's evaluations directly. It's the network you'd design if you wanted depth. It runs at maybe 20 evaluations per second on a $200 GPU.

Stockfish wins. Easily. It's not close.

The answer is that Stockfish doesn't try to be smart. It tries to look far.

## The math of looking ahead

Chess has an average branching factor of about 35 — that is, in a typical position, there are around 35 legal moves. If you wanted to brute-force look 10 moves into the future, you'd need to evaluate 35^10 positions. That's roughly 2.7 quadrillion.

Stockfish regularly looks 25 moves ahead.

It does this through aggressive pruning — alpha-beta search, transposition tables, null-move heuristics, late-move reductions, and a stack of other techniques accumulated over decades of computer chess research. The combined effect is that the *effective* branching factor drops from 35 to roughly 2. At that point, looking 25 moves ahead means evaluating around 33 million positions instead of 35^25 (I'm not going to type out all 38 zeroes).

33 million is still a lot of evaluations. This is where a small, fast network earns its keep. NNUE is designed to be cheap to run — its architecture is shaped almost entirely by the constraint "this has to fit inside a tight per-evaluation compute budget, tens of millions of times per move." The depth and sophistication you'd want for understanding chess get traded away in favor of throughput. The model isn't trying to be smart on its own. It's trying to be a fast oracle for a deep search to lean on.

There's a feedback loop worth pulling out: a better evaluator also means more aggressive pruning. If your model can confidently rank moves, you can throw away more branches earlier. Smart and fast aren't fully independent — but for any fixed compute budget, you have to pick where on the curve you sit.

## The spectrum

This tradeoff defines a spectrum. At one end, fast cheap evaluations spent on deep search. At the other, slow expensive evaluations of a single position. Three points on it.

**Stockfish.** Without search, NNUE plays around club level — many decent amateurs would beat it. It's the search machinery, not the model, that makes Stockfish the best engine in the world. (NNUE: ~70 MB, runs on CPU at tens of millions of evaluations per second. Nineteen-time TCEC champion.)

**Leela Chess Zero.** Without search, its network plays at strong master level — would crush any hobbyist, lose to a titled player. (~365 MB dense network, GPU-bound, tens of thousands of evals/sec, paired with MCTS. Beat Stockfish in 2019–2020, and has been second almost every time since.)

**"Grandmaster-Level Chess Without Search."** No search at all. The model is the answer. Plays at 2895 Elo on Lichess blitz — better than all but 16 humans on the site. Loses badly to any actual engine.

So if you rank the three engines purely by *model strength*, the order flips: DeepMind > Leela > Stockfish. If you rank them by *playing strength* — model plus search — the order is exactly reversed. The pure-scaling approach has the strongest model and finishes last.

## Theory vs. practice

There's a flavor of objection here that goes: in principle, a sufficiently large model could learn to do search internally. The DeepMind paper hints at this — they're careful to say their model does no *explicit* search, leaving open the possibility that something search-like is happening inside the weights. So why can't we just scale our way past this?

Maybe in principle. But theory is not practice, and we don't have unlimited compute. The chess engine community has been running this experiment in the open for thirty years. The result keeps coming out the same way: for any compute budget you actually have, spending it on search beats spending it on a bigger model.

This is why the recent shift in LLMs is so interesting. For years the frontier was just bigger models. Now the frontier is reasoning models — models that spend extra compute at inference time, exploring possibilities, backtracking, checking their own work. That's search. It doesn't look like minimax over a game tree, but the underlying claim is identical to the one Stockfish has been making since the 90s: depth of deliberation beats raw model strength, *for the same compute*.

The chess engine result is a thirty-year head start on a lesson the LLM world is now learning. Some problems aren't solved by scaling alone. The interesting question for the next few years isn't how big the next model gets. It's how the search layer on top of it is structured, and what the right tradeoff between the two looks like for problems that aren't chess.

My bet is that we end up somewhere closer to Stockfish than to the DeepMind transformer. We'll see.

---

P.S. I learned all of this on hone — a learning app I'm building, where you bring your own model and it builds a curriculum, tutors you through it, and tests your understanding. Coming soon at hone.study.
