- By Brian Lonsdorf
  Salesforce
  https://github.com/FrontendMasters/hardcore-functional-architecture/
- Reader Monad can inject into a chain
  ```
  const Fn = run =>
  ({
    run,
    chain: f => Fn(x => f(run(x)).run(x)),
    map: f => Fn(x => f(run(x))),
    concat: other =>
      Fn(x => run(x).concat(other.run(x)))
  })
  Fn.ask = Fn(x => x)
  Fn.of = x => Fn(() => x)
  ```
  Example:
  ```
  const res = Fn.of('hello')
                      .map(toUpper)
                      .chain(upper => 
                          Fn.ask.map(env => [upper, env])
                      )
  
  console.log(res.run({ port: 3123 }))
- ```