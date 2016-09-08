# Introduction To AI

### What is Intelligence

* Logical Thought
* Problem Solving
* Decision Making
* Learning / Adaptation

### Kenneth Craik's Model

An intelligent automation...

* Uses a small scale model of reality
* Is capable of performing actions
* Has knowledge of the effects of it's actions
* Uses inferences to make decisions

### What is Artificial Intelligence?

Computers are pretty good at:

* Mathematical computation
* Remembering Information

But pretty bad at

* Solving Problems
* Making Decisions
* Learning

Trough AI we hope to give machines the ability to reason and to __Appear More Lifelike__

## Agents

We call an AI program or machine an __agent__

| Types of agents | Behaviour |
| -- | -- |
| Reflex | Reactionary |
| Goal-Based | Seeking some goal |
| Utility-Based | Seeking some utility (happyness) |

### Agent behaviours

A __Behaviour__ is a way an agent thinks and acts

Behaviours can be

* Simple (ex, scripted) or
* Complex (A composition of simple behaviours)

When a behaviour terminates it either __Succeeds__ or __fails__. We'll use __Behaviour Trees__ to model agent behaviours

## Sequences

A __sequence__ is a set of behaviours, in which all behaviours must complete for the sequence to succeed. If any behaviour fails, the sequence fails

![Chapter01/sequence.png](Chapter01/sequence.png)

## Selectors

A __selector__ is a set of behaviours any one of which must compleate for the selector to succeed. If any child succeeds, the selector immediateley succeeds.

![Selectpr](Chapter01/selector.png)

## Knowledge Representation

How an agent remembers...

* The state of the world
* Processed information
* The actions it may perform
* Consequences of its actions

Proper representation of knowledge within an agent is crucial to its ability to function!

## Agent Architecture

![Agent](Chapter01/agent.png)

Behavioral knowledge can be temporary or persistent

```cs
class Agent {
  Knowledge currentKnowledge;
  Behaviour currentBehaviour;
  
  void Enter(); // Begin agent update cycle
  void Update(); // Gathers perceptions / filters, runs behaviours
  void Exit(); // Terminates agent update cycle
}
```

```cs
class Behaviour {
  enum state { ACTIVE, SUCCESS, FAIL }
  Behaviour Children = null;
  
  void Enter();
  state Update(Agent agent, Deletgate Function, float deltaTime);
  void Exit();
  
}
```