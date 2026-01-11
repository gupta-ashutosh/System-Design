# Idempotency

## Definition(One statement spine)
- Idempotency is the ability of the system to make sure the usual effect happens on multiple re-attempts as happend for the first time.
- Idempotency make sure no duplicate states are created on re-attempt of request.
## Story to remember
- User start the payment request
- Server received the request and processed it.
- Response from the server got lost and user sees a error message.
- User re-attempts the payment and repeat payment occurs

## Why idempotency exists
### Retries are blind and uncontrolled
- does not know if request is failed
- does not know if response is failed
- does not know if partial processed.

## How we achieve idempotency
- By detecting the duplicate requests
- By using de-duplicate effect
- By rejecting the duplicate requests

