# biotrack-unity
Unity bindings for [Biotrack](https://github.com/LeoDog896/biotrack) + examples (this is one of the projects of all time)
You should familiarize yourself with the [Biotrack Docs](https://leodog896.github.io/biotrack/) to better understand this project.

## Quick Notice
If you are very familiar with C# and web requests, these may not be the bindings for you. In an effort to make implementing Biotrack as simple as possible, the extendability of the [Biotrack API](https://leodog896.github.io/biotrack/api.html) has been reduced significantly. 

## Getting Started
1. Download the latest release
2. Open your project in unity
3. Copy the `Biotrack` assets folder into your own project
4. Attach the `BioTrackAttachable` script to a game object somewhere in your title screen
5. Configure the game ID and max players.

## Install JSON Parser
1. Open Unity
2. Go to Window > Package Manager
3. Press the plus button
4. Add from git URL
5. Enter url: `com.unity.nuget.newtonsoft-json`

## Usage

To get started with Biotrack, you will need to attach BioTrackAttachable to a game object in each scene. This will allow you to configure the game id and max players.
Note that Biotrack can only be configured once, even if there are different configurations per scene.  

When the number of join requests has reached the max player count, or `BioTrack.StartGame()` is called, the `OnStart` event will be called with a list of `JoinRequestUser` objects.
```csharp
public void Start() {
	BioTrack.OnStart((List<JoinRequestUser> users) => {
		//Do something with the users
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

Setting `doContinue` to true will allow the user to continue playing the game. This is useful for games that have multiple levels or rounds where you want to award points for each round. 

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

You can also listen in for when a game stops using `OnFinish`. By adding a function that takes a boolean argument you can perform different actions based on if the session is continuing or not. 

```csharp
public void Start() {
	BioTrack.OnFinish((cont) => {
		//do things
	});
}
```

## Questions/Support
If you have any questions or need help implementing Biotrack into your game, please reach out to me on Discord: `@coasterfan5`

