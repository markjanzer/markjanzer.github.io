---
title: "LoL Champ Recommender"
thumbnail: "/assets/images/projects/project1/thumbnail.jpg"
technologies: ["Rails", "React", "PostgreSQL", "Chart.js", "Sidekiq", "TailwindCSS"]
github_url: ""
live_url: "https://www.lolproelo.com/"
archive: false
---

LoLProElo is a web application that visualizes the evolving strength of professional League of Legends teams across major regions. Inspired by FiveThirtyEight’s Elo-based sports rankings, the site pulls match data from public APIs and applies a Elo algorithm to track team performance over time. Users can explore historical Elo trends, compare teams across seasons, and see insights for specific seasons.

The project’s biggest challenges lay in data engineering: sourcing reliable match data, normalizing formats across regions and seasons, and building a system that updates automatically based on the latest results. While implementing the Elo model itself was relatively straightforward, designing a maintainable pipeline for continuous updates and clean data storage required significant iteration. Ultimately, LoLProElo reflects a blend of statistical modeling, automation, and a passion for esports analytics.

