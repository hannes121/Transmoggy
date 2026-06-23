# RisingAPI

Lua library for accessing the Rising Gods Addon API.

## Example

```lua
local RisingAPI = LibStub("RisingAPI")

RisingAPI.Transmog.GetBalance():next(function(result)
	print("Your transmog shard balance is: " .. result.shards)
end):catch(function(err)
	print("An error occured: " .. err.message)
end)
```

## Documentation

Documentation can be found in the [docs subfolder](docs/API.md).

## Feedback

Got any questions or suggestions? Please open a thread on the [feedback forum](https://www.rising-gods.de/forum/13-anregungen-a-rueckmeldungen.html).
