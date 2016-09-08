## The Greedy Method

The __Greedy Method__ picks the move that yields the most immediately valuable game state. Let's take a look at some pseudo code that demonstrates this.

```
Move Greedy(player, gameState) {
    Move bestMove = null;
    GameState newState = new GameState();
    
    List<Move> moves = // Generate valid moves
    Move bestMove = null;
    
    foreach(Move move in moves) {
        newState.Copy(gameState);
        newState.Apply(move);
        move.Rank = Evaluate(newState);
        
        if (bestMove == null || move.Rank > bestMove.Rank) {
            bestMove = move;
        }
    }
    
    return bestMove;
}

```