# Dioxus-webview

Dioxus-webview bridges virtual and Webview DOMs together to make simple, portable, desktop applications. 

Dioxus-webview is an attempt at making a simpler "Tauri" where creating desktop applications is as simple as:

```rust
// main.rs
fn main() {
   dioxus_webview::new(|ctx| {
       let (count, set_count) = use_state(ctx, || 0);
       html! {
            <div>
                <h1> "Dioxus Desktop Demo" </h1>
                <p> "Count is {count}"</p>
                <button onclick=|_| set_count(count + 1) >
                    "Click to increment"
                </button>
            </div>
       }
   })
   .configure_webview(|view| {
      // custom webview config options 
   })
   .launch();
}
```

and then to create a native .app:

```
dioxus bundle --platform macOS
```

## Goals

Because the host VirtualDOM is running in its own native process, native applications can unlock their full potential.  Dioxus-webview is designed to be a 100% rust alternative to ElectronJS without the memory overhead or bloat of ElectronJS apps.

By bridging the native process, desktop apps can access full multithreading power, peripheral support, hardware access, and native filesystem controls without the hassle of web technologies. Our goal with Dioxus-webview is to make it easy to ship both a web and native application, and quickly see large performance boosts without having to re-write the whole stack. As the dioxus ecosystem grows, we hope to see 3rd parties providing wrappers for storage, offline mode, etc that supports both web and native technologies.