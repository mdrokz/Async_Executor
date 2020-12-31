# Async_Executor
simple bare bones executor for async futures in rust.


# Queuing async operations to a limited amount

```rust

use crate::executor::{new_queue_executor_and_spawn, SyncExecutor, SyncSpawner};

let (executor, spawner): (SyncExecutor<String>, SyncSpawner<String>) =
        new_queue_executor_and_spawn(3);
        
  for _ in 0..3 {
  
    spawner.spawn(async {
        println!("hello world");
        30
    })
  }      
  
  executor.run_queued(Box::new(|v| {
        println!("V {}", v);
    }));

```

# Normal Async Executor


```rust

  use crate::executor::{new_executor_and_spawner, Executor, Spawner};

let (executor, spawner): (Executor<'_, String>, Spawner<'_, String>) =
        new_queue_executor_and_spawn(3);

  spawner.spawn(async {
        println!("test");
        30
  });
  
  
  let r = executer.block_on();

  // for running an async loop

  // executor.run(Box::new(|v| {
  //      println!("V {}", v);
  //  }));

```
