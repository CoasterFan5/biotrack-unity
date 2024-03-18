# biotrack-unity
Unity bindings for the biotrack api + examples (this is one of the projects of all time)

## Getting Started
1. Clone this repository
2. Open your project in unity
3. Copy the `Biotrack` assets folder into your own project
4. Attach the `BioTrackAttachable` script to a game object somewhere in your title screen
5. Configure the game id and max players. 

## Usage

When a the number of join requests has reached the max player count, or `BioTrack.StartGame()` is called, the `OnStart` event will be called with a list of `JoinRequestUser` objects.
```csharp
public void Start() {
	BioTrack.OnStart((List<JoinRequestUser> users) => {
		// do something with the users
	});
}
```

Force start a game with the current join requests (not recommended)
```csharp
BioTrack.StartGame();
```

Once a player has completed the game, you need to finish the active sessions and update their scores
```csharp
public void WinCondition() {
	BioTrack.FinishGame(<score>, <doContinue>. <data>);
}

// ex: 
public void WinCondition() {
	BioTrack.FinishGame(1, false, "You win!");
}
```

Setting `doContinue` to true will allow the user to continue playing the game. This is useful for games that have multiple levels or rounds and you want to award points for each round in realtime. 

```csharp
public void WinCondition() {
	BioTrack.FinishGame(1, true, "You win!");
}
public void WinCondition2() {
	BioTrack.FinishGame(3, true, "You win!");
}
public void WinCondition3() {
	BioTrack.FinishGame(5, false, "You win!");
}
```

You can also listen in for when a game stops, by adding a function that takes a boolean argument (which represents if the game is continuing or not). 

```csharp
public void Start() {
	BioTrack.OnFinish((cont) => {
		//do things
	});
}
```

