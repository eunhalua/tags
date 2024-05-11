# Remote Events

A simple RemoteEvent implementation for a clicker simulator game.

It is important to note that RemoteEvents fired from the client to the server will ALWAYS automatically pass the Player who fired. This eliminates the need to put Player as the first argument in `RemoteEvent:FireServer()`


```lua
-- LocalScript (Client) --
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Remotes = ReplicatedStorage.Remotes
local Remote = Remotes.RemoteEvent

local Player = game.Players.LocalPlayer
local Mouse = Player:GetMouse()

-- Connection setup that fires when the player clicks
Mouse.Button1Down:Connect(function()
  -- Let the server know that the player clicked
  Remote:FireServer()
end)

-- Script (Server) --
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Remotes = ReplicatedStorage.Remotes
local Remote = Remotes.RemoteEvent

-- Connection that receives the call and updates click data.
Remote.OnServerEvent:Connect(function(Player)
  local leaderstats = Player.leaderstats
  local clicks = leaderstats.Clicks

  -- Add to the clicks value of the Player
  clicks.Value += 1
end)
```
