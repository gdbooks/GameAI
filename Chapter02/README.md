#Game Playing

## Turn Based Games

Turn based games involve multiple players who act on their own "turn" to advance. Examples of turn based games:

* RPGs: Final Fantasy, D&D, some MMORPGs
* Board Games: Chess, Checkers, Go, Backgammon
* Card Games: Poker, Old Maid, Magic Hearts
* War Games: Civilization, Master of Orien

Features of turn based games:

* Require two or more players
* Have well defined game state
* Occur as a sequence of rounds or turns
* Proceed according to precisely defined rules
* Allow players to change game state trough moves

## Data Structures

Turn based game playing is a well defined problem. It has:

* An initial state
* A set of goal states
* A set of reachable states
* 1+ Operators

Because it's well defined, we can approach it using different search techniques. We will need a few data structures and functions to play games

* __GameState__ class, contains information about pieces, cards, players, etc
* __Move__ class, represents a single move by a player in a game
* __Terminal Function__, tells us when a game is over
* __Evaluation function__, tells of the value of the games state

Game playing is __Data Synthesis__. The game has an initial state. Each move then create a new, modified state. Whatever state is the most desirable is the move we decide to make!