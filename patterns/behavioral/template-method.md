### Template Method

Define the skeleton of an algorithm as an abstract class, specifying how it should be performed.

Template Method is a method in a superclass, typically an abstract superclass, that defines the skeleton of an operation in terms of a series of high-level steps.

**Example:**

Let's take an example of a chess game.

The Template Method design pattern is a design pattern that defines the skeleton of an algorithm in a superclass but allows subclasses to implement certain steps of the algorithm without changing its overall structure. Here's the code step by step:

**Step 1:** We create the base class Game, which will serve as the game's skeleton and defines the overall flow of the game.

```
class Game {
  constructor(numberOfPlayers) {
    this.numberOfPlayers = numberOfPlayers;
    this.currentPlayer = 0;
  }

  execute() {
    this.initialize();
    while (!this.haveWinner) {
      this.takeTurn();
    }
    console.log(`Player ${this.winningPlayer} wins.`);
  }

  initialize() {}
  get haveWinner() {}
  takeTurn() {}
  get winningPlayer() {}
}
```

**Step 2:** We create the Chess class that inherits from Game and customizes specific details of the chess game, such as the number of players and maximum number of turns.

```
class Chess extends Game {
  constructor() {
    super(2);
    this.maxTurns = 10;
    this.turn = 1;
  }

  initialize() {
    console.log(`Starting a chess game with ${this.numberOfPlayers} players.`);
  }

  get haveWinner() {
    return this.turn > this.maxTurns;
  }

  takeTurn() {
    console.log(`Turn ${this.turn} taken by player ${this.currentPlayer}`);
    this.currentPlayer = (this.currentPlayer + 1) % this.numberOfPlayers;
    this.turn++;
  }

  get winningPlayer() {
    return this.currentPlayer;
  }
}
```

**Step 3:** We create an instance of the Chess class and execute the game by calling the execute method.

```
let chess = new Chess();
chess.execute();
```

This example demonstrates how the Template Method design pattern is used to define the overall flow of the game in the base class Game and how specific game details are customized in the Chess class.

**Final Code:**

```
class Game {
  constructor(numberOfPlayers) {
    this.numberOfPlayers = numberOfPlayers;
    this.currentPlayer = 0;
  }

  execute() {
    this.initialize();
    while (!this.haveWinner) {
      this.takeTurn();
    }
    console.log(`Player ${this.winningPlayer} wins.`);
  }

  initialize() {}
  get haveWinner() {}
  takeTurn() {}
  get winningPlayer() {}
}

class Chess extends Game {
  constructor() {
    super(2);
    this.maxTurns = 10;
    this.turn = 1;
  }

  initialize() {
    console.log(`Starting a chess game with ${this.numberOfPlayers} players.`);
  }

  get haveWinner() {
    return this.turn > this.maxTurns;
  }

  takeTurn() {
    console.log(`Turn ${this.turn} taken by player ${this.currentPlayer}`);
    this.currentPlayer = (this.currentPlayer + 1) % this.numberOfPlayers;
    this.turn++;
  }

  get winningPlayer() {
    return this.currentPlayer;
  }
}

let chess = new Chess();
chess.execute();

// Expected Output:

// Starting a chess game with 2 players.
// Turn 1 taken by player 0
// Turn 2 taken by player 1
// Turn 3 taken by player 0
// Turn 4 taken by player 1
// Turn 5 taken by player 0
// Turn 6 taken by player 1
// Turn 7 taken by player 0
// Turn 8 taken by player 1
// Turn 9 taken by player 0
// Turn 10 taken by player 1
// Player 1 wins.
```
