## The Minimax Method

The MiniMax method searches trough several levels of moves, it always assumes that the opponent will make the best move available. 

{% youtube %}https://www.youtube.com/watch?v=9bZkp7q19f0{% endyoutube %}


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
            move.Rank = MiniMax(nextPlayer, newState).Rank;
        }
        
        if (bestMove == null || move.Rank > bestMove.Rank) {
            bestMove = move;
        }
    }
    
    return bestMove;
}
```