Closures that steal

There's a problem with this code
```rs
use std::thread;
fn start_sorting_thread(mut cities: Vec<City>, stat: Statistic) -> thread::JoinHandle<Vec<City>>
{
    let key_fn = |city: &City| -> i64 { -city.get_statistic(stat)};
    thread::spawn(|| { // new thread runs in parallel with caller
                       // 
                       //  the new thread created by thread::spawn can’t be expected to finish its
                       // work before cities and stat are destroyed
        cities.sort_by_key(key_fn);
        cities
    })
}
```

Solution: give cities and stat to their closures with `move`
```rs
/* The first closure, key_fn, takes ownership of stat. Then
the second closure takes ownership of both cities and
key_fn. Note the use of `move`.*/
fn start_sorting_thread(mut cities: Vec<City>, stat: Statistic)
-> thread::JoinHandle<Vec<City>>
{
    let key_fn = move |city: &City| -> i64 { -city.get_statistic(stat) };
    thread::spawn(move || {
        cities.sort_by_key(key_fn);
        cities
    })
}
```