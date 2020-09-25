# Tinyquest
Tinyquest is a Rust library aiming to give you a high-level, yet performant experience. The binary size is minimal, to make small bundled CLI's which need to make requests plausible.

## Usage
To use `tinyquest`, add this to your `Cargo.toml`:
```
[dependencies]
tinyquest = "0.2"
```
Then, add this to your crate:
```
use tinyquest::{get, write};

fn main() {
  // ...
}
```
## Examples
Request a website, and print the HTML:
```
use tinyquest::get;

fn main() {
  match get("rust-lang.org", "my-application/0.1.0") {
    Err(err) => eprintln!("Failed: {:?}", err),
    Ok(result) => {
      // Block the current thread
      match result.get() {
        Ok(s) => {
          let (parts, body) = s.into_parts();
          println!(
            "Headers: '{:#?}'\n\
            Body: '{}'",
            parts.headers,
            String::from_utf8_lossy(&body),
          );
        }
        Err(err) => eprintln!("Failed: {:#?}", err),
      };
    }
  };
}

```
## License
This crate is licensed under the MIT license, and all contributions must also be.