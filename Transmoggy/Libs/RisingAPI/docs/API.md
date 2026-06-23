# RisingAPI

## Basic usage

The library can be loaded using `LibStub`:

```lua
local RisingAPI = LibStub("RisingAPI")
```

The transmog module (which is currently the only relevant module) can be accessed via `RisingAPI.Transmog` and provides multiple methods to query or update your transmogs. As an example, you can query your current shard balance like this:

```lua
RisingAPI.Transmog.GetBalance():next(function(result)
	print("Your transmog shard balance is: " .. result.shards)
end)
```

The return value of `GetBalance()` is a so-called promise (or future). If you are not familiar with this concept, please refer to the documentation [here](Promise.md).

A reference of all available methods within the transmog module can be found [here](Transmog.md).

## Error handling

Requests to the API can fail because of invalid inputs or other problems. If a request fails, the returned promise is rejected which can be handled like this:

```lua
RisingAPI.Transmog.GetBalance():next(function(result)
	-- handle result
	-- will not be called in case of an error
end):catch(function(err)
	print("An error occured: " .. err.message)
end)
```

If a promise returned from the API rejects, the error will always be a table with a `message` property which explains the problem.

Note that if you do not handle errors like this, they will be silently ignored.

Also note, that any error caused within the catch-function itself will be propagated down into the promise-chain which in most cases means that it is silently ignored. As an example, the catch-function in the following example contains a bug: You cannot concatenate strings using the `+` operator in lua. Given that this problems occurs within the catch-function, it is silently ignored and won't be displayed.

```lua
RisingAPI.Transmog.GetBalance():next(function(result)
	-- handle result
end):catch(function(err)
	print("An error occured: " + err.message)
end)
```

## Events

The API supports various events that are sent by the server. You can register to an event like this:

```lua
RisingAPI:registerEvent("transmog/balance/changed", function(newBalance)
	print("Your new transmog shard balance is: " .. newBalance.shards)
end)
```

The second parameter is an event handler function that will be called whenever the event is triggered and will receive a table with information about the event as its first parameter.

For a list of available events, please refer to the documentation of the [transmog module](Transmog.md).
