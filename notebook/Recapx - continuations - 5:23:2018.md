#Continuations
@joelhelbling
Used for flow control

Called fibers in ruby
Called coroutines in lua
Called generators in javascript
```
function * hi() {
  console.log('1')
  yield
  console.log('2')
}

const it_hi = hi()
hi.next()
hi.next()


```

Sets up fibonacci function that runs once and yields
Then an outer loop can run the continuation as often as you want - first 10 for instance
Inner function doesn't know about it's flow control - it just runs infinitely


Can be used to create pipelines in ruby - each operation is a fiber that yields
Aha! - `shifty` gem cleans up that DSL nicely

Continuations are described somewhat as "mulitthreading", but it's more useful to think of them as infinite iterators.
"Cooperatively passing flow control around"
