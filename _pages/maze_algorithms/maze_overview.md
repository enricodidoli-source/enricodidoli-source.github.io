---
layout: archive
title: "Maze Generation Algorithms"
permalink: /maze_overview/
author_profile: true
---

Welcome to my Maze Project! In this study, I implemented and analysed 5 distinct maze generation algorithms. 

I generated and evaluated more than 4,500 mazes of varying dimensions for each of the 5 algorithms. To compare them, I defined several performance metrics, such as solve time, decision points, and visited cells, along with custom metrics like path complexity. I then evaluated the generated mazes using an A* solver and analyzed the results across the different algorithms.

Based on this analysis, the study found that:

- **Aldous-Broder and Wilson** show the highest complexity. They lack discernible patterns, and their numerous decision points make them the most challenging mazes to solve. However, they also require the highest generation time and have the highest computational complexity.
- **Prim and Eller** are both very fast to generate, but they produces predictable patterns that are relatively easy to solve.
- **Recursive Backtracking** generates the least complex mazes, which may feel repetitive as the algorithm forces the deep exploration of long branches.
  
You can read the full paper directly below, or choose a destination to download the PDF, play the game, or view the source code:

[Download the Paper](/assets/pdf/Maze_Generating_Algorithms.pdf){: .btn .btn--info}
[Play the Game](/maze_game/){: .btn .btn--success}
[View Source Code](https://github.com/enricodidoli-source/maze-algorithms){: .btn .btn--primary}

<iframe src="/assets/pdf/Maze_Generating_Algorithms.pdf" width="100%" height="800px" style="border: 1px solid #ccc;"></iframe>
