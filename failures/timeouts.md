# timeout

## Definition (what is timeout): 
- timeout is setting boundaries and telling system not to wait indefinetly.
- timeout meaning ending the unbounded wait.
- timeout says I do not care if system is slow or if system is going to die, i will not wait and i will stop the waiting.

## Why waiting foreever is worse then failing (why timeout is necessary)
- failing fast hurts one request.
- waiting foreever hurts the entire system (Refer latency document for compounding effect and failure propagation of latency)

## How timeout saves system (how)
- timeout sets boundaries for waiting
- timeout turns infinite waiting into finite decision
- turns uncertainity into a controlled system
- stops one slow dependency from poising whole system

## If timeout doesn't exists
- System has no edge
- failure bleed everywhere
- whole system is impacted

## Places where we usually forgets to put timeout
- http requests
- RPC requests
- cache lookups
- DB queries

## Issues how people handles timeout
- long timeouts are a trap, it increases resource holding time
- long timeouts hide other performace issues

## timeout-retry (what happens after a timeout)
- if retry blindly
- if retry immediatly
- if retry without limits
### we just created a retry storm


## Final conclusion about timeout
- Timeouts do not guarantee correctness
- Do not guarantee availability
- Do guarantee bounded damage


