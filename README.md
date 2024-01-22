# Collector
Generated by [Rojo](https://github.com/rojo-rbx/rojo) 7.3.0.

## Wally Installation
To install with wally, insert it above wally.toml [dependecies]
```toml
Collector = "ernisto/collector@0.1.2"
```

## Usage
```lua
local eternalTrash = Collector()
local trash = Collector{ lifetime=5 } --:collect() after 5 seconds

trash:add(Instance.new('Part'))
trash:add(workspace.ChildAdded:Connect(warn))
trash:add(Promise.try(fetchData, player))
trash:add(FastSignal.new():Connect(print))

local callback, thread = trash:add(
    function() print('collected') end,
    task.delay(2, print, 'cavalo')
)
trash:remove(callback, thread)

local subTrash = trash:sub{ lifetime=2 }
subTrash:add(print)

trash:collect() -- auto subTrash:collect()
trash:destroy() -- backport for :collect()
```