## The Greedy Method

The __Greedy Method__ picks the move that yields the most immediately valuable game state. Let's take a look at some pseudo code that demonstrates this.

```
Move Greedy(Player player, GameState gameState) {
    Move bestMove = null;
    GameState newState = new GameState();
    
    // Generate all valid moves for player
    List<Move> validMoves = GenerateValidMoves(player, gameState);
    
    foreach(Move move in validMoves) {
        newState.Copy(gameState);
        newState.Apply(move);
        move.Rank = Evaluate(newState);
        
        if (bestMove == null || move.Rank -is better than- bestMove.Rank) {
            bestMove = move;
        }
    }
    
    return bestMove;
}
```

The comparison of move ranks might look a bit confusing. This is because for player 1 a negative number is better, for player 2 a positive number is better. That if block could be written as:

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

The greedy method has some distinct benefits:

* It is __FAST__
* It used moderate memory
* It uses moderate CPU time

But the greedy method also has some drawbacks

* It ignores the opponents potential reaction
* It's short sighted / dumb / not optimal

Games will often start out with a greedy AI and evolve into more sophisticated AI methods as needed.