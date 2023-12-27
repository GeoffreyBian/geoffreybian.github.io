---
layout: page
title: Boggle Board Game
description: Word search game on interactive interface 
img: assets/img/boggle2.png
importance: 2
category: work
---
`November 2023`

In the creation of the Boggle board game application, I implemented a system where the player faces off against a computer opponent. The objective is to discover words within a Boggle board in the allotted time. Players can form words by traversing not only horizontally and vertically but also diagonally across the randomized board. By finding more words than the computer, the player is victorious. 

`Technical Insights`

I employed the principles of graph theory to bring the Boggle board to life. Each letter was represented as a vertex, and edges denoted possible connections between adjacent letters, allowing for word formation in various directions. By systematically connecting edges to all potential paths, I achieved an accurate method for identifying all possible words on the dynamic game board.

A significant revelation was the application of Trie data structures to model the dictionary. This sophisticated data structure streamlined the word-checking process. As the computer traversed the board, it consulted the Trie to validate potential words, efficiently halting edge branching if a given path did not align with the Trie structure. This not only optimized the game's performance but also showcased how graphs and data structures can work together to optimize a simple game as such. 

`Application`

The Boggle board game application not only provides entertainment but also serves as a testament to the integration of theoretical concepts with practical implementation, offering players an immersive and stimulating gaming experience.

Please note the graphical user interface was created by UBC's CPEN 221 teaching team. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/boggle1.png" title="Find the word TEA" %}
    </div>
</div>
<div class="caption">
    Player finding the word "TEA" on the board
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/boggle2.png" title="End of Boggle Game" %}
    </div>
</div>
<div class="caption">
    End of the Boggle game showcasing computer outperformance on this randomized board
</div>
