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

The greedy method has some distinct benefits:

* It is __FAST__
* It used moderate memory
* It uses moderate CPU time

But the greedy method also has some drawbacks

* It ignores the opponents potential reaction
* It's short sighted / dumb / not optimal

Games will often start out with a greedy AI and evolve into more sophisticated AI methods as needed.