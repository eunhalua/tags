A simple RemoteFunction implementation for displaying the player's ping on the client side.

Like RemoteEvents, a RemoteFunction call initiated by the client to the server will ALWAYS pass the player. This eliminates the need of putting Player as the first argument in `RemoteFunction:InvokeServer()`. A RemoteFunction will yield the execution of code until it receives a response from the receiving end meaning you should not use RemoteFunctions if you are not going to return any significant data or any data at all.

##### NOTE:
`RemoteFunction:InvokeClient()` is not usually used in practice because there will almost always be no instance that a client has information that the server does not have. If invoking the client is really needed, certain risks should be taken.

##### RISKS:
If the client errors, the server will also error.
If the client does not return a value, the server will yield indefinitely.
If the client leaves or gets disconnected from the game upon invocation, InvokeClient() will error.

```lua
-- LocalScript (Client) --
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Remotes = ReplicatedStorage.Remotes
local Remote = Remotes.RemoteFunction

local pingDisplay = script.Parent

while true do
  pingDisplay.Text = tostring(Remote:InvokeServer()).."ms"
  task.wait()
end

-- Script (Server) --
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Remotes = ReplicatedStorage.Remotes
local Remote = Remotes.RemoteFunction

Remote.OnServerInvoke = function(Player: Player)
  return Player:GetNetworkPing() * 1500
end
```
