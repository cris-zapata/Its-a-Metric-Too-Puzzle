<div align="center">

# It's a Metric, Too.

### Eight days of symmetry, shortest paths, and a lot of trial and error.

*My experience working through Jane Street's 11 × 11 puzzle — from iPad sketches to an interactive board.*

[The puzzle](#the-puzzle) · [My notes](#my-handwritten-notes) · [Interactive exploration](#interactive-exploration) · [Final thoughts](#final-thoughts)

</div>

---

## The puzzle

I spent eight days trying to make sense of Jane Street's **It's a Metric, Too** puzzle. At first, I figured I'd be able to work through it by identifying a few symmetric regions and building from there. It turned out to be a lot more complicated than that.

The challenge is an **11 × 11 grid** divided into connected, symmetric regions called *states*. The numbers aren't state sizes: each one represents the minimum cost of traveling from that square to a state capital. What makes the puzzle interesting is that changing even one state can change the travel costs across the board.

<p align="center">
  <img src="assets/puzzle-11x11.png" alt="Original 11x11 puzzle" width="450">
</p>

<p align="center"><em>The original 11 × 11 puzzle. Source: Jane Street.</em></p>

### The rules, in brief

1. Every square belongs to one **state**, and each state must be connected through horizontal or vertical neighbors.
2. Each state must have at least one nontrivial **symmetry**, such as a rotation or reflection.
3. Some states have a **capital**, located at a square fixed by every symmetry of that state. Not every state has one.
4. Moving between adjacent squares **inside the same state** costs the number of squares in that state.
5. Moving between **different states** costs the size of the smaller state.
6. Each numbered square gives the **minimum total travel cost** to any capital.

After satisfying all the clues, the answer is calculated by writing each state's size in its squares, adding those values across each row, squaring the row sums, and adding the squares together.

### The 5 × 5 example

Before tackling the full puzzle, I spent time understanding the smaller example. Seeing the completed states, their capitals, and the state-size grid side by side helped me understand what the numbers were actually measuring.

![Jane Street's 5 by 5 example, completed states, and state-size grid](assets/example-5x5.png)

The example's answer is **8,045**. I kept coming back to it whenever I needed to check whether I was interpreting a rule correctly.

---

## How I approached it

I started with handwritten diagrams on my iPad. I tried placing small symmetric states, checking where capitals could go, and comparing the numbered clues with the cost of moving between squares. Sometimes an arrangement seemed to work for one part of the grid, only to cause problems somewhere else.

As I worked through it, I began writing down more general relationships instead of just drawing possible shapes. In particular, I was interested in what neighboring clues could tell me about the minimum size of the states around them.

For two adjacent numbered squares, the difference between their distances to a capital cannot be greater than the cost of crossing the edge between them:

$$
|d(u)-d(v)| \leq w(u,v).
$$

For example, the adjacent **77** and **61** clues differ by **16**, so the cost of moving directly between those squares must be at least 16. That doesn't solve the region by itself, but it immediately rules out some smaller-state arrangements.

I also experimented with coordinate formulas for rotations and reflections, along with ways of representing the board as a weighted graph. A lot of these notes are rough, but that's part of why I wanted to keep them.

---

## My handwritten notes

These are the actual pages I worked on. They're not meant to be a polished proof or a step-by-step solution; they're a record of the ideas I was testing, including ones that didn't pan out.

### 01 — Getting familiar with the rules

My first page was mostly about translating the puzzle into something I could reason about: what makes a valid state, how travel costs work, and how the 5 × 5 example is scored. I also started sketching possible state patterns on the larger grid.

<p align="center"><img src="assets/ipad-notes-01.png" alt="First page of iPad notes: puzzle rules, five-by-five example, and early state sketches" width="780" /></p>

### 02 — Turning observations into constraints

On the next page, I started treating the clue values as shortest-path distances. I wrote down inequalities for neighboring squares and tested how the cost of crossing a state boundary affects which paths are possible. I also collected the coordinate transformations for rotations and reflections, since checking symmetry by eye was getting difficult.

<p align="center"><img src="assets/ipad-notes-02.png" alt="Second page of iPad notes: shortest-path inequalities, boundary costs, and symmetry formulas" width="780" /></p>

### 03 — Applying the ideas to the 11 × 11 grid

This is where I began using the larger clues to narrow down possibilities. I looked at differences between nearby numbers, including the **77** and **61** pair, and tried assigning priorities to squares based on the clues and neighboring regions. I kept testing colored configurations to see which deductions could coexist.

<p align="center"><img src="assets/ipad-notes-03.png" alt="Third page of iPad notes: the eleven-by-eleven grid, adjacent-clue constraints, and candidate states" width="780" /></p>

### 04 — More configurations, more revisions

By this point, I had several different versions of the grid. Some regions looked promising, but the overall arrangement still wasn't consistent. I kept a few of these attempts because they show how much of the process was revisiting assumptions rather than making one clean sequence of deductions.

<p align="center"><img src="assets/ipad-notes-04.png" alt="Fourth page of iPad notes: alternative colored state arrangements" width="780" /></p>

<details>
<summary><strong>View the original four-page notebook PDF</strong></summary>

[Open my original iPad notes (PDF)](notes/Puzzles-original.pdf)

</details>

---

## Interactive exploration

Later, I found a community-made [interactive version of the puzzle](https://pazqo.github.io/#/games/nation-puzzle). This made experimenting a lot easier. Instead of redrawing the grid every time I wanted to move a boundary, I could try a different configuration and see how it affected the state sizes and clue distances.

That feedback was especially useful when I had a region that *looked* reasonable but didn't satisfy the rest of the board. It let me spend more time thinking about the mathematics and less time repeatedly drawing the same 11 × 11 grid.

**[Try the interactive Nation Puzzle board](https://pazqo.github.io/#/games/nation-puzzle)**

<!-- Optional: upload a screenshot of one of my intermediate board configurations to assets/interactive-board.png, then uncomment this line:
![One of my intermediate interactive configurations](assets/interactive-board.png)
-->

I'm grateful to the person who built and shared this tool. It made the exploration much more approachable. *I'll add a direct creator credit here once I confirm the original post.*

---

## Looking back

One thing this puzzle really drove home for me was how much harder a problem becomes when every local decision affects the rest of the system. I could make progress in one corner, but that didn't mean the full configuration would work.

I also tried approaching parts of it computationally. The smaller **5 × 5** example was manageable, but scaling the search to the **11 × 11** puzzle was a different challenge altogether. Generating more candidate states wasn't enough when the search could still miss an important shape.

After seeing the completed arrangement, the feature that surprised me most was a single **37-square state**. I had spent so much time thinking about smaller regions that I hadn't appreciated how much of the board could belong to one symmetric state.

<details>
<summary><strong>Final answer (spoiler)</strong></summary>

The verified score is **408,951**. The completed grid contains an irregular 37-square state with 180° rotational symmetry.

<!-- Optional: upload the completed board as assets/completed-board.png and uncomment:
![Completed eleven-by-eleven puzzle](assets/completed-board.png)
-->

</details>

## Final thoughts

Eight days, a lot of sketches, plenty of wrong turns, and a much better appreciation for the relationship between geometry and shortest paths. I wanted to share the process rather than just post the answer, because the attempts that didn't work were a big part of what made this interesting.

---

## Links and credits

- **Original puzzle:** Jane Street, [*It's a Metric, Too*](https://www.janestreet.com/puzzles/).
- **Interactive board:** [Nation Puzzle](https://pazqo.github.io/#/games/nation-puzzle), community-made exploration tool.
- **Notebook pages:** My original handwritten iPad notes, included above and in [PDF form](notes/Puzzles-original.pdf).

*This is a personal project journal, not an official Jane Street solution or affiliated project.*
[ ] Decide whether you want the final board revealed behind the spoiler.
[ ] Remove any unused sections.
-->
