# Retry

## Defition (One sentence spine):
- retry refers to automatically trying again the failed requests
- Requests in distributed systems are transcient in nature, 
- retry can handle the temporary errors or timeouts 
- but if not handled carefully they can amplify the load with requests that can lead to disasters.

## Retry story
- downstream requests (onward or calling requests) are slow
- system timeouts
- service retries multiple times
- downstream system is still slow and can not queues are now filled with incomplete requests
- load increases
- whole system is impacted

## Why they exists (Why retry is important)
### In distributed system temporary errors are very frequent
- due network packet lost
- due to timeouts
- due to GC pause
- due to master node elections
- resource allocation
etc

### If we do not retry 
- it will look like a permanent failure
- user experience is impacted
- wastage of resources as requests are initiated but failed
- number of errors increased
- Availability and Reliability of the system impacted

### With 3 retries the availability of the system increases from 99.9 to 99.999 percent

### small scenario
- User is about to make a payment and press pay button
- due to some packet drop, the request fails and shows error
- if the reties are implemented, the request will be retried and user wont be able to figure out if some error has occured
- without retry the request will failed and user will be shown error message; when user press pay button again this time payment is succeeded; bad experience for user

## Why retry is dangerous, if not handled carefully
- non idempotent request will create multiple entries
- all type of errors are not for retry, 500 range errors, validation errors are not for retry.
- retry increase network load and traffic
- extra resources are used
- retry should not fixed, should be dynamic and jitters should be added


## Extra care required for retries
- Exponential backoff
- Random jitters while retrying
- Retry budget - retry count should be according to the traffic
- Retries should stop when they are making things worse.



