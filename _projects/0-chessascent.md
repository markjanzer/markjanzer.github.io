---
title: "Chess Ascent"
thumbnail: "/assets/images/projects/chessascent/thumbnail.jpg"
technologies: ["Vue 3", "TypeScript", "Fastify", "tRPC", "PostgreSQL", "Prisma", "better-auth", "FSRS", "Glicko-2", "Tailwind CSS"]
github_url: ""
live_url: "https://chessascent.com"
archive: false
---

Chess Ascent is a personalized chess training app that helps players learn from their mistakes through spaced repetition. When users solve puzzles matched to their skill level and fail, those positions are automatically saved for review using scientifically-optimized intervals. The app calibrates to each player's strength using the Glicko-2 rating system—the same algorithm Lichess uses—and sources puzzles from their open database of 5.6 million positions, filtered down to 1.8 million high-quality puzzles.

This project combines many of my interests, chess, ranking, and spaced repetition, building on my experience from Tidebook and LolProElo. The full-stack TypeScript monorepo with tRPC provides end-to-end type safety from database to UI, and the Vue 3 frontend integrates a chess board library for interactive puzzle solving.
