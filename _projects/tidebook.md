---
title: "Tidebook"
thumbnail: "/assets/images/projects/project1/thumbnail.jpg"
technologies: ["Golang", "HTMX", "PostgreSQL", "TailwindCSS"]
github_url: ""
live_url: ""
archive: false
---

Tidebook is a lightweight, spaced repetition flashcard app built for the web, inspired by Anki and my desire to actually retain what LLMs were teaching me. Designed to help reinforce programming syntax and problem-solving strategies, it features a simple interface, category tagging, and a rating system that controls how far in the future cards are scheduled. At its core is a Go implementation of [the Free Spaced Repetition Scheduler algorithm](https://github.com/open-spaced-repetition/fsrs4anki), which I built from scratch to power the review logic.

This was my first full web app in Go and an exploration of HTMX and server-first development. Although HTMX played a smaller role than expected, it helped me embrace a fast, frontend-light approach similar to Rails' Hotwire. Without the opinionated structure of Rails, the biggest challenge was designing the architecture and flow of the app from scratch—routing, templating, and state management all required more manual decisions. Tidebook runs locally for now with a shared database and no auth, but I'm considering open-sourcing it or building on it further, especially with ideas for deeper LLM integration.
