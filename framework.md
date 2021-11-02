# Framework documentation
The Talibratis Imperatoria has a custom framework for making games, this framework was made by, and is still being managed by **Madonox**.

## Setup
In order to setup the framework, you must first define it and call the `init` function.  Below is an example of how to do this on both the server and client.
**Server:**
```lua
-- In server script.
local framework = require(game.ReplicatedStorage:WaitForChild("TalibratisFramework"):WaitForChild("TalibratisFramework"))
framework:init(script)
```

**Client:**
```lua
-- In local script.
local framework = require(game.ReplicatedStorage:WaitForChild("TalibratisFramework"):WaitForChild("TalibratisFramework"))
framework:init(script)
```
**Please note, it takes 3 seconds for the client to load, as the client waits 3 seconds to ensure the server is loaded.**

## Services
The framework comes with many services to make scripting easier, below are a list of services, and how to use them.

### CreateService
CreateService is a service that is made to make creating instances much easier, as well as doing it in an optimized manor.

Usage:
```lua
local CreateService = framework:GetService("CreateService")
local part = CreateService:create("Part",game.Workspace,{BrickColor=BrickColor.new("Really Blue"),Material=Enum.Material.Neon})
```
Methods:
The `create` method allows you to create an instance with an assigned parent, as well as a table containing properties of the instance.

### ClassService
ClassService is currently work in progress, do not try to use it.

### GlobalSyncService
GlobalSyncService is a service that allows you to sync a timer up to the real world time.

Usage:
```lua
local GlobalSyncService = framework:GetService("GlobalSyncService")
print(GlobalSyncService:GetTime()) -- Prints time since server start.
GlobalSyncService:TimeDelay(3,function()
  print(GlobalSyncService:GetTime()) -- Will print time three seconds after first print, it's basically a delay function.
end)
```

Methods:
The `GetTime` method will get the time passed since the server start.
The `TimeDelay` method will wait until specified time passes, then execute the supplied function.

### MouseService
MouseService is a service that works ONLY on the client, and it returns a dictionary that looks like a mouse instance, with similar events such as Move.
Usage:
```lua
local MouseService = framework:GetService("MouseService")
MouseService.Move:Connect(function()
  print("Mouse moved.")
end)
```
Please note, this service is NOT complete, and is subject to change.

### NetworkService
The NetworkService provides better communication methods between server and client, such as setting up methods, sending packets, and much more!

Usage:
**Server:**
```lua
local NetworkService = framework:GetService("NetworkService")

NetworkService.add("testFunction","event",function(player,args) -- Args will be a piece of data send by client, normally a table.
  print(player.Name.." has sent over the following args: ")
  print(args)
end)
```

**Client:**
```lua
local NetworkService = framework:GetService("NetworkService")
while wait(3) do
  NetworkService.send("testFunction",{"hi","hi2"})
end
```


-------------------------
Go home: https://talibratis-architype-industries.github.io/Docs/framework
