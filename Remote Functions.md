# Remote Functions

Like RemoteEvents, a RemoteFunction call initiated by the client to the server will ALWAYS pass the player. This eliminates the need of putting Player as the first argument in `RemoteFunction:InvokeServer()`. A RemoteFunction will wait until the function finishes or returns something.

##### NOTE:
`RemoteFunction:InvokeClient()` is not usually used in practice because there will almost always be no instance that a client has information that the server does not have. If invoking the client is really needed, certain risks should be taken.

##### RISKS:

If the client errors, the server will also error.
If the client does not return a value, the server will yield indefinitely.
If the client leaves or gets disconnected from the game upon invocation, InvokeClient() will error.

##### IMPLEMENTATION:
A simple RemoteFunction implementation for retrieving the player's network ping from the server.

```lua
-- LocalScript (Client) --
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Remotes = ReplicatedStorage.Remotes
local Remote = Remotes.RemoteFunction

local pingDisplay = script.Parent

while true do
  -- Sets the text of the display to the returned ping value by the server.
  pingDisplay.Text = tostring(Remote:InvokeServer()).."ms"
  task.wait()
end

-- Script (Server) --
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Remotes = ReplicatedStorage.Remotes
local Remote = Remotes.RemoteFunction

-- Receive the invoke signal.
Remote.OnServerInvoke = function(Player: Player)
  -- Send back the result of the calculation to the client.
  return Player:GetNetworkPing() * 1500
end
```
