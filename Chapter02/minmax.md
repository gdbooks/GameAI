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

Functions such as ```Evaluate```, ```GenerateValidMoves``` and ```NextPlayer()``` are game specific. The comparison of move ranks might look a bit confusing. This is because for player 1 a negative number is better, for player 2 a positive number is better. That if block could be written as:

```
if (bestMove == null) {
    bestMove = move;
}
if (player == GetPlayer1()) {
    if (move.Rank < bestMove.Rank) {
        bestMove = move;
    }
}
else if (player == GetPlayer2()) {
    if (move.Rank > bestMove.Rank) {
        bestMove = move;
    }
}
```

Or, even move compactly as:

```cs
bool betterMove = (player == GetPlayer1())? (move.Rank < bestMove.Rank) : (move.Rank > bestMove.Rank);
if (bestMove == null || betterMove) {
    bestMove = new ComputerMove(row, col);
    bestMove.rank = currentRank;
}
```

 