```rust
use log::info;
use std::time::{Duration, SystemTime};

#[macro_export]
macro_rules! timer {
    ($expr:expr) => {{
        let start_time = SystemTime::now();
        let result = $expr;
        let duration_time = SystemTime::now()
            .duration_since(start_time)
            .unwrap()
            .as_millis();  //使用as_nanos可以提升精度
        println!("本次查询耗时：{:.2}s", duration_time as f64/ 100.0);
        info!("本次查询耗时：{:.2}s", duration_time as f64/ 100.0);
        result
    }};
}
```
使用该宏可以记录函数运行时间，在使用时使用timer!(Fn)，其中Fn为需要跟踪的函数。