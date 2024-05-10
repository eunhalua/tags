# Filtering Enabled

Filtering Enabled is a feature that prevents changes made on the client side to replicate to the server side. This was previously an optional feature put in place by Roblox to combat exploiters but is now forced onto all experiences and cannot be toggled following Roblox's strict imposement of anti-exploits. The property was also deprecated as developers are not able to toggle it anymore.

#### How Does It Work?

Filtering Enabled works by separating the server and the client environment. Before FilteringEnabled, changes made on the client would propagate to the server allowing players to create their own scripts, instances, ruin the game for other players and more. With the environments separated, replication filtering became thing. It blocked client-sided changes from replicating to the server ultimately limiting the control of clients over the game. Exploiters will still be able to make changes on anything but that change will only appear on their end. For example, an exploiter deletes a part in the workspace on their client, it would only disappear for them but not for everyone else.

#### Exceptions

While FilteringEnabled essentially stops user-imposed client-server replication, there are still exceptions to this rule. Such things would be assemblies and baseparts that are network-owned by the client. This same exception is the very reason why movement exploits such as teleportation, speed, and jump exist. Unanchored parts may also be a part of this exception because network ownership will automatically be set to certain clients.




