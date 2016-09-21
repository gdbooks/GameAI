## The Minimax Method

The MiniMax method searches trough several levels of moves, it always assumes that the opponent will make the best move available. Here is a video that provied a great introduction to the minimax algorithm. It goes into advanced topics like aplha-beta pruning.

{% youtube %}https://www.youtube.com/watch?v=6ELUvkSkCts{% endyoutube %}

#### The Algorithm

The algorithm for minimax is simple, as it is just a recursive function! It follows these steps:

* Try to make all valid moves
  * If a move is terminal, evaluate it's value
  * If a move is not terminal, recurse with the next player
    * Set the value of the move to the value of the recursion
  * Compare each move against the best move
    * If the move is better, store it as the best move    
* Return the best move

In code, this would look something like so:


```cs
Move MiniMax(Player player, GameState gameState) {
    Move bestMove = null;
    GameState newState = new GameState();
    
    // Generate all valid moves for player
    List<Move> validMoves = GenerateValidMoves(player, gameState);
    
    foreach(Move move in validMoves) {
        newState.Copy(gameState);
        newState.Apply(move);
        
        if (newState.IsTerminal) {
            move.Rank = Evaluate(newState);
        }
        else {
            move.Rank = MiniMax(NextPlayer(), newState).Rank;
        }
        
        if (bestMove == null || move.Rank -is better than- bestMove.Rank) {
            bestMove = move;
        }
    }
    
    return bestMove;
}
```

Functions such as ```Evaluate```, ```GenerateValidMoves``` and ```NextPlayer()``` are game specific. the ```-is better than-``` section works the same way that it did for the ```Greedy``` algorithm.

#### Comparison
Compare the pseudo-code provided in this section, to the code provided in the last section! The greedy method simply evaluates a move as:

 ```cs
 move.Rank = Evaluate(newState);
 ```
 
 Where the MiniMax method changes this to:
 
 ```cs
 if (newState.IsTerminal) {
    move.Rank = Evaluate(newState);
}
else {
    move.Rank = MiniMax(NextPlayer(), newState).Rank;
}
```

The rest of the code is identical. This bit of code, the recursion, is what gives the minimax algorithm the ability to look ahead and make the best possible decisions.

#### Drawbacks
There are drawbacks to the minimax algorithm:

* Depth First Traversal
  * This could be VERY time consuming!
  * The larger the game area, the more time it takes to calculate best move.
  * Primary reason that chess is so hard to write AI for
* No "Forfeit" moves
  * Sometimes its better to skip a turn with a strategy for the next move
  * This can not be done in a generic manner 
* Unnecessary Branching
  * In the list of valid moves, there are moves that we can reason don't need to be made 
* No random capacity 
  * No support for dice, cards, etc..

In the same order as the above list, there are mitigation techniques for each of the drawbacks

* Depth limit
* Forfeit Recognition
* Alpha-Beta Pruning
* Chance Nodes