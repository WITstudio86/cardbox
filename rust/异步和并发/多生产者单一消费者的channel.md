#rust/thread 

- mpsc 是多生产者单一消费者的 channel
	- **multiple producer signle consumer**

```rust
use std::sync::mpsc::channel;

fn main() {
    // 创建一个通道，用于在线程之间传递数据
    let (tx, rx) = channel();

    let tx1 = tx.clone();
    // 创建一个新线程，用于发送数据
    let thread1 = std::thread::spawn(move || {
        // Send data to the receiver
        // 向接收者发送数据
        tx1.send("Hello from thread 1").unwrap();
    });

    let tx2 = tx.clone();
    // 创建一个新线程，也用于发送数据
    let thread2 = std::thread::spawn(move || {
        // Send data to the receiver
        // 向接收者发送数据
        tx2.send("Hello from thread 2").unwrap();
    });

    // 创建线程用于接收两者的数据
    let thread3 = std::thread::spawn(move || {
        // Receive data from the sender
        // 从发送者接收数据
        let received1 = rx.recv().unwrap();
        let received2 = rx.recv().unwrap();

        println!("Received: {} and {}", received1, received2);
    });

    // 等待所有线程完成
    thread1.join().unwrap();
    thread2.join().unwrap();
    thread3.join().unwrap();
}

```