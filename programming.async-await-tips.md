Tips for using async await.

async -> awaiting

async implies awaiting

await iff async is present

await if and only if async is present

Does this function need to respond to external events or wait on external connections to get or send data?
Use an async function

example: wait on network i/o, client requests, database request

async run_async_fn() {}

fn main() {
    loop {
        run_async_fn().await;
    }
}

By .await-ing the learn_song future, we allow other tasks to take over the current thread