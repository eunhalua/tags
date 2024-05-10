Basic usage of RemoteEvents.

##### It is important to note that RemoteEvents fired from the client to the server will ALWAYS automatically pass the Player who fired. This eliminates the need to put Player as the first argument in RemoteEvent:FireServer()

```lua
-- LocalScript (Client) --
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Remotes = ReplicatedStorage.Remotes
local Remote = Remotes.RemoteEvent
local Textbox = script.Parent

Textbox.FocusLost:Connect(function()
  if #Textbox.Text > 0 then
    local Text = Textbox.Text
    Remote:FireServer(Text)
  end
end)

-- Script (Server) --
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Remotes = ReplicatedStorage.Remotes
local Remote = Remotes.RemoteEvent

Remote.OnServerEvent:Connect(function(Player, Text)
  print(Player, Text)
end)
```